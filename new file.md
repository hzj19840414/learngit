Header V3 RSA/SHA256 Signature, key ID fd431d51: NOKEY
rpm --import /etc/pki/rpm-gpg/RPM*



一、cacti 监控软件简介
        1. cacti是用php语言实现的一个软件，它的主要功能是用snmp服务获取数据，然后用rrdtool储存         和更新数据，当用户需要查看数据的时候用rrdtool生成图表呈现给用户。因此，snmp和rrdtool是         cacti的关键。Snmp关系着数据的收集，rrdtool关系着数据存储和图表的生成。
                2. Mysql配合PHP程序存储一些变量数据并对变量数据进行调用，如：主机名、主机ip、snmp   团         体名、端口号、模板信息等变量
                3. snmp抓到数据不是存储在mysql中，而是存在rrdtool生成的rrd文件中（在cacti根目录的rra文           件夹下）。rrdtool对数据的更新和存储就是对rrd文件的处理，rrd文件是大小固定的档案文件                （RoundRobinArchive），它能够存储的数据笔数在创建时就已经定义。

----------------------------------------------------------------------------------------------

rpm -ivh deltarpm-3.5-0.5.20090913git.el6.x86_64.rpm
rpm -ivh python-deltarpm-3.5-0.5.20090913git.el6.x86_64.rpm
rpm -ivh createrepo-0.9.9-18.el6.noarch.rpm 
mkdir /var/pub
cp -R ../Packages /var/pub/


[root@localhost Packages]# createrepo ./
createrepo -g /media/RHEL_6.5\ x86_64\ Disc\ 1/repodata/6221039e7e3dabf7d538c76571d82aaf42b6292b8f6fe6cf56b8fcf1cff3d3ab-comps-rhel6-Server.xml /var/pub/Packages/


cd /etc/yum.repos.d/
cp rhel-source.repo rhel-source.repo.bak


[myyum]
name=local
baseurl=file:///var/pub/Packages/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

yum clean all
yum grouplist
yum list




setenforce 0 
vim /etc/sysconfig/selinux  把selinux=enforcing改为selinux=disabled



iptables --flush
service iptables save




