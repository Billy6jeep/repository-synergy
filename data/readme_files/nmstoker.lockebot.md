# lockebot

![LockeBotLogo](media/JohnLockeLogoMini.jpg)

**LockeBot:** a demonstration of implementing a basic question answering bot with use of [Rasa NLU](https://github.com/golastmile/rasa_nlu) and a database.

## What is this?

It is a bot that can answer simple questions, via the terminal, email, [Let's Chat](http://sdelements.github.io/lets-chat/) or [Facebook Messenger](https://messenger.fb.com/)

After being trained on examples, it is (to a degree) able to generalise the questions and respond to ones in a similar style. The questions are turned into intents and entities, which are then used to construct queries to run against a database to provide the answer.

Here is a demo of the RoyBot version :crown: (which is trained/coded to answer a range of different questions on English and British monarchs) When it's running, you can access it live on Facebook Messenger [here too](https://www.facebook.com/RoyBoticUK/)

[![asciicast](https://asciinema.org/a/buhysdhqvytr8sgq89t8bvqf4.png)](https://asciinema.org/a/buhysdhqvytr8sgq89t8bvqf4)

This project grew out of my experiments to build a bot in Python using Rasa NLU. I should be up-front that this is not necessarily the perfect way to use it and there are probably many things that could be done in a more Pythonic way, but my intent is that by sharing it, others will either be able to get something basic working quickly or they'll use it for inspiration in another project.

Rasa NLU has the great advantage of letting you handle your NLU models locally and thus not hand off data to a third-party.  I'm not idealogically against use of third-party NLU tools, but when getting a sense of what is possible it seemed to me very useful not to require external involvement and I suspect others may be in this position too.

One interesting option with this project is to run the finished bot on a [Raspberry Pi](https://www.raspberrypi.org/).  Although you may well not wish to train the model on the Pi (it may take a rather long time!), once you have a trained model, it is capable of giving responses quickly and although large scale use will likely not be viable it works for small numbers of concurrent users (no testing on maximum numbers has been done, but email-based use with a group of ~20 users is definitely viable)

There is a **BaseBot** (which does very little) and a slightly more capable version **RoyBot** :crown: (which answers questions about English/British monarchs) 

## Install

Ensure you have Python 2.7 installed (it is not currently compatible with Python 3.n, see below)

For Raspberry Pi installation, there are a couple of changes to the steps for installation. See information under Additional installation choices below.

* You may need to include the Python headers. On Debian/Ubuntu distros this is done as follows: 
	* `sudo apt-get install python-dev`

* Git clone from this repo
	* `git clone https://github.com/nmstoker/lockebot mybotfoldername` - *replace __mybotfoldername__ with any valid name you like*
	* `cd mybotfoldername`
* Create a virtual environment (optional but recommended; you need the one that corresponds with Python 2; on Arch this is `virtualenv2` but on many other distros it will be plain `virtualenv`)
	* `virtualenv2 venv` - *again you can use whatever name you like instead of __venv__ for your environment name*
* Activate the virtual environment
	* `source venv/bin/activate`
* Use pip install
	* `pip install -r requirements.txt`
* Manually install MITIE (*doesn't seem to work if included via requirements.txt even with "-e git+https://github.com/mit-nlp/MITIE.git" with or without #egg=...*)
	* `pip install git+https://github.com/mit-nlp/MITIE.git`
* Copy the feature_extractor files to MITIE folder
	* These instructions are simply the same as required by the backend set up steps for Rasa NLU under [Option 1 here](http://rasa-nlu.readthedocs.io/en/latest/backends.html)
	* Download the tar bzipped file from [here](https://github.com/mit-nlp/MITIE/releases/download/v0.4/MITIE-models-v0.2.tar.bz2)
	* Extract the contents temporarily and copy **total_word_feature_extractor.dat** into the **/MITIE** folder in sub-folders **/MITIE-models/english/**
	* You do not need the other files from the tar file
* Train models or copy existing ones into place
	* For training steps, see below (Usage) otherwise download the models from this Google Drive location:
	* https://drive.google.com/drive/folders/0B3K9eUuGgfbva2JUY2tYejc2ODg?usp=sharing
	* **/model_20170124-010214/** is required for BaseBot
	* **/model_20170423-110538/** is required for RoyBot
	* Save them in the '/models' folder of your local copy of the repo

If you simply wish to use the local terminal to work with the bot, you are ready to proceed to Usage.

But if you wish to use it via email or Let's Chat, see the addition requirements below.

### Additional installation choices

#### Raspberry Pi installation

* You may need to include the Python headers and ATLAS/BLAS libraries (this is so that Numpy/Scikit can be installed:
	* `sudo apt-get install python-dev`
	* `sudo apt-get install libatlas-base-dev`
	* `sudo apt-get install gfortran`
* It is a matter of how you plan to work, but you can install it directly from a repo or you may wish to transfer the files from a regular PC to the Pi. The latter is fine, so long as you don't copy the virtual environment files over (since they need to be created via the Pi)
* When running `pip install -r requirements.txt` you should expect to see a large amount of output as items are compiled (including a number of warnings, but you should be okay to ignore these unless something doesn't complete). It can take quite a while too (maybe 60+ minutes or so)
 

#### Let's Chat
Let's Chat has a variety of ways that it can be set up - for advice on that, please refer to the instructions in their repo's wiki [here](https://github.com/sdelements/lets-chat/wiki).  For development, I found docker very quick to get going with.  (NB: although LockeBot will work on a Raspberry Pi, no efforts have been made (yet!) to see if Let's Chat is viable on the Pi so I have no advice on that front)

Look at [config_roybot.ini](/config/config_roybot.ini) in the Let's Chat section and update them as necessary to point to your particular Let's Chat instance. The primary one to focus on is **base_url** and this should correspond to a room that you have set up in the Let's Chat. The bot will respond to all questions posted by users in the user_filter list who post in that room (there is no concept of the bot being directly addressed, eg @roybot Who was...).

Start the roybot.py script with `--channel letschat`

#### Facebook Messenger
This is more involved to set up than the other methods, as you need an externally accessible webhook where the bot can be reached.

The [Quick Start](https://developers.facebook.com/docs/messenger-platform) documentation for the Messenger Platform is the best place to start, but in summary you will need to set up an App and a Page for the bot (it can be private). There are a variety of ways you can handle the webhook depending on the resources available to you, but a simple method is to use [Ngrok](ngrok.com) to tunnel your localhost so that Facebook can access it.

Configure these two environment variables for the script to pick up the private settings that you configure with Facebook:

* VERIFY_TOKEN
* PAGE_ACCESS_TOKEN

e.g. `export VERIFY_TOKEN=....` and `export PAGE_ACCESS_TOKEN=....`

and also one related to flask: `export FLASK_APP=fb.py`


Then run the script with `flask run`, which will start a local webserver (flask obviously!)  Messages sent via the Messenger app should be turned into posts made to the server, which are then processed by the bot and the replies intended for the users are sent back to Facebook via posts made to their server.

Initially only the developer(s) will be able to access the bot, but if you get through the approval process you can make it publically accessible.

See a YouTube demonstration here: https://youtu.be/r2sbmEDep5s

[![YouTube](media/FB_Messenger_two_pages_small.jpg)](https://youtu.be/r2sbmEDep5s)

When running, you can access it live on Facebook Messenger [here too](https://www.facebook.com/RoyBoticUK/)

#### Email set up

**Disabled currently - will be updated shortly**

To use LockeBot over email, it connects via IMAP and SMTP to an email account that you set up specifically for use with the bot.

Several major email services provide details the ability to connect with IMAP/SMTP - if this is not available for the email you wish to use, you will need to figure out how you can connect programmatically via Python (and re-write the necessary sections of code).

Dreamhost instructions for IMAP are here: https://help.dreamhost.com/hc/en-us/articles/215612887-Email-client-protocols-and-port-numbers

Gmail instructions for IMAP access are here: https://support.google.com/mail/answer/7126229?hl=en

Microsoft Outlook.com instructions for IMAP access are here: https://support.office.com/en-gb/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970

If you are with another provider, check the details with them.

You need:
* Account username / password
* IMAP server name
* IMAP port #
* SMTP server name
* SMTP port #

It is possible the IMAP and SMTP hosts will match but if they differ, ensure you have them the right way around. Also if there are differences in relation to the standard ports, you would need to adjust this in the script (I plan to migrate this to an .ini setting shortly)

Simply update the details in the file `/config/settings.ini`. If you have problems, it is worth using another email client to ensure that you are definitely able to connect with the particular credentials you have.

In the bot script (eg basebot.py), edit **CHANNEL_IN** and **CHANNEL_OUT** to reference **'email'** and **'email': True** respectively (CHANNEL_IN can only take one value at a time, but CHANNEL_OUT can be true for **'screen'** and/or **'online'** as well as **'email'**) 

Email has not been tested with providers other than Dreamhost so far.

The script polls the email fairly frequently - you may find that a less frequent polling is wise but that does lead to longer delays before questions are responded to.  The use of IMAP "IDLE" commmands is not currently implemented (although it would be an obvious improvement).

## Usage

### Regular Bot Use

* Navigate to the Lockebot folder
* Activate the virtual environment (*as per the name you chose when you installed Lockebot*)
	* `source venv/bin/activate`
* `python roybot.py` (*or python basebot.py if you want to start from the simpler basebot*)
* Enter questions and see how it responds :tada:

See command-line parameters below for more options with running.

See the commands section below, but a helpful one is 'q' to quit! (or use <kbd>Ctrl-C</kbd>)

**NB:** If you've been re-training the Rasa model, you will first want to ensure you've updated the details in the setting **metadata_file** in [config_roybot.ini](/config/config_roybot.ini)

### Command-line parameters

**NB:** Not yet implemented for basebot.py

`python roybot.py --help` - Lists parameter details

`--channel` - The input channel (screen / letschat). Default is screen.

`--config` - The location of the config file.
             E.g `--config ~/path-to-other-config/config_roybot.ini`
             Useful to quickly switch between environments (eg test and live)

`--loglvl` - The level at which logging is done (DEBUG / INFO / WARN).
             Not case sensitive. Default level is WARN.

### User commands (for local input only, ie 'screen')

There are a handful of simple command shortcuts that trigger actions / toggle useful features. To use them, simply type the associated letter into the bot as if it were regular input.  To avoid remote users causing havoc, these only work for local input (ie 'screen').

`q` - **Quit:** this quits the bot (as you would expect!) You can also use <kbd>Ctrl-C</kbd> to quit.

`t` - **Tag:** stores the details of the last intent in the tag file (*eg roybot_tagged.txt for RoyBot*), useful for marking particular problem question/answer items (NB: everything is logged to the history file too, but that can get unwieldy)

`c` - **Clear the screen:** exactly what you would expect it to do

's' - **Show Parse:** this toggles the output of what Rasa NLU recognised as the intent for each subsequent entry

'v' - **Verbose:** this toggles the response style. When off responses just show the data returned and when on the data is fed into the template system to try to generate a more meaningful sentence style response. By default it is true.

#### Setting logging levels

`w` - **Warning:** this is the default level of logging (on screen)

`i` - **Info:** in conjunction with **show parse** this usually gives enough to follow the basic reasoning behind an answer

`d` - **Debug:** prints all manner of details (*excessive for normal use, but can be handy*)

The commands are intercepted in the main loop, before user input is sent to Rasa, so they do not reach Rasa and do not need to be included in the training data. This differs from the way "demo" or "example" are handled, which are treated just like other intents.

### Training

There is training data [available here](/data/RoyBot.json) which you can use as an example to start with.

See the [Rasa NLU documentation here](http://rasa-nlu.readthedocs.io/en/stable/dataformat.html) for details of the format and options for editing it.

Details of how to train the model are covered [here](http://rasa-nlu.readthedocs.io/en/stable/tutorial.html#training-your-model), with the key step being:

`python -m rasa_nlu.train -c config/config.json`

Once that completes (*which can take a __long__ time*) you should have a newly dated model folder (eg **/model_201ymmdd-hhmmss/**), simply ensure that folder is within your **/models** folder and update the setting **metadata_file** in [config_roybot.ini](/config/config_roybot.ini). The next time the bot is run, it will pick up the new model.

## Platforms
Currently it is only tested on **Linux** (specifically [Arch](https://www.archlinux.org/) x86-64 and [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) on a Raspberry Pi 3)
In due course I would be interested like to support Windows and Mac - I have access to the former but not the latter, so if there's anyone keen to look into this on the Mac, volunteers will be gratefully received.

## Python versions
Whilst I would like to support Python 3.n, currently as Rasa NLU has a Python 2.7 dependency it is going to mirror that until support there is resolved.

## Technical background

Before digging into any detail about LockeBot, I recommend looking at the documentation here:

http://rasa-nlu.readthedocs.io/en/latest/

and definitely this excellent blog post by Alan that covers the background better than I could:

https://conversations.golastmile.com/do-it-yourself-nlp-for-bot-developers-2e2da2817f3d#.44xn1gg53

You may also benefit from having a browse of the [Github issues for Rasa NLU](https://github.com/golastmile/rasa_nlu/issues), which are quite active and a useful source of information.

What LockeBot does can be broken down into:

* Taking a sentence
* Using Rasa NLU to try to find the intent and entities
* With custom coded functions, turns those details into a query
* Run the query against the database
* Send the returned data to a template to try to construct an output sentence

The only part that has machine learning in it is Rasa NLU, the rest is effectively hard-coded but able to deal with a range of question types.

This is not necessarily the "right" or only way to handle this kind of problem, but LockeBot works by taking the intents and then splitting entities into ones that correspond to fields from the database the user wants back (usually "features") and ones that select the row (or rows) that the user is referring to.

To give an example from Roybot:

Given the question **When did Elizabeth I reign from?**

Rasa responds with:

`{'text': 'When did Elizabeth I reign from', 'confidence': 1.0773836417225164, 'intent': 'ruler_feature', 'entities': [{'start': 9, 'end': 18, 'value': 'Elizabeth', 'entity': 'name'}, {'start': 19, 'end': 20, 'value': 'I', 'entity': 'number-roman'}, {'start': 21, 'end': 31, 'value': 'reign from', 'entity': 'feature'}]}`

The intent is routed to the relevant function that handles it (handle_ruler_feature).  In there, the entity '**Elizabeth**' (a "name") and '**I**' (a "number-roman") are used to select the row of interest (ie the one for Elizabeth I) and the "feature" here is '**reign from**'.

Thus a SQL statement with "Elizabeth" and "I" being used in the WHERE clause selects the desired row, and the feature of 'reign from' is mapped to the database field ReignStartDt and put into the list of returned fields for the SELECT (along with RulerId and RulerType which are useful to know for the template responses).

The ways these steps are done could quite probably be improved, made more flexible and sophisticated, but an aim was not to get too detailed that it would be a challenge to follow and as this is not trying to be a production system building in more sophisticated features did not seem necessary right now.  Plus of course it works fairly well!

A similar kind of problem is solved by [QuePy](https://github.com/machinalis/quepy) but it doesn't generalise the questions in quite the same way.

## Roadmap

This project is a personal project that I've decided to open-source - whilst I would like it to work well for people, and am keen to make improvements to it, I am likely to have somewhat limited time in the near-term (H1 2017) so expect changes to be relatively slow (however don't be deterred from forking it if you like!)

* put in some tests!
* 

## Name origin
LockeBot gets its name from a terrible pun. It is built on Rasa NLU, and [John Locke](https://en.wikipedia.org/wiki/John_Locke) (the philospher) was notable for his work in relation to the empty slate arguments regarding the mind, called tabula rasa.

## Additional demo material

* [Quick demo of BaseBot version](https://asciinema.org/a/5j5zs42kk95itm1uzdqlwys86) - shows some simple questions, along with parse on and the demo feature.

## Disclaimer
I am very grateful for the various tools which make this small project possible, however I should make clear that this software is not endorsed by any of the email providers mentioned above, Let's Chat, nor LastMile (producers of Rasa NLU).

## RoyBot data
The sqlite database for RoyBot has been populated with information gleened from public sources on the web, chiefly:

* https://en.wikipedia.org/wiki/List_of_English_monarchs
* https://en.wikipedia.org/wiki/List_of_British_monarchs

It is still a work-in-progress! :smiley:
