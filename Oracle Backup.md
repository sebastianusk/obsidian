---
tags:
  - zettelkasten
topic: 
createAt: 2024-04-03 21:20
---
- Point In Time Recovery
	- It's using [RMAN](https://docs.oracle.com/en/database/oracle/oracle-database/19/bradv/getting-started-rman.html#GUID-871FF5B2-C82B-462E-8182-FA28CF7B3E3B)
	- the command to run backup once:
		- `backup as compressed backupset incremental level 0 database plus archivelog not backed up;`
	- to recover:
```
RMAN> shutdown immediate
RMAN> startup mount
RMAN> run
2> {
3> set until time="to_date('26102009 10:34:16','ddmmyyyy hh24:mi:ss')";
4> restore database;
5> recover database;
6> }
RMAN> alter database open resetlogs;
database opened
RMAN>
```

source https://www.dba-oracle.com/t_rman_70_time_based_incomplete_recovery.htm