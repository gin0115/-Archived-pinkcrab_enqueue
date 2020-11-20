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


## Features ##

### Instantiation of \PinkCrab\Enqueue::class ###

You have 2 options when creating an instance of the Enqueue object.

```php
<?php

$enqueue_script = new Enqueue( 'my_script', 'script');
$enqueue_style = new Enqueue( 'my_style', 'style');

// OR 

$enqueue_script = Enqueue::script('my_script');
$enqueue_style = Enqueue::style('my_style');

```
When you call using the static methods script() or style(), the current instance is returned, allowing for chaining into a single call.

```php
<?php

$enqueue_script = new Enqueue( 'my_script', 'script');
$enqueue_script->src('.....');
$enqueue_script->register();

// OR 

Enqueue::script('my_script')
    ->src('.....')
    ->register();
```


> lastest_version()

This grabs the last modified date from the defined script or style sheet, allowing reducing the fustrations of caching during development. While this is really handy during development, it should be changed to **->ver('your_version')** when used in production.