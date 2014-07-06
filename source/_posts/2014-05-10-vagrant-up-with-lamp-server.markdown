---
layout: post
title: "Vagrant Up with LAMP Server"
date: 2014-05-10 17:13:52 +0900
comments: true
categories: Vagrant, PHP, LAMP
---
###Download and Create Project
First of all, download [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](http://www.vagrantup.com/downloads). Also do not forget the VirtualBox [Extension Pack](http://download.virtualbox.org/virtualbox/4.3.10/Oracle_VM_VirtualBox_Extension_Pack-4.3.10-93012.vbox-extpack)

After installing, create a directory for project and initialize the directory.
<!-- more -->
```
$ mkdir project
$ cd project
$ vagrant init 			# Creates Vagrantfile
```
Of course, we can follow the documentation to do `vagrant box add hashicorp/precise32` but let's conclude it into our `Vagrantfile`.
Let's create new provisioning script- `install.sh` in our project root to install apache, PHP, mysql, XDebug, Composer etc.

```
sudo apt-get update

sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'

sudo apt-get install -y vim curl python-software-properties
sudo add-apt-repository -y ppa:ondrej/php5
sudo apt-get update

sudo apt-get install -y php5 apache2 libapache2-mod-php5 php5-curl php5-gd php5-mcrypt php5-readline mysql-server-5.5 php5-mysql git-core php5-xdebug

cat << EOF | sudo tee -a /etc/php5/mods-available/xdebug.ini
xdebug.scream=1
xdebug.cli_color=1
xdebug.show_local_vars=1
EOF

sudo a2enmod rewrite

sed -i "s/error_reporting = .*/error_reporting = E_ALL/" /etc/php5/apache2/php.ini
sed -i "s/display_errors = .*/display_errors = On/" /etc/php5/apache2/php.ini
sed -i "s/disable_functions = .*/disable_functions = /" /etc/php5/cli/php.ini

sudo service apache2 restart

curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```
Next, let's edit the magic `Vagrantfile`.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provision :shell, :path => "install.sh"
  config.vm.synced_folder ".", "/var/www",
end
```
This basically talks to Vagrant like this:

- Hey, install Ubuntu Server 12.04(32 bit) for me, you can find it at the link given
- I want to access my server via `192.168.33.10`
- I want you to install something else. Please look at them at `install.sh`(which created at first)
- Sync all the files to the /var/www so I can access them on my host machine(own desktop)
###Boot into Virtual Machine
Yes, we can now
```
$ vagrant up 	# Start the server
# ...... This might takes a long time for the first time. ......
$ vagrant ssh 	# Log into server
```
Once you're in, try to play around by checking all the software installed.
```
php -v
composer
apache2 -v
mysql -u root -p 	# Both username and password are root
```
You should be seeing something like *It Works!* if you browse `192.168.33.10` via your Chrome or Firefox. We'll be able to see the *index.php* inside /var/www/html directory. Also, the directory `/vagrant` in virtual machine is synced to `/var/www` in host machine. 
###A more human like address  
Next, instead of typing `192.168.33.10` to access our page, we can set it to a url like address. For instance, `dev.local`. To do this, we need to configure 2 files. First, inside our virtual machine(after SSHed), let's open up `/etc/apache2/sites-enabled/000-default.conf`.

```
# ServerName www.example.com
# Uncomment it and change it to the URL you like

 ServerName dev.local

 ServerAdmin webmaster@localhost
 DocumentRoot /var/www/html
```
Here we changed the server name to `dev.local`. Also don't forget to reload apache.
```
sudo service apache2 reload
```
Next, use `ctrl+d` or `cmd+d` to logout to our host machine and customize the `/etc/hosts` file.
```
127.0.0.1 		localhost
...

192.168.33.10 	dev.local 	# Add this line according to your own private 
							# network ip and server name
```
Try to go to `dev.local/` in your browser. You should see Apache2 default page. 
The default document root is `/var/www/html`, so to start using our LAMP server, we can delete the default `index.php` inside the directory and create our own. Of course if you like you can alter your document root. For instance `/var/www/`.

So we had successful created our LAMP server on vagrant up. It might be a little bit painful at first but once you get comfortable with it, you can create your next project like a boss.

###Shut down the VM
Also don't forget to shut down your virtual machine when you're done.
```
$ vagrant suspend 	# super fast shutdown and start
$ vagrant up        # take some extra time to start 
$ vagrant destory   # take more time to start
```
All of these 3 commands work to shut down a virtual machine with differenct speed. Of course the one take shorter time to shut down and boot up consumes more disk space and RAM.

###Resource
+ http://serversforhackers.com/editions/2014/02/25/vagrant-apache/
+ https://gist.github.com/fideloper/7074502

<!--
Also, you can make your own virtual hosts under `/var/www` or you can create multiple projects on a virtual machine. Let's try the latter out. `vagrant ssh` into your virtual machine and add a *project.conf* to `/etc/apache2/sites-available`.
```
# We can copy the default file.
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/project.conf
``` 
Open up our *project.conf* and alter *ServerName* to `dev2.local` and *DocumentRoot* to `/var/www/html/project`. 

```
# Creat symlink in sites-enabled to project.conf in sites-available
cd /etc/apache2/sites-available/
sudo a2ensite project.conf

sudo service apache2 reload
```
Let's logout virtual machine and add some files to our newly created `project` folder.
```

```
-->

