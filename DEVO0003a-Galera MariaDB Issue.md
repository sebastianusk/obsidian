So Galera is a multi-master MariaDB tool to make sure we have replicas, previously the MariaDB is deployed 3 times and has galera running there.

Somehow, if you start Galera at the same time, you'll see that they'll try to communicate before the database is ready, this causes issue that all of them won't be up

Trying to reduce the deployment into one wasn't working either. the first pod is not the last that's exiting the cluster causing it to be unable to start.

To mitigate it, I pull the persistent volume snapshot via the EBS snapshot, then attach it to an EC2.

from the inside, I can run it like this 
```
mkdir /cstate
mount /dev/sdb /cstate

docker run --name galera -p 3306:3306 -e MARIADB_ROOT_PASSWORD=fazz2020P1 -e MARIADB_GALERA_MARIABACKUP_PASSWORD=fazz2020P1 -e MARIADB_USER=infra0 -e MARIADB_PASSWORD=fazz2020P1 -e MARIADB_DATABASE=infra -e MARIADB_GALERA_MARIABACKUP_USER=mariabackup -e MARIADB_ENABLE_LDAP=no -e MARIADB_ENABLE_TLS=no -v /cstate:/bitnami/mariadb docker.io/bitnami/mariadb-galera:10.4.12-debian-10-r88

```
after running this command, there will be one error where the database is not the last that's exiting the cluster. however since this is just a normal server, I can easily modify the files to let the database start as an individual database