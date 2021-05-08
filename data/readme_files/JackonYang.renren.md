人人网信息抓取与数据挖掘
========================

人人网安全措施加强了，无法抓取原本没有权限访问的内容了。

不过，通过浏览器可以访问的内容，依旧可以抓取。

环境要求
--------

* ubuntu/win7/xp 皆可。
* python3.2 --> python2.7
* igraph/pycairo: 作图依赖该组件。
	ubuntu 下使用 `apt-get install python3-igraph` 即可。
	win32 版本下载并安装 [igraph](https://pypi.python.org/pypi/python-igraph/0.6.5) [pycairo](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pycairo)
* mysql: 仅当使用mysql作为存储介质依赖该组件。

简单用法
--------

#### 人人网账号/密码配置

 `config/spider.ini` 中根据提示配置即可。

#### 抓取人人网信息

<pre><code>
# 抓取好友的好友列表，用于显示个人的好友关系图。
$ python3 get_info.py getNet2
# 正常的运行结果显示如下：
spider login success. rid=498934189
15:14:09 get net1 of 498934189
15:14:09 get net2 of 498934189,toSearch/total:40/40
</code></pre>

#### 图像显示好友网络结构图

<pre><code>
$ python3 net_graph.py
</code></pre>

结果显示如下：

注：此处因为 igraph 插件的字符编码问题，好友姓名未能正常显示。

![relationship network graph][netgraph]

[netgraph]:test_net_graph.png

功能列表
--------

#### 人人网爬虫

1. 自动登录人人网并抓取 friendList, status, profile 等信息。
2. 支持长时间(40h+)持续运行，支持断点续抓。
4. 页面超时，自动重发 3 次请求。
3. 支持 run/debug 日志。run 日志记录抓取成功/失败信息，debug 日志用于调测。
5. 可灵活扩展多种本地存储方式，现已支持: myql, file

#### 好友关系图

绘制特定用户的好友关系图，方便分析人际关系网络。

暂时可获取以下关键信息：好友圈子结构、关键好友、男/女朋友。

#### 话题分析: 
	
对状态进行自然语言分词和关键词分析，统计关心的话题。

#### 联系频率

分析状态中的~@/转发/回复~信息，统计联系频率分布规律。

一些结果
--------

#### 状态数与关键词数量关系图

近似直线，貌似意义不大。

![relationship between number of status and number of keywords][demoTopic]

[demoTopic]:topic/nstatus_nkeyword.png


design
======

人人网信息抓取与本地存储，数据源：[www.renren.com](www.renren.com)

`renren_spider` 直接依赖于 `browser` 和 `repo`。
现已支持`repo`：mysql, file。
新增`repo`只需根据 interface-repo 接口规范实现相关接口，
创建`spider`实例前调用`set_repo(module_name:str)`即可。

* browser:抓取页面并返回 record 和 运行信息（timecost or error info)。<br>
* repo: 本地保存 record 和 download history，提供读写接口。

INTERFACE
---------

最新接口，参考单元测试用例。
架构改动以前，不更新此处的接口说明。

#### browse 
* `pageStyle(renrenId) --> (record:dict,timecost:str)` 下载 pageStyle 页面的信息字段。
* `login(user,passwd) --> (renrenId,info)` 社交网站登录

#### repo
* `save_pageStyle(record, rid, run_info) --> nItemSave` 保存 record 和 history
	pageStyle list: friendList, status
* `getSearched(pageStyle) --> rids:set`
* `getFriendList(rid) --> friendsId:set`

#### spider
* `login() --> same as browser.login()` login [www.renren.com](www.renren.com)
* `getStatus_friend(rid) --> None` get status of rid's friends
* `getNet2(rid) --> None` get friendList of rid's friends

design of modules
-----------------

### browser：

1. `_download`<br>
简单的根据 url 获取 `html_content` 并返回给上层调用，便于性能统计。

