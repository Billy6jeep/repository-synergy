Latest Downloads:
https://github.com/ashdnazg/pyreshark/releases/tag/0.1.4

Windows Installer for all versions:
https://github.com/ashdnazg/pyreshark/releases/download/0.1.4/pyreshark_0.1.4_installer.exe

General Information
-------------------

Pyreshark is a plugin for Wireshark with the purpose of allowing other plugins to be written with:
    1. Python
    2. Ease
    3. Efficiency

The source code and some binaries can be found in https://github.com/ashdnazg/pyreshark

License
-------
Pyreshark is released under the GNU GPLv2 license. See <http://www.gnu.org/licenses/gpl-2.0.html> for details.

Installation
------------
Python 2.7.* or 2.6.* is required, so make sure it is installed.

Put pyreshark.dll in <Wireshark-Dir>\plugins\1.*.*\
Put all files in the python folder in <Wireshark-Dir>\python.

The overall directory structure should be:
<Wireshark-Dir>\python
<Wireshark-Dir>\python\cal
<Wireshark-Dir>\python\protocols

Using Pyreshark
---------------

To add an existing dissector just drop it in <Wireshark-Dir>\python\protocols

To write a new dissector see the guide at https://github.com/ashdnazg/pyreshark/wiki/Writing-Dissectors


Building Pyreshark
------------------
Currently the plugin was tested on win32, win64 and some linux distro's.

Win32/64 Instructions:

    1. Get Wireshark's source. (version 1.12 or 1.10 is required)
    2. Build Wireshark.
    3. Get pyreshark's source through hg clone.
    4. Place pyreshark's source in the plugins dir of Wireshark's source.
    5. Go to <WS_source_root>\plugins\pyreshark and run:
        nmake -f Makefile.nmake all
    6. If all went well, you can now copy the shiny new pyreshark.dll and python folder to your Wireshark installation.

Linux Instructions:
    1. Get Wireshark's source.
    2. Get pyreshark's source through hg clone.
    3. Place pyreshark's source in the plugins dir of Wireshark's source.
    4. If your Python dynamic library isn't named libpython2.*.so.1.0 or isn't in the search path, 
       change the PYTHON_* values in python_loader.h to the correct full path of the library.
    5. Follow the instructions in http://anonsvn.wireshark.org/wireshark/trunk/doc/README.plugins
    6. Build Wireshark and install it.
    7. If all went well, you should have the plugin installed as well. 
    
    
    
Contact
-------
I'd be more than happy to receive bug reports, suggestions and/or pleas for help through mail (<ashdnazg [AT] gmail.com>) 
and assist accordingly.
If further support or commercial work is required, I may certainly be contracted for projects of both open-source and closed-source nature.

Go wild.
