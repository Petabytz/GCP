# Wordpress Website Database Migration from AWS to GCP

## Prerequisites

* Wordpress is required in both AWS Ec2 instance and GCP Compute Engine instance.

* We installed in both using shell script 

```bash 
#!/bin/bash
yum update -y
yum upgrade -y
yum install wget zip unzip -y
yum install httpd -y
yum groupinstall Mariadb Mariadb-client -y
yum install php -y
systemctl restart httpd
systemctl enable httpd
wget https://wordpress.org/latest.zip
unzip -d /var/www/html/ latest.zip
mv /var/www/html/wordpress/* /var/www/html/
restorecon -Rv /var/www/

mysql -u root <<MYSQL_SCRIPT
CREATE DATABASE wordpress;
CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wordpress123';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'localhost';
FLUSH PRIVILEGES;
MYSQL_SCRIPT

systemctl restart mariadb
systemctl enable mariadb
firewall-cmd --permanent --add-service={http,https}
fireall-cmd --reload
```

### Note : This is script for Redhat 7 os instance. If you are using different os then you have to modify accourding to that in this file.


