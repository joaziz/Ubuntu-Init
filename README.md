# Ubuntu-Init


> first you need to update and upgrade apt-get
> use 
> ```
> sudo apt-get update
> sudo apt-get upgrade  // it may take long time
>```
> press `ctrl` `alt` `T` to open new terminal window

## Install Apaach2 
* sudo apt-get install apache2
* sudo apt-get install libapache2-mod-php5 // choose you version

## Install php 
* sudo apt-get install php5 php5-mcrypt php5-mysql libssl-dev
 
## Install MySql 
* sudo apt-get install mysql-server
* sudo mysql_install_db
* sudo mysql_secure_installation


## keep php version 

* sudo a2dismod php5
* sudo a2enmod php5.6


## phpmyadmin

* sudo apt-get install phpmyadmin     
* sudo apt-get install gksu
* gksu gedit /etc/apache2/apache2.conf

add this to end of the file

    Include /etc/phpmyadmin/apache.conf


## Install php 5.6 for Ubuntu 14.4

* sudo add-apt-repository ppa:ondrej/php
* sudo apt-get update
* sudo apt-get purge php5-common
* sudo apt-get install libapache2-mod-php5.6
* sudo apt-get install php5.6-mbstring
* sudo apt-get install php5.6-mysql



## Enabel modes

* sudo phpenmod mcrypt           // optinal
* sudo phpenmod mbstring           // optinal
* sudo a2enmod rewrite
* sudo systemctl restart apache2         // optinal

## Allaw httaccess

* sudo nano /etc/apache2/apache2.conf
```
    <Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
```



## At the end
* sudo service apache2 restart


## Install git 

* sudo apt-get install git

## Install zip 

* sudo apt-get install zip

## Install composer
* curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer



## Create vHost

* sudo gedit /etc/apache2/sites-available/{website_name}.dev.conf

past this inside

    <VirtualHost *:80>
          ServerName work.com
          DocumentRoot /var/www/html/work/public
   	      ErrorLog ${APACHE_LOG_DIR}/error.log
    	    CustomLog ${APACHE_LOG_DIR}/access.log combined
        
	        <Directory /var/www/html/work/public>
              AllowOverride All
              Require all granted
          </Directory>
    </VirtualHost>

after this 

* sudo a2enmod rewrite


## Add to hosts

* sudo gedit /etc/hosts


## Enabel site

* sudo a2ensite work.com
* service apache2 reload




## Install node js

* sudo apt-get install python-software-properties
* curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
* sudo apt-get install nodejs


## Install mongo db 

* sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
* echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
* sudo apt-get update
* sudo apt-get install -y mongodb-org
* sudo service mongod status


## Install redis


## Search for conflicts in dir
* grep -H -r "<<<<<<< HEAD" /path/to/project/dir

## install Nginx

* wget http://nginx.org/keys/nginx_signing.key
* sudo apt-key add nginx_signing.key
* sudo nano /etc/apt/sources.list
   
post it inside

    deb http://nginx.org/packages/ubuntu/ xenial nginx // Xential is distrubiotion codename
    deb-src http://nginx.org/packages/ubuntu/ xenial nginx
* sudo apt-get update
* sudo apt-get install nginx

## Compres Videos 
* ffmpeg -i videoS1.mp4 -r 30 -s 960x540 videoS1_test.mp4
