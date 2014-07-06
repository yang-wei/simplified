---
layout: post
title: "NPM Installation Issues + AngularJS set up"
date: 2014-06-01 19:50:53 +0900
comments: true
categories: Set Up, AngularJS, NPM 
keywords: NPM sudo issues
---
Package manager is tool for software developer to install,
publish and manage dependecies.
Just like other widely used programming languages, nodejs
has its own package manager - `npm`.
In this blog, I'm going to set up *AngularJS* develoment environment with

<!-- more -->
 + Yeoman
 + Grunt
 + Bower

But before that I have to set up `npm` on my machine.
Setting up `npm` can be as easy as grabbing package from
[nodejs](nodejs.org/download/). However there are other ways to install.
For instance, [command line](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager)
or other package managers. After npm is successfully installed,
we can check it.
```
node -v
npm -v
```
Yes, `npm` is included in the latest node package.
Next, we want to install Yeoman, Grunt and Bower
by using npm. But before that, I need to alter permission
of some files on my system to prevent the infamous
*Please try running this command again as root/Administrator* error.

Of course I can avoid this error by using `sudo npm install package`
but this is [not the recommended way](http://foohack.com/2010/08/intro-to-npm/).
Instead, I'll just use `chown` to change permission of `/usr/local` files.
```
sudo chown -R $USER /usr/local
```
By this way some error will be eliminated *BUT* this might not be enough.
In some case, there will be other permission issue of other directory.
This is the error I get when I first install npm.
```
npm ERR! Error: EACCES, open '/Users/username/.npm/-/all/.cache.json'
npm ERR!  { [Error: EACCES, open '/Users/username/.npm/-/all/.cache.json']
npm ERR!   errno: 3,
npm ERR!   code: 'EACCES',
npm ERR!   path: '/Users/username/.npm/-/all/.cache.json' }
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

```
Yes, I do not have ownership permission on my `/.npm/` folder which
is located in my home directory. Here is a solution from [stack overflow](http://stackoverflow.com/a/16151707).
```
sudo chown -R `whoami` ~/.npm
```
In this case system will automatically substitude username into the whomi.
Also the `~` indicates home directory path.
After this we should be fine to set up Angular JS environment.
I'll install *Yeoman*, *Grunt* and *Bower* globally by this command.
```
npm install -g yo grunt-cli bower
```
Ok let's get Angular JS set up. This can be done easily by using *Yeoman*.
```
npm install -g generator-angular
mkdir angularapp
cd angularapp
yo angular
```
This will create a new folder `angularapp` and scaffold a new AngularJS
application in current folder.
Ok, done for environment. We can start to *ng* right now.

####Other issues
To use grunt as server, we also have to install the latest
version of Grunt in project folder, and add it to devDependencies.
```
npm install grunt --save-dev
```
Also we need to do the same thing to enable karma.
```
npm install grunt-karma --save-dev
npm install karma-jasmine --save-dev
npm install karma-chrome-launcher --save-dev
```
Note that `jasmine` is my testing framework and I am
using `chrome` browser.


####Resources
 + https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
 + http://foohack.com/2010/08/intro-to-npm/
 + http://www.thinkster.io/angularjs/eqq96ECqkT/1-getting-your-project-set-up-with-yeoman