[root@localhost Packages]# yum -y install mysql mysql-server mysql-devel httpd php php-pdo php-snmp php-mysql         lm_sensors net-snmp net-snmp-utils net-snmp-libs rrdtool rrdtool-devel perl-PlRPC                 perl-DBI perl-rrdtool perl-DBD-MySQL
Loaded plugins: product-id, refresh-packagekit, security, subscription-manager
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
Setting up Install Process
Package httpd-2.2.15-29.el6_4.x86_64 already installed and latest version
No package php-snmp available.
Package 1:net-snmp-5.5-49.el6.x86_64 already installed and latest version
Package 1:net-snmp-libs-5.5-49.el6.x86_64 already installed and latest version
No package rrdtool-devel available.
No package perl-PlRPC available.
No package perl-rrdtool available.
Resolving Dependencies
--> Running transaction check
---> Package lm_sensors.x86_64 0:3.1.1-17.el6 will be installed
---> Package mysql.x86_64 0:5.1.71-1.el6 will be installed
---> Package mysql-devel.x86_64 0:5.1.71-1.el6 will be installed
--> Processing Dependency: openssl-devel for package: mysql-devel-5.1.71-1.el6.x86_64
---> Package mysql-server.x86_64 0:5.1.71-1.el6 will be installed
---> Package net-snmp-utils.x86_64 1:5.5-49.el6 will be installed
---> Package perl-DBD-MySQL.x86_64 0:4.013-3.el6 will be installed
---> Package perl-DBI.x86_64 0:1.609-4.el6 will be installed
---> Package php.x86_64 0:5.3.3-26.el6 will be installed
--> Processing Dependency: php-common(x86-64) = 5.3.3-26.el6 for package: php-5.3.3-26.el6.x86_64
--> Processing Dependency: php-cli(x86-64) = 5.3.3-26.el6 for package: php-5.3.3-26.el6.x86_64
---> Package php-mysql.x86_64 0:5.3.3-26.el6 will be installed
---> Package php-pdo.x86_64 0:5.3.3-26.el6 will be installed
---> Package rrdtool.x86_64 0:1.3.8-6.el6 will be installed
--> Processing Dependency: dejavu-lgc-sans-mono-fonts for package: rrdtool-1.3.8-6.el6.x86_64
--> Running transaction check
---> Package dejavu-lgc-sans-mono-fonts.noarch 0:2.30-2.el6 will be installed
---> Package openssl-devel.x86_64 0:1.0.1e-15.el6 will be installed
--> Processing Dependency: zlib-devel for package: openssl-devel-1.0.1e-15.el6.x86_64
--> Processing Dependency: krb5-devel for package: openssl-devel-1.0.1e-15.el6.x86_64
---> Package php-cli.x86_64 0:5.3.3-26.el6 will be installed
---> Package php-common.x86_64 0:5.3.3-26.el6 will be installed
--> Running transaction check
---> Package krb5-devel.x86_64 0:1.10.3-10.el6_4.6 will be installed
--> Processing Dependency: libselinux-devel for package: krb5-devel-1.10.3-10.el6_4.6.x86_64
--> Processing Dependency: libcom_err-devel for package: krb5-devel-1.10.3-10.el6_4.6.x86_64
--> Processing Dependency: keyutils-libs-devel for package: krb5-devel-1.10.3-10.el6_4.6.x86_64
---> Package zlib-devel.x86_64 0:1.2.3-29.el6 will be installed
--> Running transaction check
---> Package keyutils-libs-devel.x86_64 0:1.4-4.el6 will be installed
---> Package libcom_err-devel.x86_64 0:1.41.12-18.el6 will be installed
---> Package libselinux-devel.x86_64 0:2.0.94-5.3.el6_4.1 will be installed
--> Processing Dependency: libsepol-devel >= 2.0.32-1 for package: libselinux-devel-2.0.94-5.3.el6_4.1.x86_64
--> Processing Dependency: pkgconfig(libsepol) for package: libselinux-devel-2.0.94-5.3.el6_4.1.x86_64
--> Running transaction check
---> Package libsepol-devel.x86_64 0:2.0.41-4.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================
 Package                          Arch         Version                     Repository   Size
=============================================================================================
Installing:
 lm_sensors                       x86_64       3.1.1-17.el6                myyum       123 k
 mysql                            x86_64       5.1.71-1.el6                myyum       893 k
 mysql-devel                      x86_64       5.1.71-1.el6                myyum       129 k
 mysql-server                     x86_64       5.1.71-1.el6                myyum       8.6 M
 net-snmp-utils                   x86_64       1:5.5-49.el6                myyum       173 k
 perl-DBD-MySQL                   x86_64       4.013-3.el6                 myyum       134 k
 perl-DBI                         x86_64       1.609-4.el6                 myyum       707 k
 php                              x86_64       5.3.3-26.el6                myyum       1.1 M
 php-mysql                        x86_64       5.3.3-26.el6                myyum        81 k
 php-pdo                          x86_64       5.3.3-26.el6                myyum        75 k
 rrdtool                          x86_64       1.3.8-6.el6                 myyum       294 k
Installing for dependencies:
 dejavu-lgc-sans-mono-fonts       noarch       2.30-2.el6                  myyum       392 k
 keyutils-libs-devel              x86_64       1.4-4.el6                   myyum        28 k
 krb5-devel                       x86_64       1.10.3-10.el6_4.6           myyum       495 k
 libcom_err-devel                 x86_64       1.41.12-18.el6              myyum        32 k
 libselinux-devel                 x86_64       2.0.94-5.3.el6_4.1          myyum       136 k
 libsepol-devel                   x86_64       2.0.41-4.el6                myyum        64 k
 openssl-devel                    x86_64       1.0.1e-15.el6               myyum       1.2 M
 php-cli                          x86_64       5.3.3-26.el6                myyum       2.2 M
 php-common                       x86_64       5.3.3-26.el6                myyum       525 k
 zlib-devel                       x86_64       1.2.3-29.el6                myyum        44 k

