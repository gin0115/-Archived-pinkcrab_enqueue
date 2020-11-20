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
When you call using the static methods script() or style(), the current instance is returned, allowing for chaining into a single call. Rather than doing it in the more verbose methods.

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

### File Location ###

The URI to the defined js or css file can be defined here. This must be passed as a url and not the file path.

*This is the same for both styles and scripts*

```php
<?php
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->register();
```

### Version  ###

Like the underlying wp_enqueue_script() and wp_enqueue_style() function, we can define a verison number to our scripts. This can be done using the ver('1.2.2') method.
```php
<?php
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->ver('1.2.2') // Set to your current version number.
    ->register();
```
However this can be fustrating while developing, so rather than using the current timestamp as a temp version. You can use the *lastest_version()*, this grabs the last modified date from the defined script or style sheet, allowing reducing the fustrations of caching during development. While this is really handy during development, it should be changed to **->ver('1.2.2')** when used in production.
```php
<?php
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->lastest_version() 
```

### Dependencies  ###
As with all wp_enqueue_script() and wp_enqueue_style() function, required dependencies can be called. This allows for your scripts and styles to be called in order.
```php
<?php
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->dep('jquery') // Only enqueued after jQuery.
```


### Front vs wp-admin  ###
By defualt enqueue can be used for both the frontend and wp-admin (inc ajax, rest). You have control over where they called.

```php
<?php
// Dont enqueue if is_admin()
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->lastest_version() 
    ->admin(false)

// Only enqueue if ! is_admin()
Enqueue::script('my_script')
    ->src(PLUGIN_BASE_URL . 'assets/js/my-script.js')
    ->lastest_version() 
    ->front(false)
```
