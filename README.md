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
sudo apt install apache2
```
2- Once installed, Apache should be running. If it's not, for whatever reason, start it:
```
sudo systemctl start apache2
```
3- Then enable it to start on boot time.
```
sudo systemctl enable apache2
```
3- To verify the status of Apache, execute:
```
sudo systemctl status apache2
```

## Step 2: PHP

Laravel 8 requires PHP 7.3 or above. Thankfully, PHP 7.4 is available in Ubuntu repositories. So, install PHP and the following PHP extensions.
```
sudo apt install php libapache2-mod-php php-mbstring php-cli php-bcmath php-json php-xml php-zip php-pdo php-common php-tokenizer php-mysql
```

When the installation is complete, verify the PHP version.
```
php -v
```

Make sure to at least have the ***PHP 8.0.23 version*** installed!

## Step 3: Create Database for Laravel Application

Next up, we will create a database for the Laravel application.

But first, we need to install MySQL. 
This is a tricky part so 
***If you meet any issue, feel free to come to me :)***

Now that MySQL is installed, let's create our project's database!
```
sudo mysql -u root -p
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
curl -sS https://getcomposer.org/installer | php
```
Next, move the composer file to the /usr/local/bin path.
```
sudo mv composer.phar /usr/local/bin/composer
```
Assign execute permission:
```
sudo chmod +x /usr/local/bin/composer
```
Verify the Composer version installed:
```
composer --version
```

Make sure to at least have the ***Composer version 2.5.1*** installed!
## Step 5: Install Laravel 8 on Ubuntu
Congratulations!! You're almost there!!
With Composer installed, the next course of action is to install Laravel.

Now, install Laravel using the composer command, type:
```
sudo composer create-project laravel-introduction-workshop
```

You project is now installed, you can access to it
```
cd laravel-introduction-workshop
  php artisan
```

Now to run your project, all you need to do is run the following command and click the link given!
```
php artisan serve 
```

Congratulations! You have successfully installed Laravel, now have fun :)

## Step 6: Configure Apache to serve Laravel site
Lastly, we need to set up the Apache webserver to host the Laravel site. For that to happen, we need to create a virtual host file.
```
sudo vim /etc/apache2/sites-available/laravel.conf
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

<details>
  <summary>Fedora</summary>

## Step 1: Install PHP

Since it is a PHP framework it is obvious that you must install PHP. So let’s go for it.
```
sudo dnf install php php-common php-cli php-pdo php-mbstring php-zip php-xml php-cli php-json
```

## Step 2: Install MySQL
Follow these [easy step](https://computingforgeeks.com/how-to-install-mysql-8-on-fedora/)***If you meet any issue, feel free to come to me :)***

## Step 3: Install Composer
Composer is a dependencies manager for PHP. So, it is very useful to manage libraries required by our projects and is used to install Laravel.
```
curl -sS https://getcomposer.org/installer | php
```

Then, make sure that Composer can be used globally in the terminal.

```
sudo mv composer.phar /usr/local/bin/composer
sudo chmod +x /usr/local/bin/composer
composer -V
```

## Step 4: Install Laravel

It’s time to install Laravel. So, run this command.
```
composer global require "laravel/installer"
```
Once the installation is finished. You can create a new project. But, first, make Laravel executable available for the system.

```
echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc
```

Then, close the terminal and open it again. Now, create a project.
```
laravel new laravel-introduction-workshop
```
```
php artisan serve
```
Congratulations! You have successfully installed Laravel, now have fun :)

</details>

After making sure everything is installed and fully functional, make sure to follow these activities

## Activities
For this workshop, you will be handling a music shop's website!

With the given database ***music.sql***, make your own shop :)

Before that, make sure to have the correct access to the database!
Run the following command with your chosen password to access your sql databases
```
mysql -u root -p password
```

After that, import the database

```
> source music.sql;
```

Then, all you need to do is use that database
```
> USE Music;
```
Now that you're all set, let your laravel project know about that database
In the *.env* given file, enter your information as such

![database-exemple](https://github.com/angeleads/Laravel-Workshop/tree/main/resources/laravel-music-database.png)

### Step 1: Create card component
Go through the views sections and create a component to create cards.
The cards need to have a label for:
- Image for the album
- Name of the artist
- Title of the album
- Genre
- Release date

### Step 2: From database to laravel
Now to the tricky part! 

You are now asked to put the information given in the database in the component you previously made.

Make sure to import the SQL script with the .env file :)

### Step 3: Add a card
Good job! If you already made it all the way here you're a literal pro!

Now I'm going to ask you to create a button to add a card, it will create an empty card that has text input where you can add the component cards information and save thanks to a button

### Step 4: Delete a card
Almost there!

Now all you need to do is make a delete button at the top right of the cards and when clicked, the cards disappear and their information is removed from the database.

### Step 5: Update a card
Final step! You're a legend!

For this one, create an edit button that helps you change the card's information and update it even on the database.


### Collaborators

[Angel Amélia Halouane](https://github.com/angeleads)

[Blanca Sibecas Hernandez](https://github.com/bsibecas)