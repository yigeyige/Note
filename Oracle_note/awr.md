#**AWR 性能监控报表**

1. AWR report  
    
    
2. 性能指标  
    + log file sync  
        等待时间小于20ms算正常
        
    + log file parallel write  
        等待时间小于20ms算正常
        
    log file parallel write和log file sync等待时间很接近，说明就是IO问题，
    因为大部分时间都花在了log写入到磁盘上。