# WP Requirements
Simple drop-in library for WordPress plugins and themes to check for core, plugin, theme and php requirements.

## Installation
``` bash
composer require pressmodo/wp-requirements
```

## Basic usage
In the plugin main file:

```php
<?php
/*
Plugin Name: My Test Plugin
Version: 1.0.0
*/

// Composer autoload.
require_once __DIR__ . '/vendor/autoload.php' ;

$requirements = new \Pressmodo\Requirements\Requirements( 'My Test Plugin', array(
	'php'                => '7.0',
	'php_extensions'     => array( 'soap' ),
	'wp'                 => '5.3',
	'plugins'            => array(
		array( 'file' => 'akismet/akismet.php', 'name' => 'Akismet', 'version' => '3.0' ),
		array( 'file' => 'hello-dolly/hello.php', 'name' => 'Hello Dolly', 'version' => '1.5' )
	),
	'theme'              => array(
		'slug' => 'twentysixteen',
		'name' => 'Twenty Sixteen'
	),
) );

/**
 * Run all the checks and check if requirements has been satisfied.
 * If not - display the admin notice and exit from the file.
 */
if ( ! $requirements->satisfied() ) {
	$requirements->print_notice();
	return;
}

// ... plugin runtime.
```
