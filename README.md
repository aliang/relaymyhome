relaymyhome
===========
OSX Bash Script for automating the process of getting Nintendo 3DS StreetPass hits via Internet Connection Sharing. Gathers the maximum of ten (10) StreetPass hits within a few minutes. Can be re-run many times per day if using "full" mode.

What It Does
============
By setting up your Mac computer to act like a StreetPass Relay, you can get StreetPass tags from all over the world. This script cycles through over 20 of the most popular streams in order to fill up your StreetPass queue in 20-30 minutes. Just set your 3DS down, configure your computer, and run the script.

What You'll Need
================
* A Nintendo 3DS that has **updated firmware (as of August 2013)** with WiFi turned on, all apps/games closed, and in sleep mode (lid closed).
* An Apple computer running OS X (only tested on 10.8 and up, although earlier versions may work as well) with both wired and wireless network interfaces (MacBook Airs will need a USB or Thunderbolt to Ethernet adapter for the wired connection). Your wired connection must be connected to a wired network and able to access the Internet over that connection.
* An account with administrator rights on the computer, because this script requires root access to your computer to change wifi settings.

Installation (Mac OS X 10.8)
====================================
1. Download the script file from this page. The easy way is to download the ZIP file using the "Download ZIP" button on the bottom right of this page. Double click the downloaded file to unzip it.
2. Move the **relaymyhome** file to somewhere you can access (if you're completely unfamiliar with using the OSX Terminal, stick it in **Documents**).
3. Using the WiFi icon in your menu bar at the top of the screen, select "Create Network..." and create a network named **NZ@McD1** (previously attwifi, which should also still work) and make sure to set *Security* to **None** (you can ignore the Channel option).
4. Open **System Preferences**, then select **Sharing**. Select **Internet Sharing**, then set "Share your connection from:" to **Ethernet**, and check **WiFi** in the "To computers using" box. Finally, check **Internet Sharing** and click **Start** at the prompt.
5. Open **Terminal** (in your Applications folder under *Utilities*), and navigate to the location you placed **relaymyhome** -- if you put it in **Documents**, then in *Terminal* type: **cd ~/Documents**
6. If this is the first time you are running the script, in Terminal enter the command: **chmod +x relaymyhome**

Installation (Mac OS X 10.9 & 10.10)
====================================
1. Download the script file from this page. The easy way is to download the ZIP file using the "Download ZIP" button on the bottom right of this page. Double click the downloaded file to unzip it.
2. Move the **relaymyhome** file to somewhere you can access (if you're completely unfamiliar with using the OSX Terminal, stick it in **Documents**).
3. Open **System Preferences**, then select **Sharing**. Select **Internet Sharing**, then set "Share your connection from:" to **Ethernet**, and check **WiFi** in the "To computers using" box. Click the **Wi-Fi Options** button, enter **NZ@McD1** as the Network Name, leave Channel default and ensure Security is set to **None**. Finally, check **Internet Sharing** and click **Start** at the prompt.
4. Open **Terminal** (in your Applications folder under *Utilities*), and navigate to the location you placed **relaymyhome** -- if you put it in **Documents**, then in *Terminal* type: **cd ~/Documents**
5. If this is the first time you are running the script, in Terminal enter the command: **chmod +x relaymyhome**

Basic Usage
===========
1. From the directory where the **relaymyhome** file is located in Terminal, type:
  * `sudo ./relaymyhome`: This connects to the [Nintendo World](https://docs.google.com/spreadsheet/lv?key=0AvvH5W4E2lIwdEFCUkxrM085ZGp0UkZlenp6SkJablE&f=true&noheader=true&gid=3) and [HomePass addresses](https://docs.google.com/spreadsheet/lv?key=0AvvH5W4E2lIwdEFCUkxrM085ZGp0UkZlenp6SkJablE&f=true&noheader=true&gid=0). There are 21 of them, and you can get special Miis available only via Nintendo World addresses if you set your SSID appropriately.
2. Press Enter to execute the command and you should see the script do its thing. If you get an error that stops the script, something went wrong. With 5 addresses, the script takes about 8 minutes to run, after which you should have a list full of StreetPass hits on your 3DS.
3. Once you have greeted your new visitors in the StreetPass Plaza, you can run the script again to get another batch of StreetPasses. You should be able to run the script many times before you will need to wait for the eight hour cooldown on hitting the same relay twice.

Advanced Usage
==============

For those of you more comfortable on the command line, running `./relaymyhome -h` will display some usage help. You can specify the number of addresses to use, use specific addresses for shirt color or gender, spoof specific MAC addresses, and more!

What's New
==========

**3.1.0**

* Allow randomizing the order of address spoofing so you don't have to run into the same folks over and over
* Count argument now applies to any set of addresses
* Better signal handling for INT and TERM signals (it doesn't get stuck in the handler if you send the signal repeatedly)

**3.0.2**

* Cleanup work in preparation for big refactor

**3.0.1**

* Oops, now you can use the orange shirt MAC addresses

**3.0.0**

* Accept shirt and gender parameters to cycle over the appropriate addresses
* Allow passing more than one arbitrary MAC address as arguments for spoofing
* Add verbose option, it only silences two log lines right now
* Repeat way less code when cycling through addresses
* Fix double option shifting bug

**2.2.0**

* Add -t parameter to set the amount of time to wait for connections
* Split Nintendo and HomePass relay cycling into two functions.
* Split waiting for connections into its own function

**2.1.0**

* Semantic versioning from now on.
* Check for sudo, since changing wifi settings requires it, and terminate appropriately

**2.0**

* I (Alvin) forked the original code, because it was unreliable on my Early 2009 Mac Mini running 10.9 (Mavericks)
* Big refactor, everything's a function
* Wait a lot less time, except for when the MAC address changes.
* Poll amd wait for MAC address to actually change, not just 10 seconds or whatever. This was the main cause of me never getting any StreetPasses; my hardware would receive the command to change MAC address, but it would take more than 10 seconds for the MAC address change to take effect.
* Call the InternetSharing binary directly after unloading Internet Sharing plist, which seems to be more robust. (You still need to start Internet Sharing before running the script, though.)
* Remove quick mode, in favor of...
* Implementing the -c parameter to specify number of addresses. The option was parsed before in taintedzodiac's script, just not used
* More logging that's easier to read (I should really implement verbosity, though)

**1.1**

* OSX Yosemite support
* Added the Homepass relay MAC addresses.
* Updated instructions to use NZ@McD1 network name.

**1.0**

Script has been updated for the new "six at a time" feature of StreetPass Relay. The following features have been added/change:

* OS X Mavericks support
* Each address in the cycle will now connect for 90 seconds in order to provide more time for the additional data to be sent for all six potential streetpasses. This additional time is more than offset by checking far fewer addresses (see next three points below).
* Running the script in standard mode ( **./relaymyhome** ) will now hit the five main Nintendo World addresses and the code HomePass addresses. You should be able to run this mode a few times before you run out of streetpasses. This mode also provides the opportunity to get any "special" Miis that are generally only available via the official Nintendo World addresses.
* Running the script in full mode ( **./relaymyhome full** ) will now connect to five random addresses (down from 20), taking a total of 7.5 minutes. This provides 30 potential streetpasses, and should fill your 10 slots reliably.
* Running the script in quick mode ( **./relaymyhome quick** ) will connect to two random addresses, taking a total of three (3) minutes. This should quickly fill your 10 streetpasses, but will sometimes return fewer than 10.

TODO
====
* Better exit codes when bad arguments are passed
* Better cleanup after the script is done by trapping EXIT signal as well
* Set the SSID programatically via /etc/bootpd.plist or /Library/Preferences/SystemConfiguration/com.apple.nat.plist, or whatever plist it is
* More robust InternetSharing startup
* Revert back to whatever state your wifi was in before running the script (i.e. off, on and connected to whatever SSID it was before, etc.)

Credits
=======
All credit for the original idea of duplicating StreetPass Relays goes to the many folks [listed here](https://docs.google.com/spreadsheet/lv?key=0AvvH5W4E2lIwdEFCUkxrM085ZGp0UkZlenp6SkJablE&f=true&noheader=true&gid=0). All I've done is automated the process that they discovered.

Obviously, I took [taintedzodiac's code](https://github.com/taintedzodiac/relaymyhome).

Many thanks to all who have contributed time and code to this project!

Want to Help?
=============
If you'd like to improve this script, please make the changes and submit a pull request. Thanks in advance!

(Or, just do what I did and change it on your own. Yay open source! Less work for me!)
