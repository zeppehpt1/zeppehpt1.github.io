---
layout: post
title: How to easily set up a Quake 3 server with the OSP mod
---

# Prequestities
- A local server running with a linux distro (Ubuntu in my case)
- A Quake 3 copy

# First steps
The basic install of the Quake 3 server can be easily accomplished via the awesome [linux GSM](https://linuxgsm.com/servers/q3server/) script. Just follow the steps there. But please create a new user for the server. You thank yourself later on if you later play around with different server files (games). The basic usage on the linux GSM site should also be self explanatory.

After you have installed the server correctly, you need to forward the specified ports in the settings of your router. I used the default ports.

Lets fire up the server for a quick test.
```bash
$ ./quake3server start
```
We don't care about the individual client settings for now. Just go to multiplayer and change the server filter to local. Woala your wholesome server should be visible now. Try if you can join your server.

# Integrate the OSP mod
First download the files from the [website](https://www.orangesmoothie.org/download.html). You can either do this directly from the command line of your server with.
```bash
$ wget http://osp.dget.cc/orangesmoothie/downloads/osp-Quake3-1.03a_full.zip
```
or you download the zip file on your client machine and transfer the zip file to your server via scp.
```bash
$ scp file IP@hostname:/path/
```
Now extract the file to your `Quake3/root` directory and it is successfully installed.

Now you have to use another modified command to start the server.
```bash
$ quake3 +set dedicated 2 +set com_hunkmegs 32 +set fs_game osp +exec.cfg
```
You can also change the startup script from the default Linux gsm to start the server in a simple way.

On a final note, this is a very basic setup, you can now change the server settings to your liking. Play around with them and gather some friends and you will have a great time. I recommend playing instagib railgun.