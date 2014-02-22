---
layout: post
title: "WP Plugin API - Actions Hooks"
date: 2014-02-17 20:49:50 +0900
comments: true
categories: [WordPress, hooks]
---
<!-- more -->
 Hooks are triggered by events in WordPress. By action hooks, you can tell WordPress what to do at a specific points. 

From the Codex
```php Actions Hooks codex.wordpress.org/Plugin_API
<?php add_action( $hook, $function_to_add, $priority[1->10(default)], $accepted_args)?>

```

### Some Popular Action Hooks
* init - Used by plugins to initialize
* wp_head - Triggered in the <head> section of home
* wp_footer - Triggered before </body> tag
* comment_post - Triggered after a new comment
* publish_post - Triggered when a new post is created
[Complete Action Reference](codex.wordpress.org/Plugin_API/Action_reference "Codex Reference")

Let's say you want to send an email to a newly registered user. You can trigger you function to send an welcome email when new user is registered.

```php
<?php 
	add_action( 'user_register', 'send_welcome_email', );

	function send_welcome_email() {
		# check if the email address is filled up
		if ( isset ( $_POST['email'] ) )
			$email = $_POST['email'];
			$subject = 'Welcome';
			$message = 'Thank you for registering with us.';
			
			#use wp_mail function to send mail
			wp_mail ( $email, $subject, $message);
	}
?>
``` 
That's it. Hooks are probably one of the most powerful WordPress features whether in theme or plugin developement. And sometimes it took a long time to find the appropriate hook.

 

