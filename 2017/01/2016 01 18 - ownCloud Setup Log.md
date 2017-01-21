# Important
This guide isn't complete and may contain mistakes and steps that doesn't match your enviornment. This is just a log of the steps I did, nothing more.

# Configure Droplet to use SSH Keys for Login  
- While creating the droplet, choose to add SSH key.  
- Paste the public key part of the SSH  
- In Passwords and Keys app, under Secure Shell > OpenSSH Keys, right click on your key and choose Configure for Key for Secure Shell.  
- Provide the IP of the droplet, and use port number 22  
- Login name is root.  
- Click Set Up.  
- Now, from the terminal, use ssh root@<ip> to login to the machine without password  
- Tutorial: [How to connect to remote server on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server-in-ubuntu).  
- When using Windows, [generate and add SSH keys with Putty](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-putty-on-digitalocean-droplets-windows-users) for easier login. After the private key is generated for Putty, [double-click on it and enter passphrase](http://superuser.com/a/211180/96992) to save it for even easier login.  

# Set up terminal
- `apt install zsh`  
- `chsh -s /usr/bin/zsh`  
- exit  
- Log in again to find shell has changed  
- `sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`  
- `git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUTSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`  
- `apt install httpie`  
    - httpie is easier to use than curl
- `apt install grc`  
    - grc adds coloring of command output
- `cd $ZSH/custom`  
- `http --download https://raw.githubusercontent.com/garabik/grc/master/grc.zsh`  
- Add the `~/.oh-my-zsh/custom/aliases.zsh` to list the aliases you like:  
	- `alias ll="ls -al"`  
	- `alias download="http -d"`  

# Install requirements
- `apt upgrade`  
	- Upgrades packages before starting an install  
- `apt install apache2`  
- `apt install postgresql`  
	- Default is mariadb-server  
- `apt install postgresql-client`  
- `apt install libapache2-mod-php7.0`  
	- Default is libapache2-mod-php5  
- `apt install php7.0-gd`  
- `apt install php7.0-json`  
- `apt install php7.0-pgsql`  
- `apt install php7.0-curl`  
- `apt install php7.0-intl`  
- `apt install php7.0-mcrypt`  
- `apt install php-imagick`  
- Use `php -m` to check installed PHP modules  
- Modules that are already installed:  
	- ctype  
	- gd  
	- iconv  
	- json  
	- libxml  
	- posix  
	- zlib  
	- pgsql  
	- curl  
	- fileinfo  
	- intl  
	- mcrypt  
	- openssl  
	- imagick  
	- pcntl  
- Modules to be installed  
	- Common  
		- `apt install php7.0-common`  
	- dom, SimpleXML, XMLWriter  
		- `apt install php7.0-xml`  
	- mb multibyte  
		- `apt install php7.0-mbstring`  
	- zip  
		- `apt install php7.0-zip`  
	- bz2  
		- `apt install php7.0-bz2`  
	- ldap  
		- `apt install php7.0-ldap`  
	- smbclient  
		- `apt install php-smbclient`  
	- ftp  
		- `apt install php-net-ftp`  
	- imap  
		- `apt install php7.0-imap`  
	- exif  
		- `apt install exif`  
	- gmp  
		- `apt install php7.0-gmp`  
	- redis (why [choose redis over memcached](http://stackoverflow.com/questions/10558465/memcached-vs-redis), learn [how to set up memory caching for NextCloud](https://docs.nextcloud.com/server/10/admin_manual/configuration_server/caching_configuration.html))  
		- `apt install redis-server`  
		- `apt install php-redis`  
- For generating previews:  
	- ffmpeg  
		- `apt install ffmpeg`  
	- LibreOffice  
		- `apt install libreoffice`  
		- Configure document preview   

# Download Nextcloud
- `http -d https://download.nextcloud.com/server/releases/nextcloud-10.0.1.tar.bz2`  
	- Replace the URL with an updated URL. Find the correct one in the [Downloads page](https://nextcloud.com/install/).  
- `tar -xjf nextcloud-x.y.z.tar.bz2`  
    - unzip nextcloud-x.y.z.zip  
	- This extracts the tarball into the same folder as a nextcloud folder.  
- `cp -r nextcloud /var/www`  
	- This copies the nextcloud folder to the Apache document folder.  

# Use FastCGI to run PHP on Apache  
- FastCGI is faster than the default mod_php module included with Apache. It also [consumes less resources](https://www.linode.com/docs/websites/apache/running-fastcgi-php-fpm-on-debian-7-with-apache)  
- The FastCGI Process Manager (PHP-FPM) helps to reduce the amount of system resources used  
- Tutorials:  
	- [Apache with PHP FPM on Ubuntu 16.04](https://www.howtoforge.com/tutorial/apache-with-php-fpm-on-ubuntu-16-04/)
	- [Using PHP-FPM with Apache on Ubuntu 16.04](https://www.howtoforge.com/tutorial/apache-with-php-fpm-on-ubuntu-16-04/)  
	- [How to Configure Apache on an Ubuntu or Debian VPS](https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps)
- Remove default Apache module to handle PHP requests  
	- apt remove libapache2-mod-php7.0  
- To install:  
	- apt install libapache2-mod-fastcgi  
	- apt install php7.0-fpm  
	- a2enmod actions fastcgi alias  
		- Enable Apache modules: actions, fastcgi, and alias  
	- service apache2 restart  
		- Restart Apache to apply changes  
	- Modify the Apache configurations to add handler for PHP. Modify the file /etc/apache2/apache2.conf to add the following inside `<VirtualHost>`  
```
    <Directory /usr/lib/cgi-bin>                
        Require all granted
    </Directory>
    <IfModule mod_fastcgi.c>
        AddHandler php7-fcgi .php
        Action php7-fcgi /php7-fcgi virtual
        Alias /php7-fcgi /usr/lib/cgi-bin/php7-fcgi
        FastCgiExternalServer /usr/lib/cgi-bin/php7-fcgi -socket /var/run/php/php7.0-fpm.sock -pass-header Authorization
    </IfModule>  
```
- This section above is added to the apache2.conf file to apply to both virtual hosts for HTTP and HTTPS  
- Create a php file under the html folder to test PHP handling.  
	- `vi /var/www/html/info.php`  
	- Add the following in the file:  
```php
<?php
phpinfo();
```
- Restart Apache  
	- `service apache2 restart`  
- In the browser, test the page <serverip>/info.php  
- The value of Server API should be FPM/FastCGI  

# Configure Apache for Nextcloud
- Tutorial: [How to Configure Apache Web Server on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps)
- Create this file `/etc/apache2/sites-available/nextcloud.conf` with this content:
```conf
Alias /nextcloud "/var/www/nextcloud/"  
<Directory /var/www/nextcloud/>
  Options +FollowSymlinks
  AllowOverride All

 <IfModule mod_dav.c>
  Dav off
 </IfModule>

 SetEnv HOME /var/www/nextcloud
 SetEnv HTTP_HOME /var/www/nextcloud

</Directory>
```
- Create a symlink to point to this file
	- `ln -s /etc/apache2/sites-available/nextcloud.conf /etc/apache2/sites-enabled/nextcloud.conf`

- Enable mod_rewrite module
	- `a2enmod rewrite`
- Enable other recommended modules
	- `a2enmod headers`
	- `a2enmod env`
	- `a2enmod dir`
	- `a2enmod mime`
- Because Nextcloud uses Basic authentication internally for Webdav service, we need to enable a security setting in Apache for this to work.	 
- In the `/etc/apache2/sites-available/nextcloud.conf` file, add inside the Directory section
	- `Satisfy Any`
- Restart Apache for configurations to take effect
	- `service apache2 restart`

# Pretty URLs
- CAUTION: There's an [issue with pretty URLs that hasn't been resolved yet](https://help.nextcloud.com/t/apache-rewrite-to-remove-index-php/658/36), even though the .htaccess file has been updated.
- From the [documentation](https://docs.nextcloud.com/server/10/admin_manual/installation/source_installation.html)
	> Pretty URLs are created automatically when .htaccess is writable by the HTTP user, `mod_env` and `mod_rewrite` are installed, and `'overwrite.cli.url'` in your `config.php` is set to any non-null value.
- Both `mod_env` and `mod_rewrite` are installed.
- The `'overwrite.cli.url'` parameter is in the config.php file which is under `/var/www/nextcloud/config` should have a value other than null
	- The value should be the path (URL path, not file path) to the Nextcloud app. If your Nextcloud is installed at https://my.cloud/nextcloud, then the value is /nextcloud
- However, the HTTP user (www-data) doesn't have write permission to .htaccess
	- To give it access use: chmod g+w /var/www/nextcloud/.htaccess
- Run this command to let Nextcloud update the .htacess file
	- sudo -u www-data php occ maintenance:update:htaccess

# Enabling SSL
- Enable SSL module
	- `a2enmod ssl`
- Restart service
	- `service apache2 restart`
- Apache on Ubuntu comes with a simple self-signed SSL certificate
- To create your own self-signed certificate
	- `mkdir /etc/apache2/ssl`
	- `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt`
- Configure Apache to use SSL
	- `vi /etc/apache2/sites-available/default-ssl.conf`
	- You'll find a section with `SSLCertificateFile` and `SSLCertificateKeyFile`, replace the values with the values provided above to the openssl command.
	- It's better to comment out the lines and write new ones to keep them and go back to them in case of problems.
- Enable SSL site
	- `a2ensite default-ssl.conf`
- Reload service
	- `service apache2 reload`
- Tutorial: [How to Create a SSL Certificate on Apache for Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04)

# Configure Postgres
- Install additional tools for postgres
	- `apt install postgresql-contrib`
- Modify `/etc/php/7.0/mods-available/pgsql.ini` to add the following:
```ini
[PostgresSQL]
pgsql.allow_persistent = On
pgsql.auto_reset_persistent = Off
pgsql.max_persistent = -1
pgsql.max_links = -1
pgsql.ignore_notice = 0
pgsql.log_notice = 0
```
- Check `/etc/postgresql/9.5/main/pg_hba.conf` to see which type of authentication is used, `md5` or `peer`. Peer should be better in this scenario.
- Login to postgres
	- `su postgres`
		- This switchs to the postgres user instead of root.
	- `psql -d template1`
		- This starts PSQL with the Template1 database.
- Create nextcloud database:
	- `CREATE DATABASE nextcloud;`
- Create nextcloud user with password:
	- `CREATE USER nextcloud WITH PASSWORD 'password';`
- Modify some configurations for the new user:
	- `ALTER ROLE nextcloud SET client_encoding TO 'utf8';`
	- `ALTER ROLE nextcloud SET default_transaction_isolation TO 'read committed';`
	- `ALTER ROLE nextcloud SET timezone TO 'UTC';`
- Give nextcloud user permission to access nextcloud database:
	- `GRANT ALL PRIVILEGES ON DATABASE nextcloud TO nextcloud;`
- Exit psql
	- `\q`
- During installation, the config/config.php file should contain these settings
```php
<?php

  "dbtype"        => "pgsql",
  "dbname"        => "nextcloud",
  "dbuser"        => "nextcloud",
  "dbpassword"    => "password",
  "dbhost"        => "localhost",
  "dbtableprefix" => "oc_",
```
- References
	- [Nextcloud configurations for Postgres](https://docs.nextcloud.com/server/10/admin_manual/configuration_database/linux_database_configuration.html#postgresql-database)
	- [Configuring Postgres for Django application on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-16-04)
	- [Postgres roles best practice implementation](http://serverfault.com/questions/483998/postgres-roles-best-practice-implementation)
	- [How to Use Roles and Manager Grant Permissions in PostgreSQL on a VPS](https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2)
  
# Install Nextcloud
- [Installing Nextcloud from the command line](https://docs.nextcloud.com/server/10/admin_manual/installation/command_line_installation.html)
- Change permission of /var/www/nextcloud folder to www-data user
	- `chown -R www-data:www-data /var/www/nextcloud/`
- Run `occ` from the terminal
	- `sudo -u www-data php occ  maintenance:install --database "pgsql" --database-name "nextcloud" --database-user "nextcloud" --database-pass "password" --admin-user "admin" --admin-pass "password"`
 
# Hardening Security
- [Redirect all unencrypted traffic to HTTPS](https://docs.nextcloud.com/server/10/admin_manual/configuration_server/harden_server.html#redirect-all-unencrypted-traffic-to-https)
- Add this snippet to `/etc/apache2/sites-available/000-default.conf`
```
<VirtualHost *:80>
   ServerName cloud.nextcloud.com
   Redirect permanent / https://cloud.nextcloud.com/
</VirtualHost>
```
- [Enable HTTP Strict Transport Security](https://docs.nextcloud.com/server/10/admin_manual/configuration_server/harden_server.html#enable-http-strict-transport-security)
- Add this to `/etc/apache2/sites-available/default-ssl.conf`
```
<VirtualHost *:443>
  ServerName cloud.nextcloud.com
    <IfModule mod_headers.c>
      Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains; preload"
    </IfModule>
</VirtualHost>
```
- Proper SSL configurations
	- Use the [Mozilla SSL Configuration Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to generate a suitable configuration

# Errors in Admin Panel
After logging in to nextcloud, Go to the Admin panel, and check if there are any errors.
- "The "Strict-Transport-Security" HTTP header is not configured to at least "15552000" seconds. For enhanced security we recommend enabling HSTS as described in our [security tips](https://cloud.amreldib.com/nc/index.php/settings/admin/tips-tricks)"
	- This can be resolved by enabling [HTTP Strict transport security](https://docs.nextcloud.com/server/10/admin_manual/configuration_server/harden_server.html#enable-http-strict-transport-security).

# Defining Background Jobs
- In the Admin Panel, choose 'Cron'.
- View current cron jobs for www-data user:
	- `crontab -u www-data -l`
- To add a cron job, use
	- `crontab -u www-data -e`
		- `-u` changes the user
		- `-e` is for edit
	- This opens an editor to add a line at the end of the file
- Add this line to the file
	- `*/15  *  *  *  * php -f /var/www/nextcloud/cron.php`

# Configuring Memory Caching
- [Setting up Redis with PHP7 for ownCloud](https://www.techandme.se/install-redis-cache-on-ubuntu-server-with-php-7-and-owncloud/)
- [Configure memory caching](https://docs.nextcloud.com/server/10/admin_manual/configuration_server/caching_configuration.html)
- Install Redis server
- Check if Redis is working
	- `redis-cli ping`
	- You should get "pong"
- Verify that redis demon is running
	- `ps ax | grep redis`
	- You'll get: 
	- `22203 ? Ssl    0:00 /usr/bin/redis-server 127.0.0.1:6379`
- Install Redis extension for PHP
	- `apt install php-redis`
- Add extension to mods-available
	- `cd /etc/php/mods-available`
	- `vi redis.ini`
	- Add this line: 
		- `'extension=redis.so'`
	- Save and exit
		- :wq
- Enable redis extension for PHP
	- `phpenmod redis`
- Add this configuration to the file `/var/www/nextcloud/config/config.php`
```
'memcache.local' => '\OC\Memcache\Redis',
'redis' => array(
     'host' => 'localhost',
     'port' => 6379,
      ),
'memcache.locking' => '\OC\Memcache\Redis',
```
- Note that connecting over sock isn't working. Needs troubleshooting to figure out why, but the file `'/var/run/redis/redis.sock'` doesn't exist or is at a different location.
- Restart apache
	- `service apache2 restart`


