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


## Enable Proxy server on apach2

first make sure you install apache correct and its working fine
then run this commands : 

Installing Apache And mod_proxy
Note: Instructions given here are kept brief, since chances are you already have Apache installed or know how to use it. Nonetheless, by following the steps below you can get a new Ubuntu VPS running Apache in a matter of minutes.

Updating The Operating-System
We will begin with preparing our virtual server. We are going to first upgrade the default available components to make sure that we have everything up-to-date.

Update the software sources list and upgrade the dated applications:

	sudo aot update
	sudo apt -y upgrade

Getting The Essential Build Tools
Let's continue with getting the essential package for application building - the build-essential. This package contains tools necessary to install certain things from source.

Run the following command to install build-essential package:

	sudo apt install -y build-essential

Getting The Modules And Dependencies
Next, we are going to get the module and dependencies.

Run the following command to install them:

	sudo apt install -y libapache2-mod-proxy-html libxml2-dev

Configuring Apache To Proxy Connections
Activating The Modules
Before configuring Apache, we are going to enable the necessary modules that we will be using in this tutorial, or which might come in handy in the future.

First, let's verify that all modules are correctly installed and ready to be activated.

Run the following command to get a list of available Apache modules:

	sudo a2enmod

You will be presented with an output similar to:

	Your choices are: access_compat actions alias allowmethods asis auth_basic auth_digest auth_form authn_anon authn_core authn_dbd authn_dbm authn_file authn_socache authnz_ldap authz_core authz_dbd authz_dbm authz_groupfile authz_host authz_owner authz_user autoindex buffer cache cache_disk cache_socache cgi cgid charset_lite data dav dav_fs dav_lock dbd deflate dialup dir dump_io echo env expires ext_filter file_cache filter headers heartbeat heartmonitor include info lbmethod_bybusyness lbmethod_byrequests lbmethod_bytraffic lbmethod_heartbeat ldap log_debug log_forensic lua macro mime mime_magic mpm_event mpm_itk mpm_prefork mpm_worker negotiation proxy proxy_ajp proxy_balancer proxy_connect proxy_express proxy_fcgi proxy_fdpass proxy_ftp proxy_html proxy_http proxy_scgi proxy_wstunnel ratelimit reflector remoteip reqtimeout request rewrite sed session session_cookie session_crypto session_dbd setenvif slotmem_plain slotmem_shm socache_dbm socache_memcache socache_shmcb speling ssl status substitute suexec unique_id userdir usertrack vhost_alias xml2enc
	# Which module(s) do you want to enable (wildcards ok)?

Once you are prompted with the choice of modules you desire, you can pass the below line listing the module names:

The list of modules:

	proxy proxy_ajp proxy_http rewrite deflate headers proxy_balancer proxy_connect proxy_html

Or alternatively, you can run the following commands to enable the modules one by one:

	sudo a2enmod proxy
	sudo a2enmod proxy_http
	sudo a2enmod proxy_ajp
	sudo a2enmod rewrite
	sudo a2enmod deflate
	sudo a2enmod headers
	sudo a2enmod proxy_balancer
	sudo a2enmod proxy_connect
	sudo a2enmod proxy_html

Note: Some modules are likely to be enabled by default. Trying to enable them twice will just ensure that they are active.

Modifying The Default Configuration
In this step, we are going to see how to modify the default configuration file 000-default.conf inside /etc/apache2/sites-enabled to set up "proxying" functionality.

Run the following command to edit the default Apache virtual host using the nano text editor:

nano /etc/apache2/sites-enabled/000-default.conf
Here, we will be defining a proxy virtual host using mod_virtualhost and mod_proxy together.

Copy-and-paste the below block of configuration, amending it to suit your needs:

	<VirtualHost *:*>
    	ProxyPreserveHost On

	    # Servers to proxy the connection, or;
	    # List of application servers:
	    # Usage:
	    # ProxyPass / http://[IP Addr.]:[port]/
	    # ProxyPassReverse / http://[IP Addr.]:[port]/
	    # Example: 
	    ProxyPass / http://0.0.0.0:8080/
	    ProxyPassReverse / http://0.0.0.0:8080/

	    ServerName localhost
	</VirtualHost>

Press CTRL+X and confirm with Y to save and exit.

Note: To learn more about virtual host configurations, you can check out the detailed Apache manual on the subject by clicking here.

Enabling Load-Balancing
If you have multiple back-end servers, a good way to distribute the connection when proxying them is to use Apache's load balancing features.

Start editing the virtual-host settings like the previous step, but this time using the below configuration example:

<Proxy balancer://mycluster>
    # Define back-end servers:

    # Server 1
    BalancerMember http://0.0.0.0:8080/

    # Server 2
    BalancerMember http://0.0.0.0:8081/
</Proxy>

<VirtualHost *:*>
    # Apply VH settings as desired
    # However, configure ProxyPass argument to
    # use "mycluster" to balance the load

    ProxyPass / balancer://mycluster
</VirtualHost>
Enabling SSL Reverse-Proxy Support
If you are dealing with SSL connections and certificates, you will also need to enable a secondary virtual host with below settings.

Repeat the steps from the previous steps but using these configuration options:

Listen 443

NameVirtualHost *:443
<VirtualHost *:443>

    SSLEngine On

    # Set the path to SSL certificate
    # Usage: SSLCertificateFile /path/to/cert.pem
    SSLCertificateFile /etc/apache2/ssl/file.pem


    # Servers to proxy the connection, or;
    # List of application servers:
    # Usage:
    # ProxyPass / http://[IP Addr.]:[port]/
    # ProxyPassReverse / http://[IP Addr.]:[port]/
    # Example: 
    ProxyPass / http://0.0.0.0:8080/
    ProxyPassReverse / http://0.0.0.0:8080/

    # Or, balance the load:
    # ProxyPass / balancer://balancer_cluster_name

</VirtualHost>
Restarting Apache
Once you are happy with your configuration, you will need to restart the cloud server for the changes to go into effect.

Execute the following command to restart Apache:

service apache2 restart
And that's it!

You can now visit your VPS and Apache shall reverse-proxy connections to your back-end application servers.
