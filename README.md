# Simple MySQL Replication using CoreOS and Percona Galera Cluster

Once you have a working CoreOS environment you should beable to submit
the following fleet units to startup and configure your Galera Cluster.

## Requirements

 - CoreOS or similar base OS
 - etcd service 
 - fleet service
 - flannel service

## Fleet Units

There are multiple `fleet-units` 

 - `galera@.service` = This starts up the Galera docker container
 - `galera-announce@.service` = Reports to etcd the internal IP

## Submitting fleet-unit files

Submit the fleet-unit files in the following order.

```
fleetctl submit galera@.service
fleetctl submit galera-announce@.service  
```

Start up the first Galera process and its sidekick `galera-accounce`

```
fleetctl start galera@01.service
fleetctl start galera-announce@01.service  
```

```
fleetctl start galera@02.service
fleetctl start galera-announce@02.service  
```

```
fleetctl start galera@03.service
fleetctl start galera-announce@03.service  
```
