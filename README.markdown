# GravatarLib

GravatarLib is a small library intended to provide easy integration of gravatar-provided avatars.

**Copyright**: *(c) 2011 -- Damian Bushong*

**License**: *MIT License* - please see the provided file located in /LICENSE for the full license text

## Requirements

* PHP 5.3.0 or newer
* hash() function must be available, along with the md5 algorithm

## Usage

``` php
	<?php
	include __DIR__ . '/includes/Codebite/GravatarLib/Gravatar.php';
    $gravatar = new \Codebite\GravatarLib\Gravatar();
	// example: setting default image and maximum size
	$gravatar->setDefaultImage('mm')
		->setAvatarSize(150);
	// example: setting maximum allowed avatar rating
	$gravatar->setMaxRating('pg');
```

## Twig integration

It's extremely easy to hook this library up as a template asset.

When you've got an instance of the Twig_Environment instantiated, add in your instantiated gravatar object as a twig "global" like so:

``` php
	<?php
	// include the lib file here, or use an autoloader if you wish
	include __DIR__ . '/includes/Codebite/GravatarLib/Gravatar.php';
	// instantiate the gravatar library object
    $gravatar = new \Codebite\GravatarLib\Gravatar();

	// ... do whatever you want with your settings here

	// here, we will assume $twig is an already-created instance of Twig_Environment
	$twig->addGlobal('gravatar', $gravatar);
```

Now in your twig templates, you can get a user's gravatar with something like this snip of code:

(note: this template snip assumes that the "email" template variable contains the email of the user to grab the gravatar for)

```
	<img src="User avatar" src="{{ gravatar.get(email)|raw }}" />
```

We are also using the raw filter here to preserve XHTML 1.0 Strict compliance; the generated gravatar URL contains the `&amp;` character, and if the filter was not used it would be double-escaped.