Transaction Summary
=============================================================================================
Install      21 Package(s)

Total download size: 17 M
Installed size: 50 M
Downloading Packages:
---------------------------------------------------------------------------------------------
Total                                                         34 MB/s |  17 MB     00:00     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Warning: RPMDB altered outside of yum.
  Installing : php-common-5.3.3-26.el6.x86_64                                           1/21 
  Installing : mysql-5.1.71-1.el6.x86_64                                                2/21 
  Installing : perl-DBI-1.609-4.el6.x86_64                                              3/21 
  Installing : perl-DBD-MySQL-4.013-3.el6.x86_64                                        4/21 
  Installing : php-pdo-5.3.3-26.el6.x86_64                                              5/21 
  Installing : php-cli-5.3.3-26.el6.x86_64                                              6/21 
  Installing : libcom_err-devel-1.41.12-18.el6.x86_64                                   7/21 
  Installing : zlib-devel-1.2.3-29.el6.x86_64                                           8/21 
  Installing : dejavu-lgc-sans-mono-fonts-2.30-2.el6.noarch                             9/21 
  Installing : keyutils-libs-devel-1.4-4.el6.x86_64                                    10/21 
  Installing : libsepol-devel-2.0.41-4.el6.x86_64                                      11/21 
  Installing : libselinux-devel-2.0.94-5.3.el6_4.1.x86_64                              12/21 
  Installing : krb5-devel-1.10.3-10.el6_4.6.x86_64                                     13/21 
  Installing : openssl-devel-1.0.1e-15.el6.x86_64                                      14/21 
  Installing : mysql-devel-5.1.71-1.el6.x86_64                                         15/21 
  Installing : rrdtool-1.3.8-6.el6.x86_64                                              16/21 
  Installing : php-5.3.3-26.el6.x86_64                                                 17/21 
  Installing : php-mysql-5.3.3-26.el6.x86_64                                           18/21 
  Installing : mysql-server-5.1.71-1.el6.x86_64                                        19/21 
  Installing : lm_sensors-3.1.1-17.el6.x86_64                                          20/21 
  Installing : 1:net-snmp-utils-5.5-49.el6.x86_64                                      21/21 
  Verifying  : libsepol-devel-2.0.41-4.el6.x86_64                                       1/21 
  Verifying  : keyutils-libs-devel-1.4-4.el6.x86_64                                     2/21 
  Verifying  : mysql-devel-5.1.71-1.el6.x86_64                                          3/21 
  Verifying  : rrdtool-1.3.8-6.el6.x86_64                                               4/21 
  Verifying  : perl-DBD-MySQL-4.013-3.el6.x86_64                                        5/21 
  Verifying  : openssl-devel-1.0.1e-15.el6.x86_64                                       6/21 
  Verifying  : php-mysql-5.3.3-26.el6.x86_64                                            7/21 
  Verifying  : dejavu-lgc-sans-mono-fonts-2.30-2.el6.noarch                             8/21 
  Verifying  : php-common-5.3.3-26.el6.x86_64                                           9/21 
  Verifying  : perl-DBI-1.609-4.el6.x86_64                                             10/21 
  Verifying  : php-pdo-5.3.3-26.el6.x86_64                                             11/21 
  Verifying  : libselinux-devel-2.0.94-5.3.el6_4.1.x86_64                              12/21 
  Verifying  : 1:net-snmp-utils-5.5-49.el6.x86_64                                      13/21 
  Verifying  : php-cli-5.3.3-26.el6.x86_64                                             14/21 
  Verifying  : zlib-devel-1.2.3-29.el6.x86_64                                          15/21 
  Verifying  : php-5.3.3-26.el6.x86_64                                                 16/21 
  Verifying  : krb5-devel-1.10.3-10.el6_4.6.x86_64                                     17/21 
  Verifying  : lm_sensors-3.1.1-17.el6.x86_64                                          18/21 
  Verifying  : mysql-server-5.1.71-1.el6.x86_64                                        19/21 
  Verifying  : mysql-5.1.71-1.el6.x86_64                                               20/21 
  Verifying  : libcom_err-devel-1.41.12-18.el6.x86_64                                  21/21 

