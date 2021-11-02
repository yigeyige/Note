#**Linux命令**   
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 解压缩  
    + 压缩  
        * 示例：将所有jpg打gz包  
            ```shell script
            tar -czf *.jpg.tar.gz *.jpg
            tar -czf foo.tar.gz --exclude=.git foo
            tar -czf /tmp/tomcat_bpm_7001.tar.gz --exclude=tomcat_bpm_7001/logs tomcat_bpm_7001
            ```  
        * 示例：将所有jpg打tar包  
            ```shell script
            tar -cf *.jpg.tar *.jpg
            ```
    + 解压  
        * 示例1：解压tar包  
            ```shell script
            tar -xvf file.tar
            ```
        * 示例2：解压tar.gz包  
            ```shell script
            tar -xzvf file.tar.gz
            ```
        * 示例3：解压zip包  
            ```shell script
            unzip file.zip
            ```
        
2. SSH/SSL  
    + 查看ssh版本  
        ```shell script
        ssh -V
        ```  
    + 查看ssh加密算法 nmap验证  
        ```shell script
        nmap --script ssh2-enum-algos -sV -p 22 10.0.97.221
        ```
    + 查看ssl版本  
        * CentOS查看  
            ```shell script
            openssl version
            ```
     
3. 操作系统  
    + 3.1 查看操作系统版本  
        ```shell script 
        cat /etc/issue
        cat /etc/redhat-release
        ```  
    + 3.2 查看linux内核信息  
        ```shell script
        cat /proc/version
        uname -a
        ```
    + 3.3 rpm命令(Redhat Package Manager)  
        * 查询操作 rpm -q   
            a 查询所有已经安装的包  
            ```shell script
            rpm -qa | grep mysql
            yum list libsmbclient*
            ```   
            i 查询安装包的信息
            ```shell script
            rpm -qip mysql.rpm
            rpm -qa git;rpm -qa perl-Git;echo $(date +%F);hostname -I
            ```  
            l 显示安装包文件被安装的到哪些目录下  
            s 显示安装包中的所有文件状态被安装的到哪些目录下   
            p 查询的是安装包的信息   
            f 查询的是已安装的某文件信息   
        * 安装操作 rpm -i  
            安装包  
            ```shell script
            rpm -i mysql.rpm
            ```  
            安装包并显示正在安装的文件信息  
            ```shell script
            rpm -iv mysql.rpm
            ```   
            安装包并显示正在安装的文件信息以及安装进度  
            ```shell script
            rpm -ivh mysql.rpm
            ```   
        * 卸载操作 rpm -e  
            卸载软件包  
            ```shell script
            rpm -e mysql
            ```   
            卸载软件包并显示卸载的文件信息以及卸载进度  
            ```shell script
            rpm -evh mysql
            sudo rpm -ev --nodeps perl-Git-1.8.3.1-6.el7_2.1.noarch
            ```    
        * 升级操作 rpm -U  
            升级包  
            ```shell script
            rpm -U mysql.rpm
            ```   
            升级包并显示升级的文件信息以及升级进度  
            ```shell script
            rpm -Uvh mysql.rpm
            ```    
        * 验证操作 rpm -V  
            验证软件包是通过比较已安装的文件和软件包中的原始文件信息来进行的。  
            验证主要是比较文件的尺寸，MD5 校验码，文件权限，类型，属主和用户组等。  
            如果有错误信息输出，您应当认真加以考虑，是通过删除还是重新安装来解决出现的问题。   
            验证包  
            ```shell script
            rpm -V mysql.rpm
            ```   
            示例：
            ```shell script  
            rpm -Vf /app/apache/conf/apache.conf
            ```  
            输出：其中S表示文件大小被修改过，T表示文件日期被修改过    
            ```shell script  
            S.5....T c /app/apache/conf/apache.conf
            ```    
        * 附命令  
            --force 强制操作，如强制安装卸载删除等  
            --nodeps 忽略依赖关系并继续操作  
            --requires 显示该包的依赖关系    
    + 3.4 root创建用户  
        ```shell script
        useradd -d /usr/prod -m prod 
        passwd prod 
      
        groupsadd prodGroup 
        usermod -a -G prodGroup prod
        ```      
    + 3.5 重新加载系统配置文件  
        ```shell script
        source /etc/profile
        ```     
    + 3.6 修改密码  
        ```shell script
        passwd
        ```   
    + 3.7 查看文件打开数
        ```shell script
        ulimit -a
        ```    
    + 3.8 hosts配置
        配置host  
        ```shell script
        vim /etc/hosts
        ```
        重启host  
        ```shell script
        /etc/init.d/network restart
        ```  
    + 3.9 sysctl配置（比如TCP配置）   
        优化配置TCP   
        ```shell script
        cat /etc/sysctl.conf
        ```
        
        重启系统配置（可不重启系统）  
        ```shell script
        /sbin/sysctl -p
        ```
    + 3.10 dns配置  
        ```shell script
        cat /etc/resolv.conf
        ```
    + 3.11 用户环境变量  
        * 对当前用户有效，且永久 (可能会不生效)    
            ```shell script
            vim .bash_profile
            source .bash_profile
            ```
        * root用户下执行(生效)   
            ```shell script
            vi ~/.bash_profile
            source ~/.bash_profile
            ```
        * 对所有用户有效，且永久 
            ```shell script
            vim /etc/profile
            source /etc/profile
            ```
        * 只对本次shell有效，且临时  
            ```shell script
            export HOME=/a/a/a/a
            ```  
        
