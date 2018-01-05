---
layout: post
title: Be the most popular guy at the office by building a Beer O'clock monitor
date: '2014-01-26 15:01:00'
---

![](http://2.bp.blogspot.com/-VAuF7Y8WxAs/Utpv-q4U0NI/AAAAAAAAKiY/wNsLc0VW448/s1600/gecko-beer.png) 
So we have a tech team Beer o'clock on Fridays, at 5pm in the breakout room. 

What we also have is bunch of monitors mounted on the walls displaying data about how the service is doing and business metrics such as number of bookings for us to be quickly able to react if anything flashes red and goes below a certain threshold. We use [Geckoboard](http://www.geckoboard.com/) 

Geckoboard is pretty flexible on what you can feed to it. What I ended up doing is writing a few lines of PHP to produce a JSON endpoint for Geckoboard to read.  

It look like this: 

<pre style="white-space: pre-wrap; word-wrap: break-word;">{"item":[{"text":"6 days 4 hours 48 minutes","type":"0"}]}</pre>

You'll need to host  somewhere. Take a look at my previous posts on [how to build a free simple hosting solution on AWS](http://www.samituohino.com/2014/01/building-your-own-load-balanced-free.html) 
In Geckoboard on the dashboard you want the widget to reside in select Add a widget -> Custom Widget -> Text.  
![](http://1.bp.blogspot.com/-GfNeAsIGpVs/Utp38qD9ivI/AAAAAAAAKio/dNlynxuWvwU/s1600/text_widget.png) 
Fill in the Label, Widget size (I found 2x1 the best for this purpose) and the URL where you host your oclock.php. 

![](http://4.bp.blogspot.com/-yYEDQdSZuU0/Utp5smMMnOI/AAAAAAAAKi0/135lZ3h3Jbo/s1600/gecko-beer-details1.png) 
Check that the Data Feed format is JSON, choose GET and how often you want Beer O'Clock to update. 
![](http://3.bp.blogspot.com/-K_UvdP9FmpM/Utp6Vfodi_I/AAAAAAAAKjE/l93LsvM5eJk/s1600/Screenshot+from+2014-01-18+12:21:31.png) 

<pre style="white-space: pre-wrap; word-wrap: break-word;">You can download the Gecko-beer code snippet from [GitHub](https://github.com/samituohino/gecko-beer) </pre>

* I lied. This won't make you the most popular guy at the office. It is entertaining though.