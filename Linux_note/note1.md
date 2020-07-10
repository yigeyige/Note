#linux命令

1. 解压缩  
    + 压缩  
        * 示例：将所有jpg打包  
            ```shell script
            tar -czf *.jpg.tar.gz *.jpg
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

3. PID
    + 查看进程所在目录
        ```shell script
        cd /proc/PID号
        sudo ls -ail
        ```
      
4. 操作系统  
    + 4.1 查看操作系统版本  
        ```shell script 
        cat /etc/issue
        cat /etc/redhat-release
        ```
      
    + 4.2 rpm命令(Redhat Package Manager)  
        * 查询操作 rpm -q   
            a 查询所有已经安装的包  
            ```shell script
            rpm -qa | grep mysql
            ```  
            
            i 查询安装包的信息
            ```shell script
            rpm -qip mysql.rpm
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
          
        * 附件命令  
            --force 强制操作，如强制安装卸载删除等  
            --nodeps 忽略依赖关系并继续操作  
            --requires 显示该包的依赖关系                                    
      
5. 软件应用命令  
    + Apache  
        * 查看版本   
            ```shell script
            sudo ./APACHE_BASE/bin/httpd -v
            ```
    
6. 查找命令  
    