# Installing Symphony on MAMP and MAMP Pro

Also, if you're using MAMP, you're in for an easy ride setting up Symphony, and a slightly more advanced easy ride on MAMP Pro.

There are differing opinions on whether MAMP is a better route to take over the shipped Apache/MySQL setup on Mac, but it is my setup of chioce as it saves headaches. That is my opinion though, but it seems it's yours too, so we have something in common! Yay!

So, to begin with it's advisable to switch off the apache setup that shipped with your Mac. You can do this under the System Preferences > Sharing panel, just de-select Web Sharing if it is selected.

With MAMP and MAMP Pro, you have two options available in the way of ports. You can use the MAMP ports (8888 and 8889), or you can set your server to use default ports (80 and 3306). These tutorials will assume the default port option.

## MAMP

Setting up on MAMP couldn't be simpler. All you have to do is follow these few steps.

0.	Create a utf-8 MySQL database using phpMyAdmin that has been installed with MAMP, taking note of the database name, username and password too.

0.	Unzip the Symphony download and move the contents of the unzipped folder to `/Applications/MAMP/httpdocs`

0.	In your browser, go to `http://localhost/`

This will begin the installer, so just follow all the steps, and Symphony will do all the hard work for you!

Once you've done this, you will be able to access your site at http://localhost/ and the admin at http://localhost/symphony/