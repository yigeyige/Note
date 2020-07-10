#**Git 安装卸载**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. Linux安装卸载  
    + 1.1 安装  
    
    + 1.2 卸载  
        * 找到git位置  
            ```shell script
            which -a git
            ```
        * 进入git目录  
            默认位置：/usr/bin/git  
            ```shell script
            cd /usr/bin/git(这个是一般的默认位置)
            ```
        * 删除git  
            ```shell script
            
            ```
          
    + 1.3 git卸载
        ```shell script
        sudo rpm -evh git --nodeps
        ```