2. `_iter_page`<br>
页面类型分为：迭代的多页面，如 friendList, status; 单页面，如 profile,homepage。<br>
实际抓取以迭代页面为主，对方出于性能考虑，通常鉴权较少，安全策略低。<br>
`_iter_page` 迭代调用`_download`获取`html_content`并识别出其中的 items。

3. parse <br>
解析 `_iter_page` 得到的 items, 获得信息字段 record。返回 dict()。<br>
迭代页面一般包含多个 item，每个 item 有自己的 id。以此作为 dict 的 key。<br>
单页面一般包含多个字段，可以处理为 tag = value 格式。以此作为 dict 的 key 和 value。

**内部接口规范**

1. `_download(url:str) --> html_content:str`
2. `_iter_page(pageStyle,rid)  --> (items:set,'success'/error_info:str)` info is success or error info
3. `parse.pageStyle(items:set) --> record:dict() `

_parse.pageStyle 每次只解析一个用户特定 pageStyle 的字段_

###  repo-mysql：

环境依赖:

* mysql, 
* pymysql: [installation package link](https://github.com/petehunt/PyMySQL)

配置:

2. 在 `db_renren.ini` 中配置数据库信息，通常只需修改 `host`,`user`,`passwd`

以 mysql 作为本地存储介质。

每一类 `pageStyle` 一个接口，若传递了 `run_info` 字段，则自动写 `history`

1. `save_pageStyle` 存储 record 和 history
3. `self.table` 内部属性，已经确认创建的表空间及表名。
4. `_init_table` 根据 pageStyle 创建表空间并初始化 `self.table`
5. `_getConn` 获取 mysql conn。数据库连接参数在 `db_renren.ini` 中配置。
2. `getSearched` 查询 history 表，获取已查询集合。
3. `get_friendList`

**内部接口规范**

1. `save_pageStyle(record:dict, rid:str) --> number_of_items_saved:int` call `_save_process` to save record and history
2. `_save_process(pageStyle:str, record:dict, rid:str, run_info:str) --> number_of_items_saved:int`
3. `_sql_pageStyle(record:dict,rid:str) --> sqls:list` called by `_save_process` to construct sqls
4. `_sql_create_table(pageStyle:str) --> sql` call by `_init_table`, read table info from config file and return sql for create table.

### parse

#### profile

**内部字段规范:**

1. gender:
	- 'f': female
	- 'm': male
	- 'u': unknown
	- None: error
2. birth:
	- `birth_year`: 4 digits, 9999 if empty. None if error
	- `birth_month`: 2 digits, 99 if empty. None if error
	- `birth_day`: 2 digits, 99 if empty. None if error
3. hometown:
	- string.
	- '': empty
	- None: error
4. edu: now/college/senior/junior/primary
	- school_name:string: if only one school name contains, such as edu_now in pf_mini
	- list with dict element, dict value is '' if empty
		- name: '' if empty
		- year: entrance year
		- major
	- []: empty
	- None:error

请求 profile 页面，可能返回 2 种页面，分别包含以下字段。

1. profile detail.
	- basic: birthday, hometown, gender
	- edu: college, senior, junior, primary, technology
	- work: company, period
	- contact: empty and no use. qq, msn,phone, domains, personal website
2. profile brief.
	- basic: gender, birthday, hometown
	- present: location/address, work, school

字段有效性分析：

1. school
	人人网自身实现不严格，导致大学、高中信息交叉重叠。<br>
	处理方式：初始化全国高校列表，以消除中学与高校的混淆。
2. 生日/星座
	资料解析+状态/分享分析
3. 年龄
	资料解析+高中好友平均年龄估计区间
4. 性别
	资料解析，通常可信度较高。
4. 家乡
	资料解析+中学好友分布分析
5. 现居信息--不处理
	可信度较低，少有人维护。
6. 工作信息--不处理
	数据规模太少。

### spider

各种功能方法中生成待抓取的 `rid` 序列，由 `seq_process` 抓取。

**内部接口规范**

1. `seq_process(toSearch:str/set,pageStyle:str)` download and save record
