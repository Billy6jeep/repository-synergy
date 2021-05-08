code-by-voice
=============

In this repository you will find all the support files for my "code by voice" setup using Dragon Naturally Speaking and DragonFly. I was inspired to do this by Tavis Rudd (https://github.com/tavisrudd). You can see his excelent presentation from PyCon here: http://youtu.be/8SkdfdXWYaI

### !!! WORK IN PROGRESS !!!

## Requirements

* Dragnon Naturally Speaking - You can use any edition (including home). The advantage of using the Premium Edition, based on talking to the rep from Nuance, is that the Premium edition will let you backup the voice traning directly from DNS.
* Windows 8.1
* DragonFly
* Natlink / Unicode
* Python 2.7
* Virtualization Software (VMWare, VirtualBox, Parallels) if you are setting this up on Mac OS X or Linux

## Resources

* Dragon Naturally Speaking (http://www.nuance.com/dragon/index.htm)
* DragonFly (http://code.google.com/p/dragonfly/)
* Unimacro (http://qh.antenna.nl/unimacro/index.html)


## Getting Started

Here are the steps to get your system installed and running.

!!! These are a work in progress !!!

1. Install Windows 8 (7 and XP works too) 
1. Install Dragon Naturally Speaking (and go through the training)
1. Download Python 2.7 (http://sourceforge.net/projects/natlink/files/pythonfornatlink/python2.7.zip/download)
2. Extract the download
1. Install python-2.7
2. Install pywin32-218.win32-py2.7
3. Install PyXML-0.8.4.win32-py2.7
1. Install wxPython2.8-win32-ansi-2.8.12.1-py27
1. Add PATH enviroment variable for C:\Python27 and C:\Python27\Script (Right click on computer, click on Advanced system settings, click on Enviroment Variables)
1. Download easy_install.py (https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py)
1. Download Natlink (http://qh.antenna.nl/unimacro/installation/installation.html)
2. Install Natlink (Just double click the installer)
1. Download DragonFly Zip File, not the windows installer (http://code.google.com/p/dragonfly/downloads/list)
1. Exract dragonfly-0.6.5.zip
1. Install DragonFly (inside the dragonfly-0.6.5 directory run "python setup.py install")
1. Enable Natlink via GUI (using the start menu)
1. Restart Dragon NaturallySpeaking
