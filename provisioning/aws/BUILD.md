# Create PNDA build components

![](../images/breadcrumbs-build.jpg)

## Introduction

In addition to projects like Hadoop and Kafka, PNDA also includes a variety of components that provide an operations console, application deployment and more. Build these components before provisioning PNDA.

## Create build node

#### Select build node

Designate or create the PNDA build node. This could be the same machine that was used to build the mirror file sets.
 
Two types of build node are supported -

- Red Hat Enterprise Linux 7
- Ubuntu 14.04 


#### Obtain build tools

The repository [pnda](https://github.com/pndaproject/pnda) contains all the tools needed to build PNDA.

Clone this repository to the build node.

#### Configure the proxy. (Optional)

The entire PNDA build process can be performed from behind a non-transparent proxy. 

To proceeding in this mode, first set the system configuration and then run the ```set-proxy-env.sh``` script that will set up the various proxy configurations needed by the multiple build tools.

```sh
sudo su
export http_proxy=http://<proxy_host>:<proxy_port>
export https_proxy=http://<proxy_host>:<proxy_port>
. set-proxy-env.sh
```

#### Preparing the build environment

The tools are found in the [build folder](https://github.com/pndaproject/pnda/tree/master/build).

The script ```install-build-tools.sh``` installs all the necessarily build prerequisites.

Run it with superuser privileges in the location that you wish to install your build tools.

For example

```sh
sudo su # Don't substitute user again if you did configure your proxy environment!
cd /home/builder
./install-build-tools.sh
```

As well as installing all the required software, it may pause and ask the operator to carry out some configuration on the build environment, for example adjusting the contents of /etc/hosts.

The script generates a file called ```set-pnda-env.sh``` containing the necessary environment settings needed to carry out builds. Ensure this is invoked before each build

For example

```sh
. /home/builder/set-pnda-env.sh
```

Your environment is now ready to build PNDA.

## Building PNDA

The script ```build-pnda.sh``` is invoked as a non-privileged user. 

If you are running behind a non-transparent proxy, go through the [proxy configuration](#configure-the-proxy-optional) steps again for the non-privileged user (don't substitute user).

For example

```sh
cd pnda
./build-pnda.sh RELEASE release/3.5
```

It is also possible to perform more complex builds including building to a specific bill-of-materials. Please refer to the [repository notes](https://github.com/pndaproject/pnda).

## Build Products

All build products are assembled in the directory ```pnda-dist```.

# [Next](STAGE.md)

| [Home](../OVERVIEW.md) | [Prepare](PREPARE.md) | [Mirror](MIRROR.md) | [Build](BUILD.md) | [Stage](STAGE.md) | [Configure](CONFIGURE.md) | [Create](CREATE.md) | 
| --- | --- | --- | --- | --- | --- | --- |