Installed:
  lm_sensors.x86_64 0:3.1.1-17.el6             mysql.x86_64 0:5.1.71-1.el6                  
  mysql-devel.x86_64 0:5.1.71-1.el6            mysql-server.x86_64 0:5.1.71-1.el6           
  net-snmp-utils.x86_64 1:5.5-49.el6           perl-DBD-MySQL.x86_64 0:4.013-3.el6          
  perl-DBI.x86_64 0:1.609-4.el6                php.x86_64 0:5.3.3-26.el6                    
  php-mysql.x86_64 0:5.3.3-26.el6              php-pdo.x86_64 0:5.3.3-26.el6                
  rrdtool.x86_64 0:1.3.8-6.el6                

Dependency Installed:
  dejavu-lgc-sans-mono-fonts.noarch 0:2.30-2.el6   keyutils-libs-devel.x86_64 0:1.4-4.el6    
  krb5-devel.x86_64 0:1.10.3-10.el6_4.6            libcom_err-devel.x86_64 0:1.41.12-18.el6  
  libselinux-devel.x86_64 0:2.0.94-5.3.el6_4.1     libsepol-devel.x86_64 0:2.0.41-4.el6      
  openssl-devel.x86_64 0:1.0.1e-15.el6             php-cli.x86_64 0:5.3.3-26.el6             
  php-common.x86_64 0:5.3.3-26.el6                 zlib-devel.x86_64 0:1.2.3-29.el6          

Complete!




vim /etc/snmp/snmpd.conf

        41行 将 default  改为  127.0.0.1
    
        62行 将systemview 改为 all
    
        85行 将 #view all include .1 80 这一行前面的 # 号去掉



/etc/init.d/mysqld start

/etc/init.d/snmpd start

/etc/init.d/httpd start



wget http://www.cacti.net/downloads/cacti-0.8.8b.tar.gz



[root@localhost ~]# wget http://www.cacti.net/downloads/cacti-0.8.8b.tar.gz
--2016-11-15 16:53:07--  http://www.cacti.net/downloads/cacti-0.8.8b.tar.gz
Resolving www.cacti.net... 140.211.167.231, 173.225.179.10
Connecting to www.cacti.net|140.211.167.231|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2272130 (2.2M) [application/x-gzip]
Saving to: “cacti-0.8.8b.tar.gz”

100%[======================================>] 2,272,130   24.5K/s   in 2m 15s  

2016-11-15 16:55:22 (16.4 KB/s) - “cacti-0.8.8b.tar.gz” saved [2272130/2272130]





tar -zxvf cacti-0.8.8b.tar.gz
mv cacti-0.8.8b /var/www/html/cacti



ls /var/www/html/cacti/
about.php                graphs_new.php              plugins.php
auth_changepassword.php  graphs.php                  poller_commands.php
auth_login.php           graph_templates_inputs.php  poller_export.php
cacti.sql                graph_templates_items.php   poller.php
cdef.php                 graph_templates.php         README
cli                      graph_view.php              resource
cmd.php                  graph_xport.php             rra
color.php                host.php                    rra.php
data_input.php           host_templates.php          scripts
data_queries.php         images                      script_server.php
data_sources.php         include                     script_server.pl
data_templates.php       index.php                   settings.php
docs                     install                     templates_export.php
gprint_presets.php       lib                         templates_import.php
graph_image.php          LICENSE                     tree.php
graph.php                log                         user_admin.php
graph_settings.php       logout.php                  utilities.php
graphs_items.php         plugins



.向数据库导入cacti数据

mysql -uroot -p

create database cacti;

grant all privileges on cacti.* to cacti@localhost identified by 'cacti' with grant option;

use cacti;

source /var/www/html/cacti/cacti.sql;

---------------------------------------------------------------------------------


vim /var/www/html/cacti/include/config.php

useradd cacti
cd /var/www/html/cacti
chown -R cacti rra/ log/

crontab -e

        */1 * * * * php /var/www/html/cacti/poller.php > /dev/null 2>&1








