# Ansible Hadoop
**Need Help?:** [Issues Tracking](https://github.com/NFLabs/ansible-hadoop/issues) | [acorbacho@nflabs.com](mailto:acorbacho@nflabs.com) <br/>
**Contributing:** [Contribution Guide](https://github.com/NFLabs/ansible-hadoop/blob/master/CONTRIBUTING.md)<br/>
**License:** [Apache 2.0](https://github.com/NFLabs/ansible-hadoop/blob/master/LICENSE)

Ansible Haddop is a playbook that help you to deploy a new Hadoop (CDH4) and Spark cluster on a CentOS 6 or RHEL 6 environment using Ansible.

The playbooks can:

 1. Deploy a fully functional Hadoop cluster **with High Availability (HA) and automatic failover**.
 2. Deploy additional nodes to scale the cluster (datanodes and spark workers)

### List of services 
 * Hadoop CDH4
    * Zookeeper
    * Journalnode
    * HDFS
 * Apache Spark
 * Elasticsearch *--OPTIONAL--*
 * Ganglia *--OPTIONAL--*

## Requirements
 * Ansible 1.6+
 * CentOS 6.5+ or RedHat servers

## Configuration

edit the files:

 * `hosts` : Set the hosts and services
 * `group_vars/all`: to change/add  more configuration parameters (ex: hdfs path, spark port etcetc) <br/>
 
  ```
  site_name: mycluster					# The name of your cluster
  with_elasticsearch: True/False		# If true, deploy an Elasticsearch cluster.
  update_iptables: True/False			# If True, change iptables file to add ip_range.
  update_hosts: True/False				# If True, set the hosts file to every host in the cluster.
  install_oracle_jdk: True/False		# If True, download and Install Oracle JDK from oracle server. 
  with_ganglia: True/False				# If True, deploy ganglia to monitor your cluster health.
  
  spark:
    version: 1.2.1						# Set the version of Spark you want to deploy
    
  elasticsearch:
    version: 1.4.1						# Set the version of Elasticsearch you want to deploy
    									# (**only if with_elasticsearch is True**)
  
  ```

# Deploy a new cluster

To run with Ansible:

```sh
./deploy
```

To e.g. just install ZooKeeper, add the `zookeeper` tag as argument.
available tags: 
 
 * elasticsearch
 * hadoop
 * ntp
 * zookeeper
 * slaves
 * spark
 * ganglia

```sh
./deploy zookeeper
```

### Services url
Dont forget to open the port of the hosts if you want to access to your cluster remotely.


 * **HDFS : active**: master:50070 - *active*
 * **HDFS : stand by**: master2:50070 - *standby*
 * **Spark Master : active**: master:8080
 * **Spark Master2 : stand by**: master2:8080
 * **Elasticsearch**: eshost:9200
 * **Ganglia**: monitor:80

# Restart service or cluster

restart all services run 
```
./restart
```

If you want just restart some services run:

```sh
./restart serviceName
```

List of service that can be restarted

 * zookeepers
 * journalnodes
 * elasticsearch
 * namenodes
 * datanodes
 * sparkmasters
 * sparckworkers

