# Firefly FD Logger Jumpstart
This project is an installation wrapper for [Firefly Field Day Logger](https://github.com/jxmx/ffdl) to be run
on a Raspberry Pi using the Raspberry OS (Raspian) for a turnkey installation of FFDL. This installaion
is only to be used on a "clean" Raspberry OS installation that has no other webserver or database installed.
This installer will assume the Pi is dedicated to the logger and act accordingly.

## Raspberry Pi 
The first step is to install RaspberryOS 11 (Raspian 11) on the Pi. As there are many excellent
online directions on how to do it, they will not be repeated here.

### Rasberry Pi OS with GUI
If you like to use graphical interfaces, one good video on a full install of Raspberry OS can
be found [on YouTube](https://www.youtube.com/watch?v=jRKgEXiMtns). However if you follow
these directions, stop at 17m 30s after the install of VNC is complete. Finishing this tutorial will
install a conflicting setup for the webserver that will break this script. Installing Rasperry Pi OS
in this manner will require a monitor, USB keyboard, and USB mouse. None of these are necessary to
operate the Pi long-term when it's operating correctly.

After installing the operating system, enable the SSH service from a terminal window:

```
sudo systemctl enable ssh
sudo systemctl restart ssh
```

Now jump down to the Installing Firefly section of this document.

### Raspberry Pi OS Minimalist
If you are a bit more adept at Linux, I suggest doing a "headless" minimal
installation using the following general steps:

1. Download and write RaspberryPi OS 11 using the [Raspberry Pi imager](https://www.raspberrypi.com/software/).
For burning the image choose *Raspberry Pi OS (other)* then *Raspberry Pi OS Lite*. This will install the basic
operating system quickly.

2. After imaging the SD card but before removing it from the imaging computer, open the boot drive from
My Computer (assuming a Windows OS) and create an empty file named `ssh`. Then create a file named `wpa_supplicant.conf`
with the correct contents of your wireless network both at home and the one for Field Day. If you're only using 
wired ethernet at both, you do not need to create `wpa_supplicant.conf`. [This link](https://www.raspberrypi-spy.co.uk/2017/04/manually-setting-up-pi-wifi-using-wpa_supplicant-conf/) provides a good overview on creating `wpa_supplicant.conf`.

3. Eject the SD card properly from your Windows computer, install it in the Raspberry Pi, and plug the Pi in.

4. Once booted, SSH as the *pi* user with the password *raspberry* to the Raspberry Pi device.

## Installing Firefly
Use the following install Firefly.

1. From a terminal window in the GUI or using SSH, depending on your preferred method, become root by issuing the command `sudo -s`.

2. Set the hostname of the Pi to be something memorable and useful. The suggestion is "firefly" but the name isn't important
other than you like it and you remember it. This setup guide uses the name firefly for the Pi. Set 
the name using the `hostnamectl` command in the following manner:

```
hostnamectl set-hostname firefly
```

3. From the /root directory, download the installation script from this Git repository:

```
wget https://raw.githubusercontent.com/jxmx/ffdl-jumpstart/main/firefly-jumpstart
```

4. Execute the installer from the root terminal:

```
bash /root/firefly-jumpstart
```

The installer does not hide any information. It doesn't take a long time to run so watch for any errors. For a clean
Raspberry Pi with Internet access, you should have no problems.

5. Reboot the Pi

```
reboot
```

6. After the Pi has been rebooted you should be able to connect to https://firefly on your local network or the IP address
of the Pi you assign if your computer doesn't support dynamic DNS.
