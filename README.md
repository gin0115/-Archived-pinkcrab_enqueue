# PinkCrab > Enqueue #

The PinkCrab Enqueue calss allows for a clean and chainable alternative for enqueuing scripts and styles in WordPress.

```php
<?php 
add_action('wp_enqueue_scripts', function(){
    
    // Enqueue a script
    Enqueue::script('My_Script')
        ->src('https://url.tld/wp-content/plugins/my_plugn/assets/js/my-script.js')
        ->deps('jquery')
        ->lastest_version()
        ->register();
    
    // Enqueue a stylesheet
    Enqueue::style('My_Stylesheet')
        ->src('https://url.tld/wp-content/plugins/my_plugn/assets/css/my-stylesheet.css')
        ->media('all and (min-width: 1200px)')
        ->lastest_version()
        ->register();
});

```
The above examples would enqueue the script and stylesheet using wp_enqueue_script() and wp_enqueue_style()

> lastest_version()

This grabs the last modified date from the defined script or style sheet, allowing reducing the fustrations of caching during development. While this is really handy during development, it should be changed to **->ver('your_version')** when used in production.

## Features ##


