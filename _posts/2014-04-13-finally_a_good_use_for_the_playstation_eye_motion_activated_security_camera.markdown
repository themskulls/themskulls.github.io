---
layout: post
title: 'Finally a good use for the Playstation Eye: motion activated security camera'
date: '2014-04-13 13:47:00'
---

Recently we needed to give the flat keys to a builder so he could paint the front door of the flat. Landlord had organized it so we had no idea who was about to enter the flat and I wanted to be sure I'd know he (or they) stays in the entrance. As I didn't have an IP camera I started thinking ... 
A-ha! Playstation Move. I bought one a while back and hardly used it. I'd also want to be able to see the captured images remotely and only collect data when there's a change - storage is cheap but still limited. Dropbox would do. 

Here's what you need. 

* Playstation eye camera
* Ubuntu laptop (well, any Linux device should do. Think: Raspberry Pi)
* Dropbox (account + installed)
* ~Half an hour, including testing

Here's how to make it work.

#### 1\. Stick the Playstation Eye to an USB port of your laptop

For me the camera worked out of the box, I tested that I can get a picture out of it using Cheese: 

$ sudo apt-get install cheese 

#### 2\. Install Motion

Motion is an awesome piece of software that will analyse and capture video stream from a web cam, in this case the PS3 Eye. 

$ sudo apt-get install motion 

#### 3\. Configure Motion

$ sudo nano ~/.motion/motion.conf 

Search for target_dir (ctrl+w) and change the target_dir to your Dropbox directory. Mine for example is: 

target_dir /home/sami/Dropbox/security 

I also like to have my pictures placed neatly in directories based on the date the images were captured 

jpeg_filename %Y%m%d/camera-%t-%v-%Y%m%d%H%M%S-%q-motion 

This will get you something like: 

security/20140413/camera-1-01-20140413134840-01-motion.jpg 

#### 4\. Run and test

$ sudo motion 

... step in the front of camera and you should see images being captured. 

![](http://3.bp.blogspot.com/-SribxpT8cdU/U0qSuNk0jxI/AAAAAAAAM0c/4Pzyl6bRK5o/s1600/pseye.jpg) 
I'm watching you builder! (if you enter the flat )