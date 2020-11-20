# PinkCrab > Enqueue #

The PinkCrab Enqueue calss allows for a clean and chainable alternative for enqueuing scripts and styles in WordPress.

```php
<?php 
add_action('wp_enqueue_scripts', function(){

    Enqueue::script('My_Script')
        ->src('https://url.tld/wp-content/plugins/my_plugn/assets/js/my-script.js')
        ->deps('jquery')
        ->lastest_version()
        ->register();
});

```

todo

# USEAGE #


