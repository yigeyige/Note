#**Oracle*

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