[[Oracle]]
# Check status
### Check status
```
dgmgrl / as sysdba
show configuration
```
### Check Archive log
```
select max(sequence#) from v$archived_log where archived='YES';
```
# Active Dataguard
### Enable
```
SQL> alter database open;
SQL> alter database recover managed standby database disconnect from session;
```
### Disable
```
DGMGRL> edit database svfeaws set state=apply-off;

SQL> shutdown immediate
SQL> startup nomount
SQL> alter database mount standby database;
SQL> alter database recover managed standby database disconnect from session;

DGMGRL> edit database svfeaws set state=apply-on;
```
