---
layout: post
title: Building a free load balanced hosting solution on AWS - Part 1
date: '2014-01-22 20:21:00'
tags:
- aws
- hosting
- monitoring
---

![](http://3.bp.blogspot.com/-uj5SQiBB9q4/UuAqovzBnUI/AAAAAAAAKyU/yjRYgTPdqPk/s1600/aws.png) 
The great thing about building your own hosting solution instead of renting from a provider is you'll get an idea what's goes on under the hood of a typical website. AWS is pretty good for that: you get a free taster of bigger things and can experiment and learn as you go. 

Here's how to build one for your experimental project, a blog or perhaps a beer o'clock monitor! 

Recipe 

* Email address for accessing AWS
* Phone number as registering to AWS will trigger an automated call to verify you're a real person
* Credit card as Amazon will charge you if you go over the free tier limits (which you won't do of course!)

I will keep this fairly simple and won't go into AWS auto-scaling and similar features although it's pretty easy to extent what you've built afterwards to give your site more redundancy and reliability. The instructions here are valid for Ubuntu Linux and you'll need to do some steps differently if you are looking to build for example a Windows based solution. 

### Register an AWS account

Follow the instructions on the AWS website to create your account. 

The instructions to me are pretty self explanatory and there's plenty of help available if you get stuck. Note that the account activation won't be instant: AWS will call you (at least in the UK) to verify your identity. The call is automated. 
[http://aws.amazon.com/](http://aws.amazon.com/)

### Start building!

**1\. Once you've registered, go into [AWS console](https://console.aws.amazon.com/console/home)** 

And login with your account. 

**2\. Select the region you want to host your solution** 

![](http://3.bp.blogspot.com/-zKjaAWqmJ5M/Ut7UYIjtHDI/AAAAAAAAKwc/hEQlDdGYaZA/s1600/aws_region.PNG)First step is to select whereabouts in the world the instance will be started. I use EU (Ireland) as it's the nearest AWS datacenter to my physical location and where I expect most of the traffic to come from. For redundancy, it would be better to host your stuff on multiple regions but as mentioned we'll keep this fairly simple for now. 

Pick the region from the upper right hand corner. 

**3\. Create a permissions key** 

You'll need the permissions key (.pem file) to access your instance when it's launched, thus create it before. 

![](http://3.bp.blogspot.com/-wbiUkfQWZqY/U4eSMRSxc5I/AAAAAAAAN_8/JwG679IAgM4/s1600/permissions_key.png) 

Click Key Pairs  
Click Create Key Pair. 
Give your permissions key a name and click create. 

Read more about permissions keys and cryptography at http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html 

DO NOT lose this key or give it to anyone else. Promise? 

**3\. Create an instance and a security group** 

Instance is the box/the server/the host you want your stuff to run on as explained also by AWS. 

![](http://1.bp.blogspot.com/-RMtmGdpmvVs/Ut7U7lDrfWI/AAAAAAAAKwk/9WDKVs-aTHc/s1600/create_instance.PNG) 
First, click Launch Instance which can be found under Create Instance -section and you should end up on the Amazon Machine Image selection screen: 

![](http://1.bp.blogspot.com/-ScAlEJ9IlcY/Ut7VZSnWJLI/AAAAAAAAKww/s5h2-dMyl2g/s1600/choose_instance.PNG)This is where you pick which Operating System you want to run. An AMI is basically a snapshot a bare boned OS that will run but won't have too much on it. I'm going with Linux, Ubuntu Linux. 64 bit. 

![](http://3.bp.blogspot.com/-j1fd0p8dMm0/Ut7V6UEiPcI/AAAAAAAAKxA/Nnr1Gu6vXIo/s1600/ubuntu-selection.PNG) 
Check that the Ubuntu AMI says 'Free tier eligible' as there's quite many pre-built images on the list. 

Click Select and you will end up on Select Instance Type -page. Only Micro instances are eligible for the free tier - leave it so. 

Click Review and Launch for a shortcut. 

![](http://1.bp.blogspot.com/-Nrl9My8x7PQ/Ut7YQbphJdI/AAAAAAAAKxM/0gp8Q1D2W-k/s1600/choose_instance_type.PNG) 
You should get a scary looking screen telling you to improve security. You should. 

![](http://3.bp.blogspot.com/-FsqrSR_ESgs/Ut7YjWJnGiI/AAAAAAAAKxU/JBBsVH-V5yU/s1600/review_instance.PNG) 
I'd recommend keeping the security settings pretty tight and restrict access to your instance based on your IP only for certain ports.  

Change the Source Anywhere to My IP and click add rule. This will limit access to only your IP address and the port 22 used by SSH. The downside is: if your IP changes when you for example reboot your router, you'll have login to AWS to change the I the security group settings.  

You can always add more similar rules to allow access to the box from example from your office in a similar manner. 

![](http://4.bp.blogspot.com/-3JwKK4eS-8I/Ut7iZoIGa4I/AAAAAAAAKxk/UkI54DyXLqA/s1600/security_group.PNG) 
You're now ready to launch your instance. Click Review and Launch, then Launch from the next page after you've skimmed through the settings. It'll take a couple of minutes for the instance to start and the automatic health checks to pass. 

Hello web server! 

![](http://3.bp.blogspot.com/-4SwLLmx6bdM/Ut7kgBorbcI/AAAAAAAAKxw/Api9FJDbC0U/s1600/instace_running.PNG) 
Okay, it's not a web server yet but soon will be. 

You should be able to hit your host from the [instances](https://console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:) public DNS to your browser. 
To be continued... 

* Missing a step? Let me know in the comments please.