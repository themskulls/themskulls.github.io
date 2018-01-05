---
layout: post
title: Building a free load balanced hosting solution on AWS - Part 2
date: '2014-06-02 20:43:00'
tags:
- aws
- hosting
---

Long overdue ... here's the part two of how to build your own balanced hosting in AWS. In  we got the basics together and you should have a running instance. Next we'll get the instance to serve something and then attach it to a load balancer. 
The whole thing should consist of 1x load balancer, 1x webserver, 2x security groups, 1x public URLs in the end. 
**1\. Install a web server** 
We'll first need to get a web server running on the host and serve simple pages as the Load Balancer needs to know the host is alive. We're going to install the  stack including Apache Web Server, PHP5 and MySQL database. 

SSH (using your .pem file) into the instance 
$ ssh -i yourpermissionskey.pem ubuntu@awsinstancename.com 

and run 
$ sudo apt-get install php5 libapache2-mod-php5 libapache2-mod-auth-mysql php5-mysql 

By default Apache should serve stuff under /var/www/, so 
$ cd /var/www 

And create a new file that will function as a health check for the Load Balancer. 
$ vi status 

Add 0 as the content of the file and save (with vi use - :wq). 
$ cat status 
0 

Check that you can see the 0 appear in your browser by going to http://yourinstance.com/status. 
Good. As mentioned, we will use this simple status page when the Load Balancer is set up. 
I also remember hunting Apache configs later on so here's a summary if you need to dig up what's going on 

Apache config is in: $ ls /etc/apache2/conf.d/ 
Restart apache with after a config change$ sudo /etc/init.d/apache2 restart 
To see the error log$ tail -f  /var/log/apache2/error.log 
To see the access log (i.e. if your instance is being hit with any requests)$ tail -f  /var/log/apache2/access.log 
Virtual host config here (if you want to serve multiple websites from the same instance):$ cat /etc/apache2/conf.d/vhost.conf**2\. Create a Load Balancer** 
Click the large blue button Create Load Balancer. 

![](http://2.bp.blogspot.com/-PaUdheVBMks/U4eL76Ub5UI/AAAAAAAAN_s/jv1RHv5mDeo/s1600/createloadbalancer.png) 
A wizard should pop up. **Fill** in with these 

* Load Balancer name: LoadBalancer. Note that this cannot contain spaces.
* Create LB Inside: leave as default
* Create an internal load balancer: do no tick
* Enable Advanced VPC configuration: do not tick
* Listener configuration:

* Load Balancer Protocol as HTTP
* Load Balancer Port: 80 
* Instance Protocol: HTTP 
* Instance Port: 80

Hit **Continue** and you should see a page Configure Health Check. 

* Ping Protocol: HTTP
* Ping Port: 80
* Ping Path: /status 

Leave the rest to the default values. 

Hit **Continue** and youshould be on the Assign Security Group page. 

We'll want to create a new security group for the Load Balancer. We'll amend the existing security group (that was assigned for the web server instance) later on to tighten up security. 

Now, select Create a new security group 
Give it a name you're willing to look at after (quick-create-1 isn't great long term, neither is my suggestion below :-) ) 

* Leave the protocol at TCP
* Port range at 80
* Source at default 0.0.0.0/0

![](http://4.bp.blogspot.com/-SQ6WRe42scs/U4zgyB92KiI/AAAAAAAAODY/v8iN_Xe-9U4/s1600/securitygroup.png) 
**Continue**. Add Instances. You should see the launched and running instance on the page. If not, go back to Part 1. 

**Select** the instance, click **Continue** and **review** the settings on the following page. If you're happy, **go**! 

...and your Load Balancer should be created, your instance should be attached to it and you should be able to type in your browser http://yourloadbalancer.com/status and see the same familiar 0 appear. 

**Nearly there.** Go back to the Security Groups under Network & Security on the left hands side. Select the Security Group you assigned to your web server instance (not the awesome-load-balancer-security-group!). Select the Inbound tab, click Edit and add HTTP, TCP, Port Range 80\. Custom IP should be your Load Balancer's security group, sg-xxxxx. 

This will only allow traffic from the Load Balancer to your instance which will greatly increase the security of your hosting solution. If you're planning to use a domain name for your web site, remember to point the DNS to the Load Balancer name, not the instance name. 

**Done**. Now you can host your web pages for free. Nice, right? 

Missing a step? Let me know in the comments please! 

**Further reading:** 

Jeff Reifman's post about how to host a Wordpress blog on AWS for minimal price: 
http://jeffreifman.com/detailed-wordpress-guide-for-aws/ 

David Jensen's post about installing Wordpress on AWS 
http://blog.david-jensen.com/install-wordpress-amazon-aws-ec2-linux-ebs/ 

Shang Liang's how to secure EC2 instances 
http://shang-liang.com/blog/secure-amazon-ec2-instances/ 

More about Cloud Security 
http://stratumsecurity.com/2012/12/03/practical-tactical-cloud-security-ec2/ 

How install LAMP stack on AWS EC2 instance 
http://www.robotmedia.net/2011/04/how-to-create-an-amazon-ec2-instance-with-apache-php-and-mysql-lamp/ 

[LAMP](http://en.wikipedia.org/wiki/LAMP_(software_bundle))