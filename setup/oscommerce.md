서버 접속 주소 : 49.247.130.173  
OS : CentOS  

- Apache 설치  
yum -y install httpd    
yum -y install httpd                      !- 아파치 설치  
systemctl enable httpd.service            !- 부팅시 자동시작  
systemctl start httpd                     !- 아파치 서버 시작 
systemctl restart httpd  


- PHP설치  
sudo yum install epel-release  
sudo rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
sudo yum --enablerepo=remi-php73 install php  
--- Module 설치
yum --enablerepo=remi-php73 install php-xml php-soap php-xmlrpc php-mbstring php-json php-gd php-mcrypt  

- Mysql 설치  
sudo rpm -ivh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo yum install mysql-community-server  
--- 기본 chracter-set 이 latin1 이므로 /etc/my.cnf 를 수정해서 utf-8 로 설정한다  
    character-set-server = utf8
    max_allowed_packet = 64M

sudo systemctl start mysqld  
--- 초기패스워드
[loadman@bearscho-57431 etc]$ grep 'password' /var/log/mysqld.log
2019-05-10T12:42:35.987573Z 1 [Note] A temporary password is generated for root@localhost: 47se?NeUwkK#

시스템 부팅시 자동 구동되도록 설정
systemctl enable mysqld
systemctl restart mysqld

mysql -uroot -p

UPDATE user set authentication_string=password('oscommerce') where user='root';
FLUSH PRIVILEGES;

- PHP&Mysql 연동
sudo yum --enablerepo=remi,remi-php56 install php-pdo

yum install php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml





Database Server
Database Server 
localhost
The address of the database server in the form of a hostname or IP address.
Username 
root
The username used to connect to the database server.
Password 
••••••••••
The password that is used together with the username to connect to the database server.
Database Name 
oscommerce
The name of the database to hold the data in.
Table Prefix 
osc_
Prefix all table names in the database with this value.








Online Store Settings
Store Name 
OSCommerce Demo Site(for Test)
The name of the online store that is presented to the public.
Store Owner Name 
JUNGIL CHO
The name of the store owner that is presented to the public.
Store Owner E-Mail Address 
bearscho@gmail.com
The e-mail address of the store owner that is presented to the public.
Administrator Username 
root
The administrator username to use for the administration tool.
Administrator Password 
oscommerce
The password to use for the administrator account.
Time Zone 
The time zone to base the date and time on.