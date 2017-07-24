---
title: "Web CMS PHP Reverse Shell"
date: 2017-07-24T16:42:46Z
draft: true
---

# Introduction
A web content management system (CMS) is a application which supports the creation and management of web pages. The most popular of the web CMSs is WordPress. The two other most popular CMSs after WordPress are Joomla and Drupal. Web CMS generally perform similar functions so attacks on WordPress CMSs will tend to generalize to other CMSs. 

One of the key features of web CMSs is that they typically support dynamic web content through the usage of PHP which is a server-side scripting language. Because the server executes PHP code to serve web pages, if an attacker can control the PHP code that the server executes, then the attacker can gain remote code execution on the web server.

# Getting a PHP Reverse Shell on WordPress
First you need to login to the WordPress admin console. You'll typically see a login page like the screen shot below.
![WordPress Login](http://learn.greyhatctf.com/attack/wp_login.png/)

After a successful login you'll see a WordPress dashboard. On the left navigation menu go to Appearance -> Editor.
![WordPress Dashboard](http://learn.greyhatctf.com/attack/wp_dashboard.png/)

From the editor click on the Theme Footer link on the right navigation menu under Templates. The footer is contained in a file called footer.php. The nice thing about the footer is that it's contained on every page at the bottom and any PHP code contained in the footer will get executed when you browse to a page with that theme. You can use other template files with PHP code but the footer.php works well for this example.
![WordPress Editor](http://learn.greyhatctf.com/attack/wp_editor.png/)

At the top of the footer.php file you'll see PHP code contained in angle brackets.
```
<?php
/**
 * The template for displaying the footer
 *
 * Contains the closing of the #content div and all content after.
 *
 * @link https://developer.wordpress.org/themes/basics/template-files/#template-partials
 *
 * @package WordPress
 * @subpackage Twenty_Seventeen
 * @since 1.0
 * @version 1.2
 */

?>
```

This is where you'll insert your PHP code which will give you a reverse shell. A simple but functional PHP reverse shell can be found here [php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php). On the reverse shell code on line 49 change the IP address to your listener IP and on line 50 change the port to your listening port.

On your listener machine which you control, start a netcat listener. Here we're using port 4444 to listen on.
```
nc -lvp 4444
```

Replace the code starting with ```<?php``` and ending with ```?>``` with the reverse shell code. then click Update File. You'll see File edited successfully at the top of the page.

Now all you have to do browse to a page on the WordPress site and your listener should catch a reverse shell from the web server.
![Reverse shell on netcat listener](http://learn.greyhatctf.com/attack/nc_php_reverse.png/).

Executing ```whoami``` shows that you are running on the shell as ```daemon```, often instead of ```daemon``` you'll the user ```www-data```.

# References
1. [Content management system - Wikipedia](https://en.wikipedia.org/wiki/Content_management_system)
2. [Usage Statistics and Market Share of Content Management Systems for Websites, July 2017](https://w3techs.com/technologies/overview/content_management/all)
3. [WordPress - Wikipedia](https://en.wikipedia.org/wiki/WordPress)