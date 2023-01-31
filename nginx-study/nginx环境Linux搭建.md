## nginx学习
[nginx学习网址](https://mp.weixin.qq.com/s/z19cHU6H2BSYJPJ8MpJLRA)

### 环境搭建
```shell
#进入home目录
cd /home

#创建文件夹
mkdir /home/software && mkdir /home/software/nginx
cd /home/software/nginx

wget https://nginx.org/download/nginx-1.22.0.tar.gz

tar -xvzf nginx-1.22.0.tar.gz

#下载所需依赖库
yum install --downloadonly --downloaddir=/home/soft/nginx/ gcc-c++
yum install --downloadonly --downloaddir=/home/soft/nginx/ pcre pcre-devel4  
yum install --downloadonly --downloaddir=/home/soft/nginx/ zlib zlib-devel  
#紧接着通过rpm命令依次将依赖包一个个构建：
rpm -ivh --nodeps *.rpm

#或者通过如下指令一键安装所有依赖包：
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel 

#进入解压后的nginx目录，然后执行Nginx的配置脚本，为后续的安装提前配置好环境
./configure --prefix=/usr/local/nginx/

#编译并安装Nginx：
make && make install

#进去软件安装的目录
cd /usr/local/nginx/
#修改安装后生成的conf目录下的nginx.conf配置文件：
vim conf/nginx.conf  
    #修改端口号：listen    80;  
    #修改IP地址：server_name  你当前机器的本地IP(线上配置域名); 
    
#制定配置文件并启动Nginx：
sbin/nginx -c conf/nginx.conf  
ps aux | grep nginx  


#检查配置命令
sbin/nginx -t -c conf/nginx.conf # 检测配置文件是否正常  
sbin/nginx -s reload -c conf/nginx.conf # 修改配置后平滑重启  
sbin/nginx -s quit # 优雅关闭Nginx，会在执行完当前的任务后再退出  
sbin/nginx -s stop # 强制终止Nginx，不管当前是否有任务在执行


#开放80端口，并更新防火墙：

[root@localhost] firewall-cmd --zone=public --add-port=80/tcp --permanent  
[root@localhost] firewall-cmd --reload  
[root@localhost] firewall-cmd --zone=public --list-ports 

```
