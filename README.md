# Ubuntu-Init



## install lamp 

* sudo apt-get update
* sudo apt-get install apache2
* sudo apt-get install mysql-server php5-mysql
* sudo mysql_install_db
* sudo mysql_secure_installation
* sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
* sudo apt-get install libssl-dev






## install php 5.6

* sudo add-apt-repository ppa:ondrej/php
* sudo apt-get update
* sudo apt-get purge php5-common
* sudo apt-get install libapache2-mod-php5.6
* sudo apt-get install php5.6-mbstring
* sudo apt-get install php5.6-mysql


## keep php version 

* sudo a2dismod php5
* sudo a2enmod php5.6





## enabel modes

* sudo phpenmod mcrypt           // optinal
* sudo phpenmod mbstring           // optinal
* sudo a2enmod rewrite
* sudo systemctl restart apache2         // optinal

## allaw httaccess

* sudo nano /etc/apache2/apache2.conf
```
    <Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
```

## phpmyadmin

* sudo apt-get install phpmyadmin     
* sudo apt-get install gksu
* gksu gedit /etc/apache2/apache2.conf

add this to end of the file

    Include /etc/phpmyadmin/apache.conf




## at the end
* sudo service apache2 restart


## install git 

* sudo apt-get install git

## install zip 

* sudo apt-get install zip

## install composer
* curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer



## create vHost

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


## add to hosts

* sudo gedit /etc/hosts


## enbel site

* sudo a2ensite work.com
* service apache2 reload




## install node js

* sudo apt-get install python-software-properties
* curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
* sudo apt-get install nodejs


## install mongo db 

* sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
* echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
* sudo apt-get update
* sudo apt-get install -y mongodb-org
* sudo service mongod status


## install redis


## search for conflicts in dir
* grep -H -r "<<<<<<< HEAD" /path/to/project/dir

