Part of [[Oracle]]
```
SELECT * FROM DBA_SYS_PRIVS where grantee = 'VIEW_USER';
SELECT * FROM DBA_TAB_PRIVS where grantee = 'VIEW_USER';
SELECT * FROM DBA_ROLE_PRIVS where grantee = 'VIEW_USER';

SELECT * FROM role_role_privs where role = 'VIEW_ROLE';
SELECT * FROM role_tab_privs where role = 'VIEW_ROLE';
SELECT * FROM role_sys_privs where role = 'VIEW_ROLE';

-- SVFE
Select 'GRANT SELECT ON SVISTA.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='SVISTA';
Select 'GRANT SELECT ON APIGATE.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='APIGATE';
Select 'GRANT SELECT ON SMSGATE.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='SMSGATE';

-- SVBO
Select 'GRANT SELECT ON MAIN.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='MAIN';
Select 'GRANT SELECT ON SVWEB.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='SVWEB';

-- ACS
Select 'GRANT SELECT ON ACS.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='ACS';

-- SVCG
Select 'GRANT SELECT ON SVCG.'||Table_Name||' TO VIEW_ONLY;' From All_Tables Where Owner='SVCG';

GRANT VIEW_ONLY TO DATADOG;

```