# Bookstack

[Bookstack](https://www.bookstackapp.com) is a simple, easy-to-use platform for organising and storing information.

## TL;DR;

```bash
$ helm install stable/bookstack
```

## Introduction

This chart bootstraps a [Bookstack](https://hub.docker.com/r/solidnerd/bookstack/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

It also uses the [MariaDB chart](https://github.com/kubernetes/charts/tree/master/stable/mariadb) which satisfies the database requirements of the application.

## Prerequisites

- Kubernetes 1.9+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure
- If `tls` is enabled, `cert-manager` needs to be installed.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm update --install my-release stable/bookstack
```

The command deploys Bookstack on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm upgrade --install my-release \
  --set hostname=bookstack.example.com \
    stable/bookstack
```

The above command sets the hostname.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```bash
$ helm upgrade --install my-release -f values.yaml stable/bookstack
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Replicas

Bookstack writes uploaded files to a persistent volume. By default that volume
cannot be shared between pods (RWO). In such a configuration the `replicas` option
must be set to `1`. If the persistent volume supports more than one writer
(RWX), ie NFS, `replicaCount` can be greater than `1`.

## Persistence

The [Bookstack](https://hub.docker.com/r/solidnerd/bookstack/) image stores the uploaded data at the `public/uploads` path, relative to the document root of the Bookstack application. Other misc. data is stored under the `public/storage` path, also relative to the document root of the application.

Persistent Volume Claims are used to keep the data across deployments. The volume is created using dynamic volume provisioning.

See the [Configuration](#configuration) section to configure the PVC or to disable persistence.
