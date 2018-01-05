---
layout: post
title: How to point a Hover domain to a Blogger blog
date: '2014-01-23 19:50:00'
---

![](http://2.bp.blogspot.com/-ljhoJBOWwiI/UuFhthgjfqI/AAAAAAAAKzY/AFmmDA1lPF0/s1600/hover_blogger.png) 
I've found Hover a good for registering domains. It's fairly inexpensive, easy to use and customer services seem to be quick and resolve issues fast (at least the one time I had to modify details I input in accident ... ). 

I could not find many _clear_ instructions, however, how to tie a blog on Blogger to a Hover domain. It's not tricky but there seems to be slight variation in the terms found in various places which might confuse you in the process. 

Here's a step by step. 

Recipe 

* A Hover login, and a purchased domain so you can change the necessary records
* A Blogger blog (d'oh)

### 1\. Get DNS settings

In Blogger, go to Settings -> Basic. Click '_Add custom domain_'. 
![](http://1.bp.blogspot.com/-ObhP1uQlRs0/UuFghbwkv3I/AAAAAAAAKzQ/6icgVzTh2w4/s1600/add_custom_domain.png) 
Click _Advanced settings_ and type in your domain (with www) name. Click _save_ and ... 
![](http://1.bp.blogspot.com/-ICRSn2q9HMs/UuFi3BRF72I/AAAAAAAAKzg/fhXacqk3M_c/s1600/blogger_domain.png) 
Oh. I see. Google has checked if you own the domain and doesn't know any better. Let's fix that. 

### 2\. Point your domain to your blog

We'll need to refer to the values under 

* Name, Label or Host field
* and Destination, Target or Points to field

So open a new tab and login to your Hover account. 

Click the domain name you want to point to Blogger and select the DNS tab on the next page. 

![](http://3.bp.blogspot.com/-494LVzjDKmw/UuFlbZWPsTI/AAAAAAAAKzo/7pdda-XjrVs/s1600/hover_dns.png) 

Click the + Add New button, select **www** as the **hostname** and **CNAME** as the **record type**. **Target Host** should be the **Name, Label or Host field** given by Blogger. Save. 

Click the + Add New button again and add a second CNAME similarly. Save. 

![](http://2.bp.blogspot.com/-OIewaWXadtM/UuFo7gATOXI/AAAAAAAAKzw/zVi2dQ2pO3U/s1600/hover_settings.png) 
It will take a while for the settings to take place. 

### 3\. Test settings

Go back to your blog settings and check that your domain name is displayed without errors. Here's what mine looks like as an example: 
![](http://2.bp.blogspot.com/-ir9Zpu3spBo/UuFrq6Pr0WI/AAAAAAAAKz4/nFgprnzbjoM/s1600/samituohino_blogger.png) 
You should now be able to point your browser directly to your domain and still end up in your blog. 

* Missing a step? Let me know in the comments please.