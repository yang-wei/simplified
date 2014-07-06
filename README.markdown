## Simplified - Simple Octopress Theme

Simplified is a clean, single column theme for Octopress which is heavily inspired by [Jest](http://facebook.github.io/jest/).

This theme has a live preview [here](http://yangweilim.com).


### Install
```
cd octopress
git clone https://github.com/yang-wei/simplified.git .themes/simplified
rake install['simplified']
rake generate
```

### Customization
You can change the theme color easily by changing `$theme-color` at your `octopress/sass/base/_theme.scss`. <br>
 <br>

The social icon at landing page can be removed or added by editing `octopress/source/post/social_icon.html`. <br>

This theme used [Font Awesome](http://fortawesome.github.io/Font-Awesome/icons/) icons, so you can add any icon as you like. 

This theme also disable Octopress default sidebar and footer. So to get this to work you have to customuze your `_config.yml` .
```
sidebar: collapse

default_asides: [asides/recent_posts.html, ... , asides/footer_in_sidebar.html]
```


### License
This theme is licensed under a MIT License - http://opensource.org/licenses/mit-license.html

### Update
Updated with a cleaner interface(24 May 2014). Below are the main updates.
 + Replace landing page with blog page
 + Minimal search form

### More to come
More features will be updated.
 * Github like syntax highlight

Feel free to use.
