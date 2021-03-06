# Create PNDA cluster

![](../images/breadcrumbs-create.jpg)

## Introduction

With the target platform fully prepared, the PNDA software staged and the YAML configuration completed, the final step is to invoke the PNDA CLI to create the cluster.

## Create PNDA

#### Install CLI dependencies

To use the PNDA command line interface, you will need to install the python, heat and nova clients. To install them on Ubuntu, run:

```
sudo apt-get -y update
sudo apt-get -y install python python-pip python-dev
cd cli
sudo pip install -r requirements.txt
```
#### Keystone authentication

You must authenticate with Keystone before using the OpenStack clients.

The easiest way to accomplish this is to download the credentials file usually named <project>-openrc.sh from Horizon for the given user and tenant, then source it in the shell you will use to create PNDA.

```
. <project>-openrc.sh
```

#### CLI invocation

The heat_cli.py scripts allows to launch a PNDA deployment. It sits in the cli subdirectory.


```
cd cli
./heat_cli.py
usage: heat_cli.py [-h] [-y] [-e PNDA_CLUSTER] [-n DATANODES]
                   [-o OPENTSDB_NODES] [-k KAFKA_NODES] [-z ZK_NODES]
                   [-f {standard}] [-b BRANCH] [-s KEYPAIR]
                   {create,destroy}
```

In particular note that the -s option refers to the name of the key pair created in the OpenStack tenant during the preparation phase.

Make sure you have access to the private key of this key pair otherwise you will not be able to connect to the bastion node and access the cluster.

```
./heat_cli.py -e cation -n 3 -o 1 -k 2 -z 3 -f standard -s <existing keypair> create
```

In the above example we create a standard flavor PNDA named cation. We specify 3 data nodes, 1 opentsdb node, 2 kafka nodes, 3 zookeeper nodes

A small cluster typically takes around 20 minutes to fully provision while a larger cluster can take 40 minutes.

# [Home](../OVERVIEW.md)

| [Home](../OVERVIEW.md) | [Prepare](PREPARE.md) | [Mirror](MIRROR.md) | [Build](BUILD.md) | [Stage](STAGE.md) | [Configure](CONFIGURE.md) | [Create](CREATE.md) | 
| --- | --- | --- | --- | --- | --- | --- | 
