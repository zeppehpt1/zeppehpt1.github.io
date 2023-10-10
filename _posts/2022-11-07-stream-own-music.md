---
layout: post
title: Stream your own music
---

# Introduction
Spotify definitely has a lot of music on offer and offers a good selection of playlists from all genres. But there are times when you realize that your favorite track or a certain version of a song can't be found on Spotify, and then you're not happy. Or sometimes entire albums by certain artists can't be found on Spotify (I've experienced this many times with metal songs). If you've experienced this too, then look no further! 

# Prerequisteties
- Raspberry Pi 4
- Micro SD Card / USB Stick
- Storage device
- (USB to Sata cable)

# Pi installation
Visit the official website of [raspberrypi.com](https://www.raspberrypi.com/software/) and download the Raspberry Pi Imager. This is a conveniant tool to set up your Pi. Select the 64 bit headless (lite) image for the OS. Then write the image on the Pi. Don't forget to set up an initial password + username and enable ssh for the usage of the Pi because an update from April 2022 disabled the use of a default password for the headless installation.

Test if everything worked by first checking the IP of the device in your router (FritzBox etc.) if you don't use a static IP for your Pi. Then enter the following in your command line:
```bash
ssh $USER@$IP_OF_YOUR_PI
```
$User = username of the pi

$IP_OF_YOUR_PI = IP address of your Pi

Enter the password from earlier and you should now be successfully logged in.

# Set up of streaming software (Navidrome)
There are several applications available for managing your own music. Some are literally whole media libraries for playing videos and other stuff. I'dont needed that so Navidrome with its pure focus on managing large music storages (12k songs) it perfectly fitted my needes.


I went with the docker installation of [Navidrome](https://www.navidrome.org/). So I had to prepare/install docker + docker-compose. There are several tutorials on the web on how to do this. While you are in your home directory (~/), create a folder for your application with:
```bash
mkdir navidrome
sudo
```
and give the folder the right permissions:
```bash
sudo chown 1000 -R /navidrome
```

Go to the folder and create a `docker-compose.yaml`. In this file, write the default settings that will be used to create your container. The default settings can be found on the Navidrome website. Then you are safe to fire it with:
```bash
docker-compose up -d
```
Test if it works by entering the IP of your Pi with the correct port (default 4533) into your browser. You should see a login view.

You can now also change some environment variables via the `navidrome.toml` file. [Here](https://www.navidrome.org/docs/usage/configuration-options/) you can find the documentation of this configuration file.

# Set up and connect storage device
I decided to go with a 4TB hard drive that is optimized for using a Raid system. I chose such a hard drive because I want my Music Pi to run 24/7 with almost daily accesses, so I believed that the NAS hard drive would be beneficial for me. I bought a Sata-to-USB cable with an external power supply because I was afraid that the power of the Pi's USB port might not be enough.

After everything is plugged in, check to see if your Pi has found the external device:
```bash
sudo fdisk -l
```
At the bottom it usually says something like /dev/sda1 for your external device. Now we need to mount the external device so we can access it. To do this, we first need a folder where we can mount the device:
```bash
cd /mnt
mkdir -p media/music
sudo mount /dev/sda1 /mnt/media/music/
```
Switch to the music folder if you are in the /mnt folder and look at your music folders to see if it was correct.
```bash
cd media/music
ls | head
```
Note: When you restart your music Pi, you must manually remount the storage device to access it. If you want the storage device to be mounted automatically on every boot, you will need to add an entry in fstab.

# Supplementary steps

## Fstab setup

get uuid of your mounted device
```bash
lsblk -f
``` 

Add the uuid of the device to /etc/fstab with the nofail option so that booting is secured
```bash
sudo vim /etc/fstab
```
Example with the last entry being the mounted music device
```bash
proc            /proc           proc    defaults          0       0
PARTUUID=801f56e2-01  /boot           vfat    defaults          0       2
PARTUUID=801f56e2-02  /               ext4    defaults,noatime  0       1
PARTUUID=A228-6C52 /mnt/media/music exfat defualts,noatime, nofail  0 2
```

## Setup root user for easy file transfer

Perhaps you have already done that. But root access makes it easier to transfer new music files to the navidrom equipped hard drive.

in *etc/sshconfig* enable ssh over for a quick solution. Then you can use for example winSCP as a convincing tool to transfer new music files from your work computer to your music server.

# Finish

If you now take a look at your navidrome application via your browser, you should see that it has already started scanning your library. If it hasn't, you may need to restart the container by running the docker-compose command again.

And now, have fun listening to your own music wherever you are!