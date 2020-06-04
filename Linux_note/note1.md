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
        
2. SSH  
    + 查看ssh版本  
        ```shell script
        ssh -V
        ```  
    + 查看ssh加密算法 nmap验证  
        ```shell script
        nmap --script ssh2-enum-algos -sV -p 22 10.0.97.221
        ```

3. PID
    + 查看进程所在目录
        ```shell script
        cd /proc/PID号
        sudo ls -ail
        ```
4. 操作系统  
    + 查看操作系统版本  
        ```shell script 
        cat /etc/issue
        cat /etc/redhat-release
        ```
      
5. 软件应用命令  
    + Apache  
        ```shell script
        sudo ./APACHE_BASE/bin/httpd -v
        ```