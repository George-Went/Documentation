
# Setting up vagrant 
ubuntu/trusty64 Vagrant box


# Vagrant 
Vagrant allows for virtualization of linux system within a computer, allowing for projects to work within their own containerized environment (basically it means that you know what dependencies are installed onto a system) 

## Installation 
Download the vagrant packages:   
```npm apt-get install vagrant```

Move them to the correct location + unzip files 


Extra: Add vagrant to the PATH:  
```Export PATH=$PATH:/opt/vagrant``` (in my case)

This means that you can use the “vagrant” cmd anywhere on your linux system
To add the program permanently (on ubuntu), add the path to ```/etc/environment ```

> add :/opt/vagrant to the end of path (inside the quotation marks)

## Install a virtualization software
In this case we will install the commmonly used virtualbox

```Sudo apt-get install virtualbox ```

## Setting up a vagrant vm
Make sure to make a directory and use ```cd ~/vagrantProject``` to be inside the directory you want the vagrant box to be located in.

You can pull pre existing repos of common operating systems with no dependencies installed as vagrant boxes 

```Vagrant init hashicorp/precise64```   
Or for a more updated ubuntu build, use 
```Vagrant init ubuntu/trusty64```

This will place a vagrantfile in your directory

Connect to the box using:   
```Vagrant up```  - boots up the vm (you have to be in the directory storing the vm)  
```Vagrant ssh``` - ssh’s you into the vm

The location with the Vagrantfile in is copied across to the VM
Any files stored in the directory with Vagrantfile will also appear (sync) in the VM under /vagrant

Install the software you want to use 
Run    do-release-upgrade to upgrade the version of the vagrant box (setup) that you are using
If installing pip (because pip --version == 1.0)
  curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py


phpMyAdmin login screen
We can also use the VM as a seperate system so we can test connections as if there were two seperate computers, this is great for testing database and server connections, as well as hosting both on seperate VM's then attempting to connect to your system using you main OS - just like a normal user would in real life. 

## synced folders 

By default, vagrant uses 


## Shuting Down a Vagrant Machine
To suspend a machine (save current state and stop it): 














## Setting up LAMP Stack
L - linux
A - apache
M - mySQL
P - php 

>**Note:** Most of what is below can be found at: 
https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04

## Setting up Apache
you can install apache on ubuntus package manager, ```apt```:  
```sudo apt-get install apache2```

### Adjusting firewall 
we should check / adjust the firewall to allow incoming traffic from other computers.
```sudo ufw app list```

with this command we should get the following results
```
Output
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH

```

If we look at the ```Apache Full``` we get:
```
Output
Profile: Apache Full
Title: Web Server (HTTP,HTTPS)
Description: Apache v2 is the next generation of the omnipresent Apache web
server.

Ports:
  80,443/tcp
```

we can allowin incoming http and https using 
```sudo ufw allow in "Apache Full"```

### Accessing the server through a browser 
On a browser we can access our apache server using:
```http://your_server_ip```

>**Note:** if your accessing the server on the same computer you set the server up on, you can access it by going to:
```http://localhost:80``` with the ```80``` standing for the port number we set up earlier.

### Starting / Stopping the server 
On debian / ubuntu applications we can use: 
```
## Start command ##
systemctl start apache2.service
## Stop command ##
systemctl stop apache2.service
## Restart command ##
systemctl restart apache2.service
```
On Centos/RHEL : 
```
## Start command ##
systemctl start httpd.service
## Stop command ##
systemctl stop httpd.service
## Restart command ##
systemctl restart httpd.service
```





## 2 Installing MySQL 
We can install MySQL using:  
```sudo apt-get install mysql-server```

we can set up security for the system by running:
```sudo mysql_secure_installation``` 
THis asks if you want to secure a password, y for yes or press any other key for no 

The script the asks you to set up a root account - this is the admin account for the mysql database 

**MySQL is now installed**

We can run MySQL using:  
```sudo mysql```

You can run MySQL commands, or exit using:
```exit```






## 3 Installing PHP 
PHP allows us to display dynamic content with data from a database such as MySQL 

We can install php using - with some pacakges that help us use MySQL:  
```
sudo apt install php libapache2-mod-php php-mysql
```