5. 软件应用命令  
    + Apache  
        * 查看版本   
            ```shell script
            sudo ./APACHE_BASE/bin/httpd -v
            ``` 
    + Git  
        * 查看版本  
            ```shell script
            
            ```
    
6. top命令  
    [TOP命令各参数详解](https://www.cnblogs.com/sbaicl/articles/2752068.html)  
    CPU:  
    us 用户空间占用CPU百分比  
    sy 内核空间占用CPU百分比  
    ni 用户进程空间改变过优先级的进程占用CPU百分比  
    id 空闲CPU百分比  
    wa 等待输入输出的CPU时间百分比    
    hi CPU服务硬中断的时间百分比  
    si CPU服务软中断的时间百分比  
    
7. 切换文件所有者  
    + 将当前目录名下title文件夹极其子文件的所有者改为guest组下的dev用户
        ```shell script
        chown -R su.guest title
        ```  
    + root创建title文件 切换给其他用户用户组  
        ```shell script
        chown prod title
        chgrp prodGroup title
      
        chown appuser:appgrp access_log
        ```
   
8. 查看命令  
    + 查看文件或者目录大小  
        ```shell script
        ls -lht
        df -h
        du -h --max-depth=1 /home/prod/web   
        du -sh /home/prod/web
        du --max-depth=2 / | sort -rn | head
        ```  
    + 查看服务器打开文件数量以及其他数据  
        ```shell script
        ulimit -a
        ```   
    + 查看线程数  
        * 查看某进程的线程数  
            ```shell script
            ps -Lf pid|wc -l 
            ```       
        * 查看某进程数   
            ```shell script
            ps -eLf|grep java|wc -l
            ```   
    + 查看网络连接  
        * 查看网络连接状态以及数量  
            需要拥有netstat命令权限
            ```shell script
            netstat -an | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
            ```  
        * 查看网络已连接数量  
            ```shell script
            netstat -nat|grep ESTABLISHED|wc -l
            netstat -nat
            ```
        * 查看端口  
            * 查看所有3306端口使用情况  
                ```shell script
                netstat -an | grep 3306
                ```
            * 查看端口对应进程  
                ```shell script
                netstat -tunlp | grep 8080
                ``` 
            * 查看所有80端口使用情况  
                ```shell script
                netstat -nlp |grep 80
                ```  
            * 查看当前所有监听端口  
                ```shell script
                netstat -nlp |grep LISTEN
                ```
        * 查看实时网速  
            ```shell script
            sar -n DEV 1 100
            ```
    + 查看进程所在目录  
        ```shell script
        cd /proc/PID号
        sudo ls -ail
        ```     
    + 查看进程pid对应服务目录  
        ```shell script
        pwdx 7226
        ```   
    + 查看物理CPU个数   | wc -l（即为统计数量）
        ```shell script
        cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l
        ```  
    + 查看每个物理CPU中core的个数(即核数) 主要使用这个  
        ```shell script
        cat /proc/cpuinfo| grep "cpu cores"| uniq
        ```  
    + 查看逻辑CPU个数  
        ```shell script
        cat /proc/cpuinfo| grep "processor"| wc -l
        ``` 
    + 查看文件最多的目录
        ```shell script
        for i in /*; do echo $i; find $i | wc -l; done
        ```   
    + 查看逻辑卷组信息  
        ```shell script
        sudo vgs
        sudo lvs
        sudo pvs
        ```
9. 普通用户切换到root  
    ```shell script
    su root
   
    sudo su
   
    sudo sh
    > bash
    ```    
   
10. cron服务 类似计划任务  
    + 执行命令   
        要把cron设为在开机的时候自动启动，在 /etc/rc.d/rc.local 脚本中加入 /sbin/service crond start 即可.  
        ```shell script
        /sbin/service crond start
        /sbin/service crond stop
        /sbin/service crond restart
        /sbin/service crond reload
        ```   
    + crontab配置  
         * 查看当前用户的crontab  
            ```shell script
            crontab -l
            ```
         * 编辑crontab  
            ```shell script
            crontab -e
            ```  
         * 删除crontab  
            ```shell script
            crontab -r
            ```  
         * 查看crontab运行状态  
            ```shell script
            service crond status
            ```
           
11. 复制命令  
    + 去除特定文件的复制  
        ```shell script
        cd /user/web
        cp -R 'ls|grep -v *.log | xargs' /tmp/web
      
        ls /tmp/test/ |grep -v .gz |xargs -i cp -r /tmp/test/{} /tmp/test_cp
      
        rsync -av --progress sourcefolder /destinationfolder --exclude thefoldertoexclude
        ```
        
        
12. 网络命令  
    + 端口查看以及监听  
        ```shell script  
        netstat -nlp |grep LISTEN   //查看当前所有监听端口
        netstat -an | grep 6379
        ```  
      
13. java日志分析命令  
    ```shell script
    /app/soft/jdk1.8.0_211/bin/jstack -l 15429  | tee -a /tmp/15429_jstack.log
    /app/soft/jdk1.8.0_211/bin/jmap -dump:live,format=b,file=/tmp/15429.hprof 15429
    ```
    
14. 查看jar/zip中的文件  
    [Linux查看jar包中的文件](./File/Linux查看jar中的文件.png)  
    [Linux查看jar包中的文件](https://blog.csdn.net/weixin_41344042/article/details/80278433?utm_source=blogxgwz1)
    ```shell script
    vim axis-1.0.jar
    /server-config.wsdd
    ```
    
15. 查找文件  
    ```shell script
    find / -name rabbitmq.config
    #查找当前目录制定时间内的文件 并打包
    find ./ -newermt '2021-06-03 10:58' ! -newermt '2021-06-03 11:01' -exec tar -czf aa.tar.gz {} \;
    find ./ -newermt '2020-07-13 09:38' ! -newermt '2020-07-13 10:32' -exec cp {} /tmp/yige1  \;
    ```
    + find -exec 命令解释  
        {}是花括号代表前面find查找出来的文件名，对于某些版本的find,{}对于shell来说有特殊含义，
        所以在前面加\或者引号对他进行转义,\本身对{\}就进行了转义，实际上\{\}这种用法是不妥的,应该使用用\{},或者用引号引起来。
    
    + atime,mtime,ctime就是分别对应的“最近一次访问时间”“最近一次内容修改时间”“最近一次属性修改时间”
      这里的atime的单位指的是“天”，amin的单位是分钟  
        ```shell script
        #表示查找在一天内没有访问过的文件
        find /app/tomcat_web_7092/logs -mtime +1 -name
        #表示查找在一天内访问过的文件
        find /app/tomcat_web_7092/logs -mtime -1 -name
        ```
    
    + 统计当前目录文件数量  
        * 不包括目录 
            ```shell script
            ls -l | grep "^-" | wc -l
            ```
        * 包括子目录  
            ```shell script
            ls -lR| grep "^-" | wc -l
            ```
        
    
16. 查看服务  
    + 查看服务进程ID 并关闭   
        ```shell script
        ps aux | grep snmp | grep -v grep | awk '{print $2}' | xargs kill
        ```
    