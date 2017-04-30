## Introduction

# Virtual machine

A virtual machine is a software computer that, like a physical computer, runs an operating system and applications. The virtual machine is comprised of a set of specification and configuration files and is backed by the physical resources of a host.

### Configuration and deployment of the virtual machine

The first screen asks for name and operating systems

# Enter 

  Name:ubuntu-1  
  Type:Linex  
  Version: Ubuntu(32)  
  Then Next
  
From the next screen select memory size 512MB.  
From the next screen select "Create a virtual hard drive now"and then select create.  
Then select VDI(virtualbox disk image) and then press next.  
Choose  "Dynamically allocated" and click next.  
Change the size to 10GB. Click Create.  
Now you will see the virtual machine created but in state " powered off".  

# Inserting a virtual cd..  

Before starting a virtual machine, click on setting button.  
Click on storage..
You should see :  

- Controller: IDE    
- Empty (with a cd icon)  
- Controller: SATA  
- ubuntu-1.vdi  

Click on CD icon by Empaty. To the right you will see:  
- Attributes  
- CD/DVD DRives: IDE Secondary Master, and another cd icon  

Click on this CD icon. From the menu which appears, select"choose a virtual CD/DVD disk file.."  
Browse to the directory where you copied the ubuntu server ISO image, and select it.  
You should now see:  

- Controller: IDE  
- ubuntu- 12.04-3-server -i386  
- Controller: SATA  
- Ubuntu-1.vdi  

click ok.  

# Start the Virtual Machine  

Select the virtual machineand click the green start arrow - or double click the virtual machine and your virtual machine will start.  
The ubuntu installer should start. Click inside the window. Note that you may have to press the host key to get your mouse out again.  
Select your language and press F3 if you want to select a non -US keyboard layout.  
Next press F4 and select" Install a minimal virtual machine".  
Then select " Install Ubuntu Server" from the front menu.  
We do strongly suggest the following settings:  

- Encrypt your home directory? No  
- Partitioning method: Guided - Use entire disk  
- Select none for HTTP proxy  
- No automatic updates  
- Then choose software to install, move to Open SSH Server and hit space to select it, but leave every thing else unselected.  
- Install GRUB boot loader to the master boot record? Yes  

# Try the console  

Here are few basiuc commands you can try:  

$ update  
$ uname -a  
$ df -h  
$ ls /  

# Mouse cursor  

if u want a mouse cursor in ubuntu server, you need to install the package "gpm".These commands need to run with "Sudo".  

$ sudo apt-get update packages  
$ sudo apt-get install gpm  

# ACPI shut down  

$ sudo apt-get install acpid  

## Deploment of a LAMP stack on your Ubuntu Server...   

1. Install Apache Web-Server 

Enter the following commands to install the Apache web server:  

$ sudo apt-get install apache2 apache2-utils  
$ sudo systemctl enable apache2  

We cam start the service by entering the command:  

$ sudo systemctl start apache2  

Apache server is up and running. First we will need to make sure that our
network adapter settings make our VM visible from our host. We will need to shut down our VM and
change the settings on our virtual network adapter. By default our adapter is configured as a
Network Address Translation. We can set up port forwarding with our host to make it accessible
from the host. These settings can be accessed through the Settings – Network – Advanced – Port
Forwarding

2. Install MySQL  

MySQl is a open source database program. It's vital for many features of modern website to maintain database for purpose such as allowing users to login, saving any user generated input to the website.  

# To install the MySQL database server run the following commands:  

$sudo apt-get install mysql-client mysql-server 

We should run the following command to see how security would normally be configured:  

$ sudo mysql_secure_installation  

3. Install PHP and Modules  

PHP is an open source server-side scripting language mainly used for web development. It allows
web developers to create dynamic, interactive websites. Enter the following command to install php
and the modules we will need for our Content Management System.  

$sudo apt-get install php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-cli php7.0-cgi php7.0-gd  

When the command is finished running we need to test that PHP is working. We will do this by
creating a info.php file in our /var/www/html directory.  

Type the following command:  

$ sudo vi /var/www/html/info.php  

This will open a new file called info.php. Press the i key to enter insert mode and then type the
following php code in:  

<?php
phpinfo();
?>  

Press ESC when you’re done entering text then enter the command :wq to save your file and close Vi.
Open your web browser in your host computer and go to the address localhost/info.php You should
see a page containing configuration information.  

### Content Management System (CMS)  

A content management system is a computer application that supports creation and editing of digital content. We are going
to use the world’s most popular CMS Wordpress, an open source CMS, which is used on
approximately 27% of websites.  

1. Install WordPress  

We’ve got all our prerequisites installed and checked that they’re up and running. Now it’s time to
install the CMS. Run the following command to download the latest WordPress package from their
repository:  
$ wget -c http://wordpress.org/latest.tar.gz  

When the download is complete we need to extract the files from the compressed folder. Enter the following command to extract the archive to the current directory:  

$ tar -xzvf latest.tar.gz  

We need to move all the contents of the WordPress folder to the default Apache root directory with
the following command.  

$ sudo rsync -av wordpress/* /var/www/html/  

Finally we need to set the correct permissions on the website directory. That is to give ownership of
the word files to the web server (called www-data) :  

$ sudo chown -R www-data:www-data /var/www/html  

Then change permissions to allow anyone to read and execute the file but only the owner will be
able to write.  

$ sudo chmod -R 755 /var/www/html  

2. Create a MySQL database for wordpress  

Before we can run Wordpress we need to set up a MySQL database for it. Enter the following
command to open MySQL  

$ mysql -u root -p  

With MySQL now open enter the following commands line by line to create your database. Make
sure you use a strong and secure password.  

CREATE DATABASE wp_project;  

GRANT ALL PRIVILEGES ON wp_project.* TO ‘your_username_here’@’localhost’ IDENTIFIED BY
‘your_chosen_password_here’;  

FLUSH PRIVILEGES;  

EXIT;  

We can restart the web server and MySQL service to allow changes to take affect.  

sudo systemctl restart apache2.service  

sudo systemctl restart mysql.service  

Go to the address http://localhost:80/wp-config-sample.php
You will be prompted to enter the information about your MySQL database which you created in the
previous step.  

3. Configure your wordpress site  

Once you have finished connecting your MySQL database to wordpress it should trigger the start of
the wordpress, browser-based setup. You will need to enter some details here (make sure you save
the password).
Once you’ve finished this process you should be logged into the wordpress Dashboard from which
you administer your website. Make sure you can access your index page (you may need to delete the
old apache “It works!” index.html file before you can see the index.php file wordpress has created.

### Conclusion  














