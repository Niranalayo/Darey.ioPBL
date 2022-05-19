
# LAMP STACK INSTALLATION

### There were 5 installations/process involved in the this project.

## STEP ONE- INSTALLING APACHE AND UPDATING THE FIREWALL:

### This was done using Ubuntu package manager *apt*
### Three steps are involves in ensuring this:
`sudo apt update`

`sudo apt install apache2`

`sudo systemctl status apache2`


### The Images below show Apache installed and evidence that the Apache is running

![Install Apache](./Images/Install%20Apache2.PNG)


![Verify Apache runnung](./Images/Verify%20Apache2%20runnung.PNG)

### To confirm the server is correctly installed, is to run the IP address and if the welcome Ubuntu pages show, this confirms that it has been installed correctly.

![Web Page uploaded correctly](./Images/Web%20Test.PNG)

### This concludes and confiems that the Apaches is up and running smoothly.





# INSTALLING MYSQL

### The second phase involves installing a database that will store all the data that will be displayed by the Apache when requested by the user/client.

### To do this, we need to run some codes in stages.


### Again we use apt command to install the Database

`$ sudo apt install mysql-server`

![MySQL Server Installed](./Images/MySQL%20image.PNG)


### When download is completed, one can log in by running the sudo command again:
`$ sudo mysql`

### Once done, you can interact with the database by runnung:

`$ sudo mysql_secure_installation`
![Succesfully Installed](./Images/Install%20MySQL%20server.PNG)

### Once completed and password set, you can exit by running the command code:

`mysql> exit`



# INSTALLING PHP
### The third step is installing PHP.
### PHP is the code that will help display information to the user. 
### As well as displaying information, the PHP codes is also used to retrieve data from the Database MySQL

### Three packages need to be installed and this is done by inputting the data.

`sudo apt install php libapache2-mod-php php-mysql`

### The next code confirms that PHP has been installed
`php -v`



![PHP has now been installed](./Images/Install%20PHP.PNG)

![Confirmation screenshot](./Images/PHP%20intstalled%20confirm2.PNG)




# CREATING A VIRTUAL HOST


### Once all steps completed, we now need to create a virtual host for our website.
### To do this we need to
### 1. Create a new directory

`sudo mkdir /var/www/projectlamp`


### 2. Assign user

` sudo chown -R $USER:$USER /var/www/projectlamp`


### 3. Configure and create a new file in Apache's directory

`sudo vi /etc/apache2/sites-available/projectlamp.conf`


### 4. use the ls command to show the new file in the sites-available directory

`sudo ls /etc/apache2/sites-available`

### You can now use a2ensite command to enable the new virtual host:
`sudo a2ensite projectlamp`

### 5. To make sure your configuration file doesn’t contain syntax errors, run:

`sudo apache2ctl configtest`


### 6. Finally, reload Apache so these changes take effect:

`sudo systemctl reload apache2`

### The new website is now active.



### 7. But the web root is still empty. We need to create an index.html file in that location so that we can test that the virtual host works as expected:

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`




### Now when we open the browser by using my IP address.

![alt text](./Images/New%20Host%20Creation.PNG)






# ENABLING PHP ON A WEBSITE

### By default, an HTML file will take precedence over a PHP file as the defaul is always HTML and will always take precedence over a home PHP file.

### To enable a PHP file we need to do the followings:

### 1. You need to change the order of the file in which the PHP file is listed in the directory 

`sudo vim /etc/apache2/mods-enabled/dir.conf`

### <IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>


### 2. Save and close the above file.


### 3. After saving the file, we will need to uplaod Apache for the changes to take effect using:

`sudo systemctl reload apache2`


### 4. Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

### Now that I have a custom location to host my website’s files and folders, I then need to create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

### 5. Create a new file named index.php inside my custom web root folder:

`vim /var/www/projectlamp/index.php`

### This will open a blank file. I then add the following text, which is valid PHP code, inside the file:


### `<?php
### phpinfo();`


![PHP Page displayed and confirmed](./Images/PHP%20Page.PNG)



### 6. After checking the relevant information about the PHP server through the above page, it’s best to remove the file  created as it contains sensitive information about the PHP environment -and my Ubuntu server. You can use rm to do so:
`sudo rm /var/www/projectlamp/index.php`

### This page can always be recreated to access the information later.




    