In most cases we will need to modify the type of file that the apache system looks for. Currently if a user requests a directory from the server, apache will first look for ```index.html```. We can modify this so that it prefers PHP files over others so that it looks for ```index.php```

We can use the text editor nano: 
```sudo nano /etc/apache2/mods-enabled/dir.conf```

We need to turn 
```
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
``` 
Into 
```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
we can then restart apache by using:  
```sudo systemctl restart apache2```

we can also check on the state of apache by using: 
```sudo systemctl status apache2```

Apache should now be serving your domain name. You can test this by navigating to http://your_domain, where you should see something like this:













## 4 Setting up Virtual Hosts
When using apache, you can set up different *virtual* hosts to save different states of configuration.

On ubuntu 18.04, apache has one set up by default to serve documents from the ```/var/www/html``` directory. 

While this works well for a single site, it can become unweildy if multiple sites need to be hosted. We can create a directory structure starting within ```/var/www``` for a domain. 

>**Note:** While most domains now serve ```www.``` protocol, in the past it was common to have sites with ```ftp``` or other domains so that a single url could be used for multiple purporses.  

Creating the directory for the domian: 
```sudo mkdir /var/www/your_domain```

We can assign ownership to the user (instead of root) by using:  
```sudo chown -R $USER:$USER /var/www/your_domain```

If the permissions have changed, we can use:  
```sudo chmod -R 755 /var/www/your_domain```

Next, create a sample index page:  
```nano /var/www/your_domain/index.html```

And paste: 
```html
<html>
    <head>
        <title>Welcome to dissertation!</title>
    </head>
    <body>
        <h1>Success!  The dissertation server block is working!</h1>
    </body>
</html>
```

In order for apache to serve the correct files, we need to create a virtual host file with the correct dirrectives.  Instead of modifying the default configuration file located at ```/etc/apache2/sites-available/000-default.conf``` directly, let’s make a new one at ```/etc/apache2/sites-available/dissertation.conf```:    

```sudo nano /etc/apache2/sites-available/dissertation.conf```

Paste in the following code: 
```conf

```

Save and close the file when you are finished.

Let’s enable the file with the a2ensite tool:   
```sudo a2ensite dissertation.conf``` 
#
Disable the default site defined in 000-default.conf:
```sudo a2dissite 000-default.conf```

Next, let’s test for configuration errors:
```sudo apache2ctl configtest```

You should see the following output:
```
Output
Syntax OK
```

Restart Apache to implement your changes:  
```sudo systemctl restart apache2```

you can now go to ```http://dissertation.localhost/``` instead of ```http://localhost/``` due to your new fancy domian



### Problems i have run into 

**Default vhost file**  

From: ```https://support.rackspace.com/how-to/set-up-apache-virtual-hosts-on-the-ubuntu-operating-system/``` 
 
Although you changed the default virtual host, you did leave it in place.

If someone enters the IP address of the cloud server, they are served the contents of that default vhosts file (if you did not set up a separate vhost for the IP address).

Why are they served from that vhost file?

>Apache searches the enabled vhost files in alphabetical order and if it can’t find one for the requested IP address or domain name, it serves the first one (alphabetically).

If you had disabled or deleted the default vhost file, then the contents of domain1.com would be displayed (being before domain2.com alphabetically).

This is something to consider when planning your websites. Do you want a particular domain to be the default? Do you want the IP address to have completely different content?

>**Note:** 
Creating virtual host configurations on your Apache server does not magically cause DNS entries to be created for those host names. You must have the names in DNS, resolving to your IP address, or nobody else will be able to see your web site. You can put entries in your hosts file for local testing, but that will work only from the machine with those hosts entries.

 - each conf is a different server 
 - if you want to have multiple domians on one server, just have them in the same file

### Removing Apache 
You can remove apache by using:  
```sudo apt-get remove apache2```

### Site not found
This is usally because while the configuration file is avalible, it is not enabled - you can enable a site by using ```sudo a2ensite <exampelsite.conf>```. After this you can run ```systemctl reload apache``` to restart the server.


## 5 Testing PHP Processing on the Web Server

In order to test that your system is configured properly for PHP, create a very basic PHP script called info.php. In order for Apache to find this file and serve it correctly, it must be saved to your web root directory.

Create the file at the web root you created in the previous step by running:  
```sudo nano /var/www/your_domain/info.php```

This will open a blank file. Add the following text, which is valid PHP code, inside the file:  
info.php
```php
<?php
phpinfo();
?>
```
When you are finished, save and close the file.

Now you can test whether your web server is able to correctly display content generated by this PHP script. To try this out, visit this page in your web browser. You’ll need your server’s public IP address again.

The address you will want to visit is:

```http://your_domain/info.php```


The page provides basic details about the server from the perspective of php - you can remove this file (for security reasons) using:  
```sudo rm /var/www/your_domain/info.php```


## 6 (Optional) Creating a symlink from your files to the actual location 
Our files for the web server are hosted under ```/var/www```, while this is a good place for the computer to store files, for us it can make it difficult to create an deploy data if we want to keep a normal directory strucutre ```home/Documents/Programming ```. 

This is where simulated links / soft links, come in:

### Creating a symlink 
The syntax for a symlink is 
Files:  
```ln -s {source-filename} {symbolic-filename}```
Directories:  
```ln -s {source-dir-name} {symbolic-dir-name}```

We can verify our links by using:   
```ln -l {source-filename} {symbolic-filename}```

So for our web server, we can use:   
```ls -s /var/www/ /home/user/Documents/Programming/```

In my case, we can see that the ```dissertation``` project links to ```/var/www/dissertation```:
```
1 george george     22 May 29 12:08  dissertation -> /var/www/dissertation/
```


## 7 phpMyAdmin 
### Installation 
phpMyAdmin can be used to setup and look at your databases without neeeding to use the mySQL command line.

To install phpMyAdmin, we can use ubuntus ```apt``` package manager:  
```sudo apt install phpmyadmin php-mbstring php-gettext```

>**Note:** **Warning**: When the prompt appears, ```apache2``` is highlighted, but **not** selected. If you do not hit SPACE to select Apache, the installer will not move the necessary files during installation. Hit ```SPACE```, ```TAB```, and then ```ENTER``` to select Apache.

After this we need to enable the ```mbstring``` addon:  
```sudo phpenmod mbstring```

Then we can restart apache to see if it works:  
```sudo systemctl restart apache2```

### Configuring Password Access 

Installing PHP onto a server account will automatically create a database *user* called ```phpmyadmin``` which peforms underlying processes in the program. 

Using this account can cause security risks so instead we can log in as ```root```. 

In Ubuntu systems running MySQL 5.7 (and later versions), the root MySQL user is set to authenticate using the auth_socket plugin by default rather than with a password. This allows for some greater security and usability in many cases, but it can also complicate things when you need to allow an external program — like phpMyAdmin — to access the user.

In order to log in to phpMyAdmin as your root MySQL user, you will need to switch its authentication method from auth_socket to mysql_native_password if you haven’t already done so. To do this, open up the MySQL prompt from your terminal:  

```
sudo mysql
```

Next, check which authentication method each of your MySQL user accounts use with the following command:
```
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
```


To configure the root account to authenticate with a password, run the following ```ALTER USER``` command. Be sure to change ```password``` to a strong password of your choosing:  

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'; 
```

Then we can run ```FLUSH PRIVILEGES``` which tells the server to reload the grant tables.

we can check that this works by looking at the ```mysql.user``` table using:   
```
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
```
If the root account now has the ```mysql_native_password``` as its plugin, the change worked and you can now log in as root with the chosen password

















# XAMPP
XAMPP is the linux version of WAMP - Windows, Apache, MySQL, PHP.

>**Note:** Most of what is below can be found at: https://www.apachefriends.org/faq_linux.html

## Installing XAMPP 
You can download the installer at : https://www.apachefriends.org/index.html

Once downloaded, we can change the permissions of the installer (so it has permission to execute on our linux system):
```chmod 755 xampp-linux-*-installer.run```
Run the installer using:
```sudo ./xampp-linux-*-installer.run```

This will run a installation wizard with a graphical component.

## Starting XAMPP 
We can start XAMPP by using: 
```sudo /opt/lampp start```

You can also launch a graphical interface by using:
```
cd /opt/lampp

sudo ./manager-linux.run (or manager-linux-x64.run)
```

We can stop XAMPP using:  
```sudo /opt/lampp/lampp stop```