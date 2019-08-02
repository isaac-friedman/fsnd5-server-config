# fsnd5-server-config
This is the final project in Udacity's Fullstack Nanodegree. The project is an Amazon Lightsail  
Server that will host the Tool Trackr app I completed in a previous project.

## Location
* IP: 3.221.183.77  
* URL: http://3.221.183.77.xip.io/
* ssh port: 2200

## Software Installed
* Python 2.7
* pip
* Apache2 web server
* PostgresSQL -- app uses SQLlite3 but the project requires installing Postgres so I did it.

## Configuration Log
* Run updates after building instance  
* Add user "grader"
* Configured firewall with the following rules:
```  
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
2200/tcp                   ALLOW       Anywhere
80/tcp                     ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
2200/tcp (v6)              ALLOW       Anywhere (v6)
80/tcp (v6)                ALLOW       Anywhere (v6)

```
* Disable all vhosts
* Configure vhost for my app as follows:
```
<VirtualHost *:80>
 ServerName 3.221.183.77.xip.io
 WSGIDaemonProcess app user=ubuntu group=ubuntu threads=5
 WSGIScriptAlias / /var/www/tool-trackr/app.wsgi
<Directory /var/www/tool-trackr/>
 Order allow,deny
 Allow from all
 WSGIPassAuthorization On
 WSGIProcessGroup app
 WSGIApplicationGroup %{GLOBAL}
 WSGIScriptReloading On
 Require all granted
</Directory>

Alias /static /var/www/tool-trackr/static
<Directory /var/www/tool-trackr/static/>
        Order allow,deny
        Allow from all
</Directory>
 ErrorLog ${APACHE_LOG_DIR}/error.log
 LogLevel warn
 CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
* Enable new virtual host `sudo a2ensite tool-trackr.conf`


## References
* Tero Karvinen's [minimal WSGI tutorial](http://terokarvinen.com/2016/deploy-flask-python3-on-apache2-ubuntu) for the virtual host  
* [Apache2 documentation](https://httpd.apache.org/docs/2.4/vhosts/) (obviously)

## ToDos


## Authors
Isaac Friedman

## Acknowledgments
