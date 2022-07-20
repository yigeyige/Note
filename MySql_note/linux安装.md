#**MySql**  
**author: YIGe**  
**date: 2022/07/20 23:02**  

1. Linux  
    + 安装
        * 1. 解压 增加data文件夹 
            ```shell script
            cd /app/soft/mysql
            tar -xvf mysql-8.0.29-linux-glibc2.12-x86_64.tar.xz
            mkdir data
            ```  
        * 2. 增加用户  
            ```shell script
            groupadd mysql
            useradd -r -g mysql mysql
            ```  
        * 3. 切换目录权限  
            ```shell script
             chown -R mysql:mysql /app/soft/mysql
             ``` 
        * 4. 初始化mysql  =o+=X_apr3S+
            初始化的时候设置 lower_case_table_names=1才有效
            ```shell script
            cd /app/soft/mysql/bin/
            ./mysqld --user=mysql --basedir=/app/soft/mysql --datadir=/app/soft/mysql/data --lower_case_table_names=1 --initialize
            ```  
        * 5. 添加mysql自动启动  
            ```shell script
            cd /app/soft/mysql
            cp -a ./support-files/mysql.server /etc/init.d/mysql
            chmod +x /etc/init.d/mysql
            chkconfig --add mysql
            ```  
        * 6. 添加my.cnf  
            [参数配置](./File/my.cnf) 
        * 7. 修改root密码  
            ```shell script
            ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'wasd1234';
            ```