---
layout: post
title: How to set up an Quake 3 server with the OSP mod the easy way
---

# Prequestities
- A local server running with a linux distro (Ubuntu in my case)

# First steps
The basic install of the Quake 3 server can be easily accomplished via the awesome [linux GSM](https://linuxgsm.com/servers/q3server/) script. Just follow the steps there. But please create a new user for the server. You thank yourself later on if you later play around with different server files (games). The basic usage on the linux GSM site should also be self explanatory.

After you have correctly installed the server you must forward the given ports in your router settings. "insert screenshot of fritzbox with port freigaben" I used the default ports. You can find the exact ports for yourself if you open the config file "screen shot".

Lets fire up the server for a quick test:
```bash
$ ./quake3server start
```
We don't care about the individual client settings for now. Just go to multiplayer and change the server filter to local. Woala your wholesome server should be visible now. Try if you can join your server.

# Integrate the OSP mod
First download the files from the [website](https://www.orangesmoothie.org/download.html). You can either do this directly from your servers command line via "TTESTS THIS COMMAND with:
```bash
$ wget
```
or you download the zip on your client machine and transfer the zip file via scp on your server.
```bash
$ scp 
```
Now unzip the file in your `Quake3/root` directory and it is successfully installed.

Now you have to use another altered command to start the server.
```bash
$ ./
```
You can also change the start script from the default linux gsm.

# Change important server settings
# Extra: Some notes for the clients 