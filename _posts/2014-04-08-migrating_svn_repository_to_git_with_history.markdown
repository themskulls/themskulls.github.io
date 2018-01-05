---
layout: post
title: Migrating SVN repository to Git with history
date: '2014-04-08 21:41:00'
tags:
- git
- svn
- version_control
---

Right-o. 

Today we're going to be migrating a repository from SVN to Git. 

We will only migrate one branch, trunk, because to me it doesn't make sense to keep all the obsolete branches that are just lying around confusing people. Surely, trunk has everything you need to keep ... right? 

#### 1\. Create users.txt

You can consider this step optional however I like to keep my repo tidy and track back who committed the piece of code later on without having to wonder obscure user names. 

What I'd recommend doing is generating the users.txt automatically, punch this command in Git Bash on high enough level in your SVN repository so you'll cover all developers who've worked on the code 

```
svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u >> users.txt
```

#### 2\. Fix users.txt

Again, skip if you decided to skip step number 1 for some reason. The generated file will most likely be wrong and look like 

s.tuohino = s.tuohino (s.tuohino) 

Change the names as suitable 

s.tuohino = Sami Tuohino (sami.tuohino@....com) 

Let me know if you figure out an automated way of doing this as it's a little bit of a pain! 

#### 3\. Clone your SVN repository 
```
$ git svn clone -A users.txt <svn-repository>
```
#### 4\. Create .gitignore

Grab the template for the language you're using from here 

https://github.com/github/gitignore 

For example Visual Studio solutions, use this 
https://github.com/github/gitignore/blob/master/VisualStudio.gitignore 

#### 5\. Push your repository to Git

```
$ git remote add origin <git-repository> 
$ git push origin master 
```

#### 6\. Lock the SVN repository to avoid confusion

SSH to your SVN host and...

```
$ cd /repositories/REPOSITORY/hooks
$ vi pre-commit
```
```
#!/bin/sh
echo "This component has been migrated to Git." 1>&2
exit 1
```

Save and you're done.

Voilà.