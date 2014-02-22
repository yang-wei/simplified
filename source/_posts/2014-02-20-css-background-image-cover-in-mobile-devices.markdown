---
layout: post
title: "CSS Background Image Cover in Mobile Devices"
date: 2014-02-20 23:18:32 +0900
comments: true
categories: 
---

One of the problem when I was creating this blog (2014 February) is the background image on my home page does not work well in my Android device. I expected that doesn't work well on iOS devices too.

CSS I used at first from [CSS-Tricks](http://css-tricks.com/perfect-full-page-background-image/)
``` css
	html {
    background: image-url('../images/header.jpg') no-repeat center center fixed;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
}
```
This worked well for my browser(Firefox, Chrome, Safari) on desktop. It seems perfect too when I try to resize the browser. 

But this failed. 

So here is the solution for this. We set the height of the image to 100%.
``` css
	html {
        background: image-url('../images/header.jpg') no-repeat center center fixed;
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
        height: 100%;
    }

    body {
        height: 100%;
        overflow: scroll;
        -webkit-overflow-scrolling: touch;
    }
```

This solved my problem ! Credited to [Johan](http://johanbrook.com/browsers/native-momentum-scrolling-ios-5/ "Johan Brook"). 

