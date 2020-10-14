#**MySql**  
**author: YIGe**  
**date: 2020/10/14 11:22**  

1. windows系统  
    + 启动
        * 切换到bin下目录启动  
            ```shell script
            start mysqld-nt
            ```
        * 安装服务再启动  
            ```shell script
            mysqld-nt --install
            net start mysql
            ```
    + 停止  
        * 切换到bin目录下停止  
            ```shell script
            mysqladmin -u root shutdown
            mysqladmin -u root -p password shutdown
            ```
        * 安装过服务再停止  
            ```shell script
            net stop mysql
            ```
        