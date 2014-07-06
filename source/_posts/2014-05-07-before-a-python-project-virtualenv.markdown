---
layout: post
title: "Before a Python Project: virtualenv"
date: 2014-05-07 13:35:48 +0900
comments: true
categories: Python, virtualenv
---
###Introduction
`virtualenv` is a tool to create isolated Python enviroments. 

Imagine that when you have a few projects on hand simultaneously, and each project requires different Python package. Of course you can install the package i.e:Django globally on your `/usr/bin/python` but it's not recommendeded to install packages gloablly. <!-- more -->For instance, let's install Django package globally into your computer via `pip`. 

```
$ sudo pip install django
```
*[pip](https://pypi.python.org/pypi/pip) is a tool for installing and managing Python packages.*

With this package, you created a successful project. After sometime you update you package for the new Django version.
```
$ sudo pip install -U django 
```
Then another client demands for a slightly different project and you use the current package to create another awesome project. Everything seems fine on this awesome project but you'll sooon discover that your brilliant project(previous) doesn't work anymore. This is because as newer version of package is released, the API is changed simultaneously. It might be just a minor upgrade for the code, but it'll do a lot of damage. And that's when you spend your time to upgrade your code for your previous project. If you're using `virtualenv` for each of your project, you won't be affect.

###Installation
Installing virtualenv is extremely easy. 
```
$ sudo pip install virtualenv
```

###Getting Started
To create a new virtual environment,
```
$ cd /projects/
$ virtualenv ENV
```
where ENV is the name of your new created directory. Of course if your have other projects, you probably will do something like this.
```
$ virtualenv ENV_projectA
$ virtualenv ENV_projectB
```
To begin using the ENV, it had to be activated.
```
#First let's check if we are using the global python
$ which python 			
/usr/bin/python

#Now let's activate the virtual environment
$ source ENV/bin/activate 
$ which python
/home/username/projects/ENV/bin/python

```
Then it's time for you to install any modules you wish under this environment. When you're done working for the moment, you can deactivate it. Also there is no command to delete your virtual environment. Simply delete the directory using **rm** after deactivating.
```
$ deactivate
$ sudo rm -rf ENV 			# ENV gone
```
###Conclusion
The workflow of `virtualenv` is extremely easy and simple. The only module you need to install it globally is probably `virtualenv` which containing copy of **python**, **pip** and their own directory to store other libraries installed.

###Resource
+ [http://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/](http://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/)
+ [https://virtualenv.pypa.io/en/latest/virtualenv.html#usage](https://virtualenv.pypa.io/en/latest/virtualenv.html#usage)
