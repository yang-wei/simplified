---
layout: post
title: "Local SVN Repository Workflow"
date: 2014-05-11 14:11:39 +0900
comments: true
categories: SVN
---
This tutorial will outline the simple workflow to create a SVN local repository. Of course you can get a free online repository from website like [assembla](https://www.assembla.com/home). However for simplicity and first time, I will just create a repository on local machine.
<!-- more -->
###Installing
If you do not have *SVN* installed on your machine, you can go and grab it [here](https://subversion.apache.org/packages.html) according to your OS. 
```
# for Ubuntu/Debian user
$ apt-get install subversion
$ apt-get install libapache2-svn
```
###Create repository
Let's start by creating a new repository. (Substitude user with your username or you can use ~/ to replace /home/user/)
```
$ mkdir /home/user/repo 					# Creates a directory 'repo'
$ cd /home/user/repo
$ svnadmin create alpha_project			# Creates a repository 'alpha_project'
```
The `svnadmin` program is the repository administrator's best friend. In this case, we used it to create a new Subversion repository, but this program can also be used to preform several maintenance operations. 
###Import project
The new created `alpha_project` repository is empty. So let's import some project into it. Let's say we had some project in our `/home/user/code` directory.
```
$ svn import /home/user/code` file:///home/user/repo/alpha_project/trunk -m "Init alpha_project"
...
Committed revision 1.
```
This command import our project in `/home/user/code` into the repository. Notice that we store our data in another folder `trunk` by following SVN repository layout convention. 
{% blockquote  %}
Most projects have a recognizable "main line", or trunk, of development; some branches, which are divergent copies of development lines; and some tags, which are named, stable snapshots of a particular line of development.
{% endblockquote %}

And normally here is what it looks like in a SVN single project.
```
$ svn list file:///home/user/repo/alpha_project
trunk/
branches/
tags/
```
This tutorial won't talk much about tags and branches (It's ok to not create these 2 files). And for the message inside double quotations after -m is called commit. Commit is a message to record who and when created the change and who committed it. You can think of it as a message to describe the changes.
###Checkout
Now we have our project in the repository, but we are not going to do our work there. Instead, we create another directory by checkout from it, and work on this directory. 
```
$ svn checkout file:///home/user/repo/alpha_project/trunk /home/user/alpha_project_copy
...
Checkout revision 1.
```
This duplicate a working copy of the repository into `alpha_project_copy` directory. We'll do our work here. After we've done our work, we will commit these changes back to the repository.
```
$ svn commit -m "Fixed bugs in footer"
...
...
Committed revision 2.
```
Always commit your message with short and meaningful description. Let's say if we have another collaborator who is doing this project together. She made some changes to the project and commit it to the repository. For instance, in this case a revision 3 is committed but our working copy remains revision 2. To update our working copy to the latest changes,
```
$ svn update
``` 
I concluded the basic workflow of SVN in this tutorial. There are still a lot SVN can do. 

###Resource
+ http://svnbook.red-bean.com/
+ http://www.guyrutenberg.com/2007/10/29/creating-local-svn-repository-home-repository/