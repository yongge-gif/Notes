导入项目                   cd /mnt/项目目录  (注意: 最开头的C盘D盘用小写)
复制项目到windows
# Gunicorn
安装                         pip install gunicorn
进入项目目录                  cd 项目名称
启动                         gunicorn -w 4 -b 127.0.0.1:5000 day13.app:app
停止                         Ctrl+C

# Nginx
安装                         sudo apt update
                             sudo apt install nginx
启动                         sudo service nginx start
配置                         sudo nano /etc/nginx/sites-available/default
    保存配置文件信息           Ctrl+O
                             Enter
    退出配置                  Ctrl+X
快速定位问题                  nginx -t
重启                         sudo service nginx restart

# mysql
安装                         sudo apt install mysql-server
启动                         sudo service mysql start
停止                         sudo service mysql stop
进入                         mysql -u root -p
    取消当前未完成的 SQL       \c
    退出                     exit
重启                         sudo service mysql restart
查socket                     mysqladmin -u root -p variables | grep socket

# 静态资源测试                cd /var/www/html
                            sudo nano index.html

# 修改默认页面                sudo nano /var/www/html/index.nginx-debian.html


# 容器
运行容器                    docker compose up -d (容器所在目录执行)