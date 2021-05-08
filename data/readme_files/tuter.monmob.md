** MonMob project

This is a set of tools to provide monitor mode and raw frame injection for
devices using broadcom chipsets bcm4325, bcm4329 and bcm4330.

** Important Notes

Patching the firmware for monitor mode and raw frame injection will not
break the common functionality of the wireless card. The wireless card
will continue to work and you will be able to join networks.

In case you want to revert changes, bcm-patcher.py tool makes a backup of the
original firmware. To do this just overwrite the firmware with the backup
and reboot your device.

** Known Supported Devices

 + iPad 1 - iOS 5.0.1, 5.1.1
 + Galaxy Tab - Android 3.4

** Requirements

 + python
 + libpcap
 + tcpdump

** How to use it

 + iOS
   1 - Patch your firmware with bcm-patcher.py.
   2 - Copy tools/iOS/server/ioctl.py to a directory on your iPhone/iPad/etc.
   3 - Copy tools/iOS/aeropuerto.py to a directory on your iPhone/iPad/etc.
   4 - Execute aeropuerto.py to disable MPC and set the channel.
     # ./aeropuerto.py start 6
   5 - Start executing tcpdump.
     # tcpdump -i en0 -s 65535 -w monitor.cap ether host 88:88:88:88:88:88
   6 - Once we stop tcpdump execute monitor_mode_magic_pcap.py to extract
       the ethernet header and create a valid 802.11 pcap capture file.
     # /monitor_mode_magic_pcap.py monitor.cap test.cap
   7 - Execute aeropuerto.py to enable MPC.
     # ./aeropuerto.py stop

 + Android
   1 - Patch your firmware with bcm-patcher.py.
   2 - Start executing tcpdump.
     # tcpdump -i en0 -s 65535 -w monitor.cap ether host 88:88:88:88:88:88
   3 - Once we stop tcpdump execute monitor_mode_magic_pcap.py to extract
       the ethernet header and create a valid 802.11 pcap capture file.
     # /monitor_mode_magic_pcap.py monitor.cap test.cap

** Files

patcher/
    scripts to modify firmware.
tools/
    monitor-mode-magic.py

    iOS/
        server
        UI

** Greetings

