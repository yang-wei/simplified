## Simplified - Simple Octopress Theme

Simplified is a clean, single column theme for Octopress with a cool landing page.

This theme has a live preview [here](http://yangweilim.com).


### Install
```php
cd octopress
git clone https://github.com/yangweilim/simplified.git .themes/simplified
rake install['simplified']
rake generate
```

### Customization
You can change the theme color easily by changing `$theme-color` at your `octopress/sass/base/_theme.scss`. <br>

For the landing page image, simply rename your favorite image as `header.jpg` and replace it at your `octopress\source\images`. <br>

The social icon at landing page can be removed or added by editing `octopress/source/post/social_icon.html`. <br>

This theme used [Font Awesome](http://fortawesome.github.io/Font-Awesome/icons/) icons, so you can add any icon as you like. 

### License
This theme is licensed under a MIT License - http://opensource.org/licenses/mit-license.html

Feel free to use.
