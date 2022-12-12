# HPC Cluster

This is the starting point for deploying an HPC Cluster with
[juju](https://juju.is).

## Prerequisites

### Juju

Install snap:

```
apt install snapd
```

Install juju:

```
snap install juju --channel=3.0/stable
```

Set up juju (for lxd, "localhost-localhost"):

```
juju bootstrap
juju add-model default
```

### Charms

* https://github.com/canonical/hpc-node-operators
* https://github.com/canonical/hpc-package-operators
* https://github.com/canonical/openldap-operators


## To Monitor

Set up monitor (in separate terminal window):

```
juju status --watch 5s --relations
```

## Basic Cluster

Note: Initial version of [hpc-cluster.yaml](./hpc-cluster.yaml)
is set up to pull local charms from the current directory. This will
be updated once the charms are in the charmhub store.

### Deploy

Note:
> The required charms must be available. At the moment (2022-12-12),
they should be in the same directory as the `hpc-cluster.yaml` file.

Deploy the cluster:

```
juju deploy ./hpc-cluster.yaml
```

### Scaling

Increase head (from 1 to 2):

```
juju add-unit -n 1
```

Increase interactive (from 1 to 4):

```
juju add-unit interactive -n 3
```

Increase compute (from 1 to 10):

```
juju add-unit compute -n 9
```
