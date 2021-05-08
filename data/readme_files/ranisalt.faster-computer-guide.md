# ranisalt's guide to a faster computer

First of all, take your time to measure the bottlenecks. You can check if your boot time is reasonable with the `systemd-analyze` tool:

```bash
$ systemd-analyze
Startup finished in 3.104s (firmware) + 50ms (loader) + 914ms (kernel) + 1.409s (userspace) = 5.479s
```

And you can go deeper and check what takes most time to load from userspace passing the parameter `blame`:

```bash
$ systemd-analyze blame
           879ms psd-resync.service
           601ms docker.service
           319ms psd.service
           285ms dev-sdb3.device
           277ms wicd.service
           276ms user@1000.service
           135ms dev-sda2.swap
            86ms systemd-journald.service
(...)
```

## General recommendations
- **Disable unnecessary services**. You can check what are the major hogs with *systemd-analyze blame*, and it will list processes taking boot time, sorted by heavier first. Then, mask them with *systemctl mask <unit name>* and you're ready, and *systemctl unmask <unit name>* if something goes wrong. You will look forward to disabling Bluetooth, infrared, and even firewalls if you are not concerned with it.

---

- **Use a lighter display manager**. **SLiM** is always a good option, **LightDM** is good too. You can also go with no DM at all, shaving off precious time. If your distro comes with, consider disabling Plymouth too (we're going FAST, not EYE-CANDY).

---

- **Use a lighter bootloader**. GRUB can take a big time just running scripts. If you have only one boot option or you can use the UEFI bootloader, you can use lighter options such as **Syslinux** and **Gummiboot**, or if you are savvy you can give a shot to [EFI stub](https://wiki.archlinux.org/index.php/EFISTUB).

---

- **Use a lighter desktop environment (or none)**. Run away from **GNOME** and **KDE** if you are pursuing performance, as those giants can consume up to one gigabyte of memory and lots of CPU cycles. Opt to a lighter alternative, such as **XFCE** and **LXDE**, or even better, give up completely on DEs and use only a window manager, such as **dwm**, **i3** (my personal choice) or **xmonad**.

---

- **Avoid using fancy disk settings**, such as LVM, if you don't need to. Also, don't use encrypted partitions (*/home* is fine). Also remember to set your SATA disks to run in AHCI mode, not IDE.

---

- **Replace your HDD with SSD**. This is probably the simplest option. You don't need to run your entire system on SSD to get a boost, you only need to have your boot files (*/boot* partition) and executables (*/usr*), although personally I only have */home* and swap on HDD.

---

- **Use lighter software always**. From personal experience, I found that **wicd** is faster and lighter on resources than **NetworkManager**. **Firefox** tends to use less memory than **Chrome**. **mpv** is a simple but amazingly complete media player, usually better than **Totem** and **VLC**. Consider learning **vim** instead of an IDE or graphical editors. Also, you do not need an office suite since Google Docs is great.

If you followed the guide religiously up to here, you are ready to dig into more command line stuff. Don't be scared, I won't brick your computer.

## Finer system tuning
- **Decrease output during boot**. Your system might spit out a ton of information during boot, but really it's too much and too fast to care. Go to your bootloader configuration (Google it) and append the following to the kernel command line:

  ```
  quiet loglevel=3 splash
  ```

  It removes most of the messages and sets the log level to display only error messages. You can read the boot output later using *dmesg* and *journalctl*.

---

- **Use faster disk schedulers**. If you have a SSD, you can change the scheduler since the default one, CFQ, accounts for seek time of HDDs, which do not exist on SSD. I recommend the **deadline** scheduler, but the **noop** scheduler can be faster, especially on boot. To configure it, first create the file */etc/udev.d/60-scheduler.rules* and insert:

  ```
  # set deadline scheduler for non-rotating disks
  ACTION=="add|change", KERNEL=="sdb", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="<scheduler>"
  ```

  Replacing `sdb` with your disk (you can get its name with *lsblk*) and `<scheduler>` with your favorite scheduler (e.g. [my configuration](https://github.com/ranisalt/dotfiles/blob/master/etc/udev/rules.d/60-schedulers.rules). You can also replace the disk scheduler on boot, in which case there will be less overhead on boot times, adding the following to your kernel command line (like in the previous tip):

  ```
  elevator=<scheduler>
  ```

  [This post](https://bbs.archlinux.org/viewtopic.php?id=123427) has some benchmarks with **cfq**, **deadline** and **noop** and concludes native SATA queueing (called NCQ) probably does a slightly better job than kernel schedulers, so **noop** might have the best throughput. Replacing accordingly.

---

- **Finer tuning of _/etc/fstab_**. First of all, you can use the *noatime* option on ext filesystems to prevent updating access time of files, thus not writing to the disk every time you touch a file (although *touch* still works). You can also specify *discard* on SSD partitions to activate TRIM (Google it), and *commit=60* on SSD to sync to disk less frequently. For example, the full line for my */* partition:

  ```
  /dev/sdb3	/	ext4	discard,noatime,commit=60	0	0
  ```

  **Addendum**: [this blog post](https://patrick-nagel.net/blog/archives/337) claims that *discard* might have a negative impact. As always, your mileage may vary.

---

- **Optimize your initrd**. On Arch Linux, you can modify */etc/mkinitcpio.conf* and it is very well documented, and there's a pretty explained guide [here](http://blog.falconindy.com/articles/optmizing-bootup-with-mkinitcpio.html) (don't mess with it if you use LUKS). You can change the *COMPRESSION* to *cat* on SSD to generate a larger initrd in favor of faster (instant) decompression, a fine trade-off around 10 times faster than gzip, or you can use *lz4* compression which can compress more than 30% and has almost instant decompression ([benchmark](http://catchchallenger.first-world.info//wiki/Quick_Benchmark:_Gzip_vs_Bzip2_vs_LZMA_vs_XZ_vs_LZ4_vs_LZO)). On other distros, refer to the official guides and manuals.

---

- **Use [profile-sync-daemon](https://wiki.archlinux.org/index.php/Profile-sync-daemon)**. It is a great tool by [@graysky2](https://github.com/graysky2) to manage your browser profile on tmpfs, and it both increases performance and reduces disk wear. If supported, use it in "overlayfs" mode to minimize sync delay. To check if your system supports it, run the supplied script [testoverlay.py](testoverlay.py), or run the following manually:

  ```bash
  $ zgrep OVERLAY /proc/config.gz
  ```

  On Fedora (kernels that do not export */proc/config.gz*), you need to run the following:

  ```bash
  $ grep OVERLAY /boot/config-$(uname -r)
  ```

  And it should output either `CONFIG_OVERLAY_FS=m` or `CONFIG_OVERLAY_FS=y`, else you need to recompile your kernel. Then, edit */etc/psd.conf* and uncomment `USE_OVERLAYFS="yes"`. Reboot and check.

---

- **Replace bash by dash on boot**. This is a tricky one. **dash** is a very slim alternative to **bash** and it can be used on boot to shave off some milliseconds. You need to redirect */usr/bin/sh* to */usr/bin/dash* if it was linked to bash. Check it first:

  ```bash
  $ ls -og /usr/bin/sh
  lrwxrwxrwx 1 4 Aug 14 03:03 /usr/bin/sh -> bash
  ```

  So yes, it was linking bash. Go to */usr/bin* and change it:

  ```bash
  $ cd /usr/bin
  $ ln -s dash sh
  ```

  And you are good to go. Just remeber to update your scripts if they rely heavily on bash and are configured to use */usr/bin/sh*.

---

- **Avoid swapping (or disable at all)**. Swap is a major bottleneck. You will not want to have it on SSD since it will wear out your SSD, and use a too big space if you have a small SSD like me, but HDD is very slow and when your system starts thrashing, it'll feel like hell.

  Create a file under */etc/sysctl.d* named *99-swappiness.conf* and add the following:

  ```
  # Do less swapping
  vm.dirty_ratio = 6
  vm.dirty_background_ratio = 3
  vm.dirty_writeback_centisecs = 1500
  ```

  Those configurations are responsible for controlling how often the kernel swaps ([documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/sysctl/vm.txt)), I use them on a 6 GB system with a 8 GB swap partition and this is a good value. [Here's a good article on how swappiness works](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that), I recommend the reading.

There's more to come.

## License
[This work is under public domain](https://github.com/ranisalt/faster-computer-guide/blob/master/LICENSE).
