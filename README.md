# Vagrant Yii2 (debian/jessie64)

Creates a Vagrant box using debian/jessie64 as base and sets up Yii2 advanced app using ansible as provisioning tool

The following items are currently installed

- Apache 2.4.10
- PHP 5.6.29
- composer 1.3.0 2016-12-24
- Memcached 1.4.21
- MySQL 5.5.53 & Sqlite (sqlite 2.8.17 & sqlite3 3.8.7.1)
- phpMyAdmin (don't boo please)
- Adminer
- Yii Project (advanced)

**Virtualization Related Notes:**
- vCPUs: 2
- vCPUs execution cap: 50%
- Memory: 1024MB
- virtualbox title: yii2/jessie64

**Document root:** /var/www/

**VM Hostname:** lamp.local

**Automatic Host Entries:**
- yii2.local
- admin.yii2.local
- phpmyadmin.yii2.local
- adminer.yii2.local
