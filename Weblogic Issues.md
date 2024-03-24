- Staging
	- [[2023-03-21]]
```[root@ntttestapp01 init.d]# ./wls12 status
MY_MW_HOME_TO_USE hasnt been specified. Trying to detect it...
MW_HOME: /home/weblogic/Oracle/Middleware/Oracle_Home
Checking Managed Servers...
Checking Applications...
Status: Failed
Managed servers status: 1
Applications status: 1
[root@ntttestapp01 init.d]# ./wls12 start
MY_MW_HOME_TO_USE hasnt been specified. Trying to detect it...
MW_HOME: /home/weblogic/Oracle/Middleware/Oracle_Home
Adding Virtual IP address is not enabled
Removing lock files...
starting AdminServer
Starting Nodemanager
Wait for Adminserver startup
AdminServer is started
Starting Managed Servers

Initializing WebLogic Scripting Tool (WLST) ...

Welcome to WebLogic Server Administration Scripting Shell

Type help() for help on available commands

Invoking base_domain.startManagedServersMany.py script
Connecting to Adminserver.
Connecting to t3://localhost:7001 with userid weblogic ...
Successfully connected to Admin Server "AdminServer" that belongs to domain "base_domain".

Warning: An insecure protocol was used to connect to the server.
To ensure on-the-wire security, the SSL port or Admin port should be used instead.

Location changed to domainConfig tree. This is a read-only tree
with DomainMBean as the root MBean.
For more help, use help('domainConfig')

Location changed to domainRuntime tree. This is a read-only tree
with DomainMBean as the root MBean.
For more help, use help('domainRuntime')

Skipping server: AdminServer
SVFE: RUNNING
SVBO: RUNNING
SVBUS: RUNNING
SVCG: RUNNING
ACS_CORE: RUNNING
ACS_UI: RUNNING
SMSGATE: RUNNING
APIGATE: RUNNING
Disconnected from weblogic server: AdminServer


Exiting WebLogic Scripting Tool.

Weblogic Started successfuly

```

