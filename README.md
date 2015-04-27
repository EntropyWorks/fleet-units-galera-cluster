# Simple MySQL Replication using CoreOS and Percona Galera Cluster

Once you have a working CoreOS environment you should beable to submit
the following fleet units to startup and configure your Galera Cluster.

## Requirements

 - CoreOS or similar base OS
 - etcd service 
 - fleet service
 - flannel service

## Template needs modification

The file galera@.template should be modified to reflect the proper endpoints you need.

## Fleet Units

There are multiple `fleet-units` 

 - `galera@.service` = This starts up the Galera docker container
 - `galera-announce@.service` = Reports to etcd the internal IP

## Warning 
You really should change the default passwords within `galera@.service`. I haven't figured 
out a good way to have `ansible` or `saltstack` be the actually process that 
submits the `fleet-units`. So for now while I'm testing this is how the password
are being done. 

If you don't change them thats your call. These are just templates.

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
