===============
About autoforms
===============

create by jeffkit (http://jeffkit.info,@jeff_kit)

autoForms is a Django application with which you can create,modify forms in Admin Panel,and then use the form for information collecting.

------------------
Who need autoforms
------------------

- polling.
- information collecting.
- custom form in workflow.
- you want a dynamic form in your django application.
- etc.....

-----
Links
-----

Browser Source on github : https://github.com/jeffkit/autoforms/

Try the Demo (login:form,password:form) : http://f.jeffkit.info/admin/

----------
how to use
----------

step1: install 

- install from source
git clone git@github.com:jeffkit/autoforms.git
cd autoforms
python setup.py install

step2: config your django project

edit settings.py , add 'autoforms' 'django.contrib.admin' to INSTALLED_APPS.
edit urls.py, uncomment admin url configs.
if you want to receive email when someone submit the form,set
NOTIFY_FORM_CHANGE = True and config the send mail staffs.

You can also cd to the sample directory, I made a empty project for you:
cd sample

step3: syncdb
python manage.py syncdb

step4: done,have fun! go and create your own forms.
python manage.py runserver

visit: http://localhost:8080/admin

     
=================
欢迎使用AutoForms
=================

作者 jeffkit (http://jeffkit.info 、@jeff_kit)

AutoForms是一个Django的应用，通过它，你可以通过非编程的手段在程序运行的过程中定义、创建、修改表单甚至保存表单数据。

---------
使用场景
---------

- 投票，调查
- 信息收集
- 工作流中的自定义表单
- 你需要用到动态表单的Django应用程序
- 等等.....

----
链接
----

到github浏览源码 https://github.com/jeffkit/autoforms/

试用(login:form,password:form) http://f.jeffkit.info/admin/>

-------
如何使用
-------

第一步：安装

或从源码安装：
git clone git@github.com:jeffkit/autoforms.git
cd autoforms
python setup.py install

第二步：配置

修改项目的settings.py文件，将'autoforms'加入INSTALLED_APPS中。
如果需要在用户提交表单后接收系统通知，则设置 NOTIFY_FORM_CHANGE = True ，同时设置发送Email的其他参数。

如果想快速体验，你可以直接使用我为您提供的sample项目。
cd sample

第三步：创建数据表
python manage.py syncdb


第四步： 完成，开始使用吧。
python manage.py runserver
访问http://localhost:8080/admin

