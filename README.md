# Deploying WordPress to an Amazon EC2 Instance
## WordPress
WordPress is a web content management system. It was originally created as a tool to publish blogs but has evolved to support publishing other web content, including more traditional websites, mailing lists and Internet forum, media galleries, membership sites, learning management systems and online stores.

## Amazon EC2 Instance
Amazon Elastic Compute Cloud is a part of Amazon.com's cloud-computing platform, Amazon Web Services, that allows users to rent virtual computers on which to run their own computer applications.

### Step 1: Launch and configure an Amazon Linux or Red Hat Enterprise Linux Amazon EC2 instance

1. Sign in into your AWS Console and Click on EC2
2. Navigate to the EC2 Dashboard and Launch Instance

![Choosing the Server Name and Amazon Machine Image (Ubuntu)](./Images/server1.png)

1. Make sure your server is updated
```
sudo apt-get update

```

1. Install Apache server on Ubuntu
``` 
sudo apt install apache2 -y

```

2. Install php runtime and php mysql connector
```
sudo apt install php libapache2-mod-php php-mysql -y

```

3. Install MySQL server
```
sudo apt install mysql-server -y

```

4. Login to MySQL server
```
sudo mysql -u root

```

5. Change authentication plugin to mysql_native_password (change the password to something strong)
```
ALTER USER 'root'@localhost IDENTIFIED WITH mysql_native_password BY 'Ironchest@567.';

```

6. Create a new database user for wordpress (change the password to something strong)
```
CREATE USER 'Promise'@localhost IDENTIFIED BY 'Ironchest@567.';

```

7. Create a database for wordpress
```
CREATE DATABASE wordPress;

```

8. Grant all privilges on the database 'wordPress' to the newly created user
```
GRANT ALL PRIVILEGES ON wordPress.* TO 'Promise'@localhost;

```

9. Download wordpress
```
cd /tmp
wget [Lastest Wordpress version](https://wordpress.org/latest.tar.gz)

```

10. Unzip
```
tar -xvf latest.tar.gz

```

11. Move wordpress folder to apache document root
```
sudo mv wordpress/ /var/www/html

```

12. Command to restart/reload apache server
```
sudo systemctl restart apache2

```
OR
```
sudo systemctl reload apache2

```

13. Sign in the wordpress website using (http://ipaddress/wordpress/)

14. Login using the required credentials like password, username e.t.c

15. To configure the wp-config.php file
```
sudo vim wp-config.php

```
and paste this details

```


```
16. To configure WordPress to be access form the ipaddress rather than the ipaddress/wordpress
```
cd /etc/apache2/sites-available/`
ls
sudo vim 000-default.conf

```

17. Edit the 000-default.conf file
```
DocumentRoot /var/www/html/wordpress

```

18. Reboot apache to adopt new changes
```
sudo systemctl restart apache2

```

16. Install certbot
```
sudo apt-get update
sudo apt install certbot python3-certbot-apache

```


17. Request and install ssl on your site with certbot
```
sudo certbot --apache

```