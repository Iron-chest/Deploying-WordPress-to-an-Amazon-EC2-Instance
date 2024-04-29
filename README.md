# Deploying WordPress to an Amazon EC2 Instance
## WordPress
WordPress is a web content management system. It was originally created as a tool to publish blogs but has evolved to support publishing other web content, including more traditional websites, mailing lists and Internet forum, media galleries, membership sites, learning management systems and online stores.

## Amazon EC2 Instance
Amazon Elastic Compute Cloud is a part of Amazon.com's cloud-computing platform, Amazon Web Services, that allows users to rent virtual computers on which to run their own computer applications.

### Step 1: Launch and configure an Amazon Linux or Red Hat Enterprise Linux Amazon EC2 instance

a. Sign in into your AWS Console and Click on EC2
b. Navigate to the EC2 Dashboard and Launch Instance
c. Choose the Server Name.
![Choosing the Server Name](./Images/server1.png)

d. Choose the Amazon Machine Image.
![Choosing the Amazon Machine Image](./Images/server2.png)

e. Choose the Instance type and KeyPair
![Choosing the Amazon Machine Image](./Images/server3.png)

f. Configure the Network Settings
![Choosing the Amazon Machine Image](./Images/server4.png)

g. Configure Storage for the EC2 Instance
![Choosing the Amazon Machine Image](./Images/server5.png)

h. Then, Click on Launch Instance and the server should be running.
![Choosing the Amazon Machine Image](./Images/server6.png)

### Step 2: Connecting to the EC2 Instance
a. Click on your Public IPv4 address
b. I would be using a ssh-client called Mobaxterm to access my EC2 Instance
[Download Mobaxterm](https://mobaxterm.mobatek.net/download.html)

c. Login your EC2 Instance using:
- Ip Address
- Private Key (.pem)
- Server Name (Ubuntu)

### Step 3: Download Apache, PHP, MySQL.
1. Make sure your server is updated
```
sudo apt-get update

```

2. Install Apache server on Ubuntu
``` 
sudo apt install apache2 -y

```

3. Install php runtime and php mysql connector
```
sudo apt install php libapache2-mod-php php-mysql -y

```

4. Install MySQL server
```
sudo apt install mysql-server -y

```
### Step 4: Creating and Configuring MySQL Database
5. Login to MySQL server
```
sudo mysql -u root

```

6. Change authentication plugin to mysql_native_password (change the password to something strong)
```
ALTER USER 'root'@localhost IDENTIFIED WITH mysql_native_password BY 'Ironchest@567.';

```

7. Create a new database user for wordpress (change the password to something strong)
```
CREATE USER 'Promise'@localhost IDENTIFIED BY 'Ironchest@567.';

```

8. Create a database for wordpress
```
CREATE DATABASE wordPress;

```

9. Grant all privilges on the database 'wordPress' to the newly created user
```
GRANT ALL PRIVILEGES ON wordPress.* TO 'Promise'@localhost;

```
### Step 5: Download WordPress and configure it 
10. Download Wordpress
```
cd /tmp
wget [Lastest Wordpress version](https://wordpress.org/latest.tar.gz)

```

11. Unzip
```
tar -xvf latest.tar.gz

```

12. Move wordpress folder to apache document root
```
sudo mv wordpress/ /var/www/html

```

13. Command to restart/reload apache server
```
sudo systemctl restart apache2

```
OR
```
sudo systemctl reload apache2

```

14. Sign in the wordpress website using (http://ipaddress/wordpress/)

15. Login using the required credentials like password, username e.t.c

16. To configure the wp-config.php file
```
sudo vim wp-config.php

```
and paste this details

```


```
17. To configure WordPress to be access form the ipaddress rather than the ipaddress/wordpress
```
cd /etc/apache2/sites-available/`
ls
sudo vim 000-default.conf

```

18. Edit the 000-default.conf file
```
DocumentRoot /var/www/html/wordpress

```

#### 18. Reboot apache to adopt new changes
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