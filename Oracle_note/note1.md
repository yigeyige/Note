#**Oracle**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 查询锁表语句  
    + 简洁锁表查询  
        ```sql
        select *
          from v$locked_object aa,
               all_objects     oo
         where aa.object_id = oo.object_id;
        ```
    + 查询锁，生成解锁语句  
        ```sql  
        select lo.*,
               lo.locked_mode,
               lo.session_id,
               vss.serial#,
               vps.spid,
               vss.action action,
               vss.osuser osuser,
               vss.process ap_pid,
               vps.spid db_pid,
               'alter system kill session ' || '''' || lo.session_id || ',' ||
               vss.serial# || ''';' kill_command
          from v$locked_object lo, 
               all_objects     aa,
               v$session       vss,
               v$process       vps
         where lo.session_id = vss.sid
           and aa.object_id = lo.object_id
           and vss.paddr = vps.addr
         order by 2,
                  3;
        ```
      
2. with as 用法  
    如果在package中使用 可能会存在问题，因为其相当于是产生一个临时表  
    
3. delete问题  
    delete和insert中断都有回滚事务的。
    TRUNCATE TABLE TableName 
    1、删除表全部内容，但保留表结构 
    2、速度快，但不可回滚，要三思 
    3、触发器中没有TRUNCATE，即这个语句无法触发任何操作 
    4、行标识的序号重置（或者可以说：新行标识所用的计数值重置为该列的种子） 
    5、DELETE语句每删除一条记录都是一个事务，会产生若干"日志"。但TRUNCATE是释放整个数据页（一个页8K），所以解释了上述的第二点。
    
    