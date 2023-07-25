Mysql 环境搭建

```shell
#查找是否安装过mysql
rpm -qa | grep mysql

#删除mysql相关

# 下载依赖库
cd /usr/local/  
wget https://dev.mysql.com/get/mysql80-community-release-el7-7.noarch.rpm
rpm -Uvh mysql80-community-release-el7-7.noarch.rpm


systemctl start mysqld

systemctl status mysqld 
#查看临时密码
cat /var/log/mysqld.log | grep password

#用临时密码登录页mysql 后修改密码
mysql -u root -p    

alter user 'root'@'localhost' identified by '密码';  # 这里的密码需要符合规则  包含大小写字母 数字 特殊符号 长度大于8
#这里密码   1L..


#修改root用户的host字段为% 允许任何域名访问
update mysql.user set host="%" where user="root";
#刷新配置
flush privileges;

#开放端口号
firewall-cmd --zone=public --add-port=3306/tcp --permanent
#添加端口后刷新防火墙
firewall-cmd --reload








```