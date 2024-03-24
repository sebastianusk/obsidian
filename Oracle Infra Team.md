Part of [[Oracle]]
```
SQL> SELECT * FROM DBA_SYS_PRIVS where grantee = 'ALIYUL';

"GRANTEE","PRIVILEGE","ADMIN_OPTION","COMMON","INHERITED"
"ALIYUL","UNLIMITED TABLESPACE","YES","NO","NO"

SQL> SELECT * FROM DBA_TAB_PRIVS where grantee = 'ALIYUL';

no rows selected

SQL> SELECT * FROM DBA_ROLE_PRIVS where grantee = 'ALIYUL';

"GRANTEE","GRANTED_ROLE","ADMIN_OPTION","DELEGATE_OPTION","DEFAULT_ROLE","COMMON","INHERITED"
"ALIYUL","DBA","YES","NO","YES","NO","NO"
```