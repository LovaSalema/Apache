<div id="top"></div>

<br />
<div align="center">

  <h3 align="center">APACHE</h3>

  <p align="center">
    An awesome README template to jumpstart your projects!
    <br />
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ul>
    <li>
        <a href="#Overview">overview</a>
    </li>
    <li>
      <a href="#Installing apache">Installing apache</a>
    </li>
    <li><a href="#Creating-Your-Own-Website">Creating Your Own Website</a></li>
    <li><a href="#Setting-up-the-VirtualHost-Configuration-File">Setting up the VirtualHost Configuration File</a></li>
    <li><a href="#Activating-VirtualHost-file">Activating VirtualHost file</a></li>
  </ul>
</details>



<!-- ABOUT THE PROJECT 


[![Product Name Screen Shot][product-screenshot]](https://example.com)-->
## Overview
Apache is an open source web server that’s available for Linux servers free of charge.

In this tutorial we’ll be going through the steps of setting up an Apache server.

### What you’ll learn
* How to set up Apache
* Some basic Apache configuration


### What you’ll need
* Ubuntu Server 16.04 LTS
* Secure Shell (SSH) access to your server
* Basic Linux command line knowledge


## Installing Apache

To install Apache, install the latest meta-package ``apache2` by running:
```sh
sudo apt update
sudo apt install apache2
```
After letting the command run, all required packages are installed and we can test it out by typing in our IP address for the web server.

<img src="apache.png" alt="apache" width="669" height="455">
If you see the page above, it means that Apache has been successfully installed on your server! Let’s move on.

<p align="right">(<a href="#top">back to top</a>)</p>


## Creating Your Own Website
By default, Apache comes with a basic site (the one that we saw in the previous step) enabled. We can modify its content in `/var/www/html` or settings by editing its Virtual Host file found in `/etc/apache2/sites-enabled/000-default.conf`.

We can modify how Apache handles incoming requests and have multiple sites running on the same server by editing its Virtual Hosts file.

Today, we’re going to leave the default Apache virtual host configuration pointing to www.`example.com` and set up our own at `gci.example.com`.

So let’s start by creating a folder for our new website in `/var/www/` by running
```sh
sudo mkdir /var/www/gci/
```

We have it named gci here but any name will work, as long as we point to it in the virtual hosts configuration file later.

Now that we have a directory created for our site, lets have an HTML file in it. Let’s go into our newly created directory and create one by typing:
```sh
cd /var/www/gci/
nano index.html
```

Paste the following code in the `index.html` file:
```sh
<html>
<head>
  <title> Ubuntu rocks! </title>
</head>
<body>
  <p> I am running this website on an Ubuntu Server server! </p>
</body>
</html>
```
Pretty cool, right?

Now let’s create a VirtualHost file so it’ll show up when we type in `gci.example.com`.
<p align="right">(<a href="#top">back to top</a>)</p>

## Setting up the VirtualHost Configuration File
We start this step by going into the configuration files directory:
```sh
cd /etc/apache2/sites-available/
```
Since Apache came with a default VirtualHost file, let’s use that as a base. (gci.conf is used here to match our subdomain name):

```sh
sudo cp 000-default.conf gci.conf
```

Now edit the configuration file:

```sh
sudo nano gci.conf
```

We should have our email in ServerAdmin so users can reach you in case Apache experiences any error:

ServerAdmin `yourname@example.com`
We also want the DocumentRoot directive to point to the directory our site files are hosted on:

DocumentRoot `/var/www/gci/`
The default file doesn’t come with a ServerName directive so we’ll have to add and define it by adding this line below the last directive:

```sh
ServerName gci.example.com
```
This ensures people reach the right site instead of the default one when they type in gci.example.com.

Now that we’re done configuring our site, let’s save and activate it in the next step!



 ### Activating VirtualHost file
After setting up our website, we need to activate the virtual hosts configuration file to enable it. We do that by running the following command in the configuration file directory:

```sh
sudo a2ensite gci.conf
```

You should see the following output

Enabling site gci.
To activate the new configuration, you need to run:
```sh
  systemctl  reload apache2
root@ubuntu-server:/etc/apache2/sites-available#
```

To load the new site, we restart Apache by typing:
```sh
systemctl  reload apache2
```
#### End result

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
