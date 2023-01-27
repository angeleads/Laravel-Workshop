# Introduction to Laravel

Welcome to your first introduction to the beautiful world of Laravel (trust me you're going to love it)
But before that, let's get started with the installation (good luck...)

## Installation

<details>
  <summary>Ubuntu:</summary>

Let's first install a webserver to host the Laravel application. You can either use [Apache](https://httpd.apache.org/) or [Nginx](https://www.nginx.com/) web server. 

But let's all use Apache to not get lost...

## Step 1: Apache2

1 - Install apache2, type:
```
$ sudo apt install apache2
```
2- Once installed, Apache should be running. If it's not, for whatever reason, start it:
```
$ sudo systemctl start apache2
```
3- Then enable it to start on boot time.
```
$ sudo systemctl enable apache2
```
3- To verify the status of Apache, execute:
```
$ sudo systemctl status apache2
```

## Step 2: PHP

Laravel 8 requires PHP 7.3 or above. Thankfully, PHP 7.4 is available in Ubuntu repositories. So, install PHP and the following PHP extensions.
```
$ sudo apt install php libapache2-mod-php php-mbstring php-cli php-bcmath php-json php-xml php-zip php-pdo php-common php-tokenizer php-mysql
```

When the installation is complete, verify the PHP version.
```
$ php -v
```

## Step 3: Create Database for Laravel Application

Next up, we will create a database for the Laravel application.

But first, we need to install MySQL. 
This is a tricky part so 
***If you meet any issue, feel free to come to me :)***

Now that MySQL is installed, let's create our project's database!
```
$ sudo mysql -u root -p
```
Once logged in create the database, and database user, and grant all privileges to the database user.
```
> CREATE DATABASE laravel_db;
```

```
> CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'secretpassword';
```
```
> GRANT ALL ON laravel_db.* TO 'laravel_user'@'localhost';
```
```
> FLUSH PRIVILEGES;
```
```
> QUIT;
```

## Step 4: Install Composer
Composer is a dependency package manager for PHP. It provides a framework for managing libraries and dependencies and required dependencies. To use Laravel, first install composer.

To download Composer, invoke the command shown.
```
$ curl -sS https://getcomposer.org/installer | php
```
Next, move the composer file to the /usr/local/bin path.
```
$ sudo mv composer.phar /usr/local/bin/composer
```
Assign execute permission:
```
$ sudo chmod +x /usr/local/bin/composer
```
Verify the Composer version installed:
```
$ composer --version
```
## Step 5: Install Laravel 8 on Ubuntu
With Composer installed, the next course of action is to install Laravel.
Navigate to the webroot directory, type:
```
$ cd /var/www/html
```
Now, install Laravel using the composer command, type:
```
$ sudo composer create-project laravel-introduction
```

The command creates a new directory called laravel-introduction and installs all the files and directories for Laravel.
Change the ownership of the Laravel directory to the webserver user and also the permissions:
```
sudo chown -R www-data:www-data /var/www/html/laravel-introduction
sudo chmod -R 775 /var/www/html/laravel-introduction/storage
```
Once the installation is done navigate to the installation directory and check the Laravel version.
```
$ cd laravel-introduction
  php artisan
```

## Step 6: Configure Apache to serve Laravel site
Lastly, we need to set up the Apache webserver to host the Laravel site. For that to happen, we need to create a virtual host file.
```
$ sudo vim /etc/apache2/sites-available/laravel.conf
```
Next, past the content shown and replace the example.com ServerName directive with the FQDN or public IP of the server ( Or private IP in case the server is on a LAN network ).
```
<VirtualHost *:80>
ServerName example.com
ServerAdmin admin@example.com
DocumentRoot /var/www/html/laravelapp/public
<Directory /var/www/html/laravelapp>
AllowOverride All
</Directory>
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Save the changes and exit the file. Next, enable the Laravel site and Apache rewrite module using these two commands.
```
$ sudo a2ensite laravel.conf
```
```
$ sudo a2enmod rewrite
```
To apply the changes, restart Apache.
```
$ sudo systemctl restart apache2
```

## Step 7: Access Laravel from a browser
Finally, to access Laravel visit your server's FQDN or IP address. The default Laravel webpage will be displayed.

</details>