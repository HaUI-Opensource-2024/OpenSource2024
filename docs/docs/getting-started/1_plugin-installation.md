# === Plugin Installation ===

## Prerequisites
To install the Hagen plugin, you can follow one of two methods: **Manual Installation** or **Docker Compose Installation**.
To use this plugin, 

## Method 1: Manual Installation
1. **Install WordPress**  
   - Download the latest version of WordPress from the [official WordPress website](https://wordpress.org/download/).  
   - Follow the WordPress installation instructions to set up your website.  
   - Or you can use script above to install wordpress for ubuntu or centos.
## ubuntu 
```bash
apt install apache2 -y 
apt install mysql-server -y 
mysql_secure_installation
apt install php libapache2-mod-php php-mysql -y

systemctl status apache2.service 

mysql 
CREATE DATABASE wordpress;
CREATE USER 'test'@'localhost' IDENTIFIED BY 'test1234';
GRANT ALL PRIVILEGES ON wordpress.* TO 'test'@'localhost';
FLUSH PRIVILEGES;
EXIT;

curl -LO https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz

cp wordpress/wp-config-sample.php wordpress/wp-config.php

nano wordpress/wp-config.php # Chỉnh sửa thông tin database

rsync -avP wordpress/ /var/www/html/
chown -R www-data:www-data /var/www/html/
chmod -R 755 /var/www/html/
rm /var/www/html/index.html
```

## Centos  
```bash
# Cài đặt Apache (httpd trên CentOS)
yum install httpd -y 

# Cài đặt MariaDB (thay thế MySQL trên CentOS)
yum install mariadb-server -y 

# Khởi chạy MariaDB và chạy cấu hình bảo mật
systemctl start mariadb
systemctl enable mariadb
mysql_secure_installation

# Cài đặt PHP và các gói cần thiết
yum install epel-release -y
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
yum install yum-utils -y
yum-config-manager --enable remi-php74
yum update -y
yum install php php-cli php-common php-fpm php-mysqlnd php-json php-xml php-mbstring php-gd php-curl -y
php -v

# Khởi động Apache và kiểm tra trạng thái dịch vụ
systemctl start httpd
systemctl enable httpd
systemctl status httpd.service 

# Đăng nhập MariaDB và cấu hình cơ sở dữ liệu cho WordPress
mysql 
CREATE DATABASE wordpress;
CREATE USER 'test'@'localhost' IDENTIFIED BY 'test1234';
GRANT ALL PRIVILEGES ON wordpress.* TO 'test'@'localhost';
FLUSH PRIVILEGES;
EXIT;

# Tải và giải nén WordPress
curl -LO https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz

# Cấu hình file wp-config.php cho WordPress
cp wordpress/wp-config-sample.php wordpress/wp-config.php
nano wordpress/wp-config.php # Chỉnh sửa thông tin cơ sở dữ liệu tại đây

# Di chuyển WordPress vào thư mục Apache và thay đổi quyền
rsync -avP wordpress/ /var/www/html/
chown -R apache:apache /var/www/html/
chmod -R 755 /var/www/html/
rm /var/www/html/index.html

# Khởi động lại dịch vụ Apache và PHP-FPM
systemctl restart httpd
systemctl restart php-fpm
```

2. **Install the Plugin**  
   - Place the plugin folder into the `/wp-content/plugins/` directory of your WordPress installation.  
   - Navigate to the WordPress dashboard and go to the **Plugins** section.  
   - Activate the plugin from the list of installed plugins.

## Method 2: Installation via Docker Compose

1. **Set Up Docker Compose**  
   - Install Docker and Docker Compose on your system.  

2. **Run a `docker-compose.yml` File**  
```bash
docker-compose up -d
```
3. Activate the Plugin

    - Access your WordPress dashboard at http://localhost:8080 (or your chosen port).
    - Navigate to the Plugins section and activate the plugin.
    - And your plugin are being installed successfully.