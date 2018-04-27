---
layout: post
title: Housekeeping - organised chaos is better than chaos
date: '2018-04-28 22:00:21'
tags:
- music
- album
- record
- housekeeping
---

Contents
* Naming convention
* Directory structure
* Backups


### Naming convention
It's a good idea to decide a naming convention from the start as otherwise you will spend your time trying to find stuff rather than being able to focus on what matters: writing new stuff.

### Directory structure

For the same reason, getting organised on how and where you are going to store everything is extremely important.

### Backing up

Please do this. I've heard horror stories where a whole recordful of guitars had been recorded and an attempt was made to move them from a PC to an external hard drive to take for further works with the band. Except that the person doing the transfer did ctrl+x instead of ctrl+c followed by a dead hard drive in the process. Data loss. You want to avoid your hard work going to waste.


#### Automating back ups

I use Google Drive which is relatively inexpensive way of backing up your data outside your home. Insurance companies  rarely value these kinds of things so should my flat catch fire and burn - at least my music is safe wehey \o/. I've only got a NAS storage ticking away in an utility cupboard preserving the state of my Macbook which is handy if something goes wrong and I want to go back in time to recover.

#### Version controlling your music

I work in software engineering and follow the golden rule of "if it's not in version control, it doesn't exist.". I, therefore, commit all my songs to Git and push to Google Drive for the said offsite back up.

If you're not familiar with Git there is a bit of a learning curve but luckily also lots of material available to learn from. In a nutshell Git is the worlds most popular version control tool. I use the command line out but there are several Graphical User Interfaces too. It works with Mac, Windows and Linux so you've got options whichever platform you are on. <insert GitHub interactive guide here>. Purists will say I'm using Git wrong and you should not commit binaries and large files such as audio to Git. Haters gonna hate. I don't really care as this works great! Cheap, reliable, simple way of protecting my music - what more can I ask? Show me a better way and I will considering it.

To make version controlling a new song easy, I wrote a small script to help.

<./init-tune.sh song_name> will create an empty Git repository locally and push it to your Google Drive automatically if configured correctly. Configuring can be done by opening the script the changing a couple of paths. Make sure you've got Google Drive set up before thou as otherwise you'll have the version control tightly only on your machine (which doesn't help in the events of a disaster).
