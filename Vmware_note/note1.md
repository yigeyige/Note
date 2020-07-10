#**Vmware虚拟机**  
**author: YIGe**   
**date: 2020/7/10 15:28**  

1. 安装Vmware虚拟机  
    + 1.1 下载安装  
        下载连接：[VM官网](https://www.vmware.com/cn.html)。  
        安装步骤：一直下一步即可。  
    
    + 1.2 可用密钥  
        截止2020-06-03可用：VG5HH-D6E04-0889Y-QXZET-QGUC8  
    
2. 虚拟机环境搭建  
    [VMware虚拟机安装详细教程](https://blog.csdn.net/java_xinshou1/article/details/100010099)
    + 2.1 CentOS7  
        * 配置  
            选择 -> [自定义(高级)](./Image/1-选择配置.png)  
        * 选择虚拟机版本  
            选择 -> [虚拟机版本](./Image/2-选择虚拟机版本.png)  
        * 选择客户机操作系统  
            选择 -> [镜像文件](./Image/3-选择镜像文件.png)  
            &nbsp; &nbsp; &nbsp; &nbsp; -> [虚拟机名称/路径](./Image/4-配置虚拟机名称以及路径.png)  
        * 配置处理机内核数  
            选择 -> [处理器](./Image/5-配置处理器.png)  
        * 配置内存   
            选择 -> [内存](./Image/6-配置内存.png)  
        * 配制网络连接模式 默认NAT模式  
            选择 -> [网络连接](./Image/7-配置网络连接模式.png)  
        * 配制I/O控制器  
            选择 -> [IO控制器](./Image/8-配置IO控制器类型.png)  
        * 配制磁盘   
            选择 -> [磁盘类型](./Image/9-配置磁盘类型.png)  
            &nbsp; &nbsp; &nbsp; &nbsp; -> [选择磁盘](./Image/10-选择磁盘.png)  
            &nbsp; &nbsp; &nbsp; &nbsp; -> [选择容量](./Image/11-指定磁盘容量.png)  
            &nbsp; &nbsp; &nbsp; &nbsp; -> [选择磁盘文件](./Image/12-指定磁盘文件.png)
        * 完成安装虚拟机  
            选择 -> [完成虚拟机安装](./Image/13-完成虚拟机.png)  
        * 选择CentOS  
            选择 -> [CentOS](./Image/14-选择CentOS7.png)  
        * 选择语言  
            选择 -> [语言](./Image/15-选择英文.png)  
        * 选择系统配置  
            选择 -> [系统配置](./Image/16-安装配置.png)  
            &nbsp; &nbsp; &nbsp; &nbsp; ->  [安装图形](./Image/17-选择安装图形.png)  
        * 选择磁盘分区  
            选择 -> [磁盘分区](./Image/18-选择磁盘分区.png)  
        * 开始安装及配置密码  
            选择 -> [安装及配置密码](./Image/19-开始安装以及配置密码.png)    
        * 选择同意协议    
            选择 -> [同意协议](./Image/20-同意协议.png)    
        * 打开有线连接  
            选择 -> [有线连接](./Image/21-打开有线连接.png)  
            
3. 虚拟机固定IP  
    [Vmware虚拟机网络配置(固定IP) - 简书](https://www.jianshu.com/p/6fdbba039d79)  
    + 3.1  NAT模式固定IP
    
4. Vmware快捷键  
    + 命令行/图形界面切换  
        图形到命令行：Ctrl + Alt + F2  
        命令行到图形：
        ```shell script
        startx
        ```
    + 虚拟机系统与真实主机切换  
        Ctrl + Alt