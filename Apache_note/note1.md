#**Apache**

**注：以下均为apache2.4及以上版本**

1. Linux安装apache  
    +  安装资源列表  
        + httpd-2.4.41.tar.gz
        + apr-1.6.5.tar.gz
        + apr-util-1.6.1.tar.gz
        + expat-2.1.0-10.el7_3.x86_64.rpm
        + expat-devel-2.1.0-10.el7_3.x86_64.rpm  
    +  安装软件步骤  
        1. 若服务器无expat依赖包，执行rpm安装expat相关依赖
            > *不分析包依赖关系安装* --nodeps --force 
            ```shell命令
            rpm -iv *.rpm --nodeps --force
            ```
        2. 执行安装步骤   
            ```shell命令
            tar -zxvf httpd-2.4.41.tar.gz
            tar -zxvf apr-1.6.5.tar.gz
            tar -zxvf apr-util-1.6.1.tar.gz
            mv apr-1.6.5 /APACHE_HOME/srclib/apr
            mv apr-util-1.6.1 /APACHE_HOME/srclib/apr-util
            ./configure -prefix=/APACHE_HOME --with-included-apr --enable-so --enable-ssl --enable-deflate=shared --enable-expires=shared --enable-rewrite=shared --enable-static-support --disable-userdir --enable-proxy=shared --enable-proxy-http=shared --enable-proxy-ftp=shared --enable-proxy-connect=shared
            make
            make install
            ```  
        3. 最后完成启动  
            ```shell命令
            sudo ./httpd -k start
            ```  

2. apache处理模式  
    + prefork MPM  
        特点：单线程进程。<br/>
        在一个时间点只能处理一个连接，需要启动大量的进程来处理高并发的请求。<br/>
        由于是单线程进程，因而无须考虑线程安全的问题，可以使用非线程安全的库，例如mod_php。<br/>
        优点是成熟稳定，缺点是比较消耗内存，而且并发支持受限于进程数量，对高并发支持稍差。
    + worker MPM  
        特点：多线程进程。<br/>
        worker同样使用多个进程，但每个进程又拥有多个线程，每个线程处理一个连接。<br/>
        由于线程是轻量级的，因而具有较高的并发性，同时，多个进程又获得了一定的稳定性。
        worker模式特点是占用内存少，并发性比较高，缺点是必须考虑线程安全。<br/>
        如果使用了keep-alive方式，一个线程可能会被一直保持一个连接，但中间没有请求，直到超时。<br/>
        如果有多个线程被这样占据，在高并发场景下同样会出现无线程可用的情形。
    + event MPM  
        特点：worker模式的优化版。<br/>
        event模式是在2.4版本中才稳定发布的模式，它在worker的基础上，<br/>
        解决了keep-alive连接不能释放的问题。event MPM中，<br/>
        会有一个专门的线程来管理这些keep-alive类型的线程，当有真实请求过来的时候，<br/>
        将请求传递给服务线程，执行完毕后，又允许它释放。这样增强了高并发场景下的请求处理能力。

3. 参数配置以及调优  
    + prefork MPM  
        StartServers : apache启动时初始化的服务子进程数量。<br/>
        MinSpareServers：最小空闲进程数量，空闲进程指的是没有处理请求的进程。<br/>
        MaxSpareServers : 最大空闲进程数量。<br/>
        ServerLimit: 最大派生的进程数(MaxRequestWorkers的上限值，最大不能超过这个值可以等于)。<br/>
        MaxRequestWorkers : 最大处理请求的线程数量，也是最大的同时连接数，表示了apache的最大请求并发能力，
        超过该数目后的请求，将排队。<br/>
        MaxConnectionsPerChild : 进程生命周期内，每个进程处理的最大请求数。达到该数值后，进程将被杀死。
        如果设置为0，表示没有限制。该参数的意义在于，避免了可能存在的内存泄露带来的系统问题。 
        ```
        <IfModule mpm_prefork_module>
            StartServers         10         # 启动时进程数
            MinSpareServers      5          # 最小空闲进程数 
            MaxSpareServers      10         # 最大空闲进程数
            MaxRequestWorkers    100        # 最大并发进程数
            MaxConnectionsPerChild   10000  # 最大连接数限制
        </IfModule> 
        ```
        项目配置示例：  
        ```
        StartServers              30
        MinSpareServers           30
        MaxSpareServers           75 
        MaxRequestWorkers       2000
        MaxConnectionsPerChild   100
        ```   
    + worker MPM  
        StartServers: apache启动时初始化的服务子进程数量。<br/>
        MinSpareThreads: 最小空闲线程数。<br/>
        MaxSpareThreads: 最大空闲线程数。<br/>
        ServerLimit: 指定最大请求子进程数，默认是16。<br/>
        ThreadLimit: 每个进程可以启动的线程数量上限值。<br/>
        ThreadsPerChild: 每个进程可以启动的线程数量。<br/>
        MaxRequestWorkers: 最大处理请求的线程数量，也是最大的同时连接数，表示了apache的最大请求并发能力，
        超过该数目后的请求，将排队。<br/>
        MaxConnectionsPerChild: 进程生命周期内，每个进程处理的最大请求数。达到该数值后，进程将被杀死。
        如果设置为0，表示没有限制。该参数的意义在于，避免了可能存在的内存泄露带来的系统问题。<br/> 
        ServerLimit默认是16，必要时可以显式声明加大这个值,MaxRequestWorkers必须是ThreadsPerChild的整数倍, 
        MaxRequestWorkers <= ServerLimit * ThreadsPerChild。<br/>  
        ```
        <IfModule mpm_worker_module>
            StartServers         2        # 启动时进程数
            MinSpareThreads      25       # 最小空闲线程数
            MaxSpareThreads      75       # 最大空闲线程数
            ThreadLimit          64       # 每个进程可以启动的线程数量上限值
            ThreadsPerChild      25       # 每个进程可以启动的线程数量
            MaxRequestWorkers    400      # 线程数量最大值
            MaxConnectionsPerChild   0    # 最大连接数限制
        </IfModule> 
        ```
    + event MPM  
        event模式下的参数意义和worker模式完全一样，按照上面的策略来调整即可。 
        event相比于worker的优势是，它解决了worker模式下长连接线程的阻塞问题。 
        值得一提的是，worker/event模式的请求处理模式，已经和nginx的libevent模式相同了。<br/>
        项目配置示例：  
        ```
        StartServers             3
        MinSpareThreads         75
        MaxSpareThreads        250
        ServerLimit			   100
        ThreadsPerChild         25
        MaxRequestWorkers     2000
        MaxConnectionsPerChild 100
        ```