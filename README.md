# local-k3d

Playing around with using [Taskfile](https://taskfile.dev/) to configure a local setup with k3d + apps and services.

Tested on:

![](img/neofetch.png)

## Requirements

The only things you need to have installed are:

- [Taskfile](https://taskfile.dev/installation/)

## Environment Variables

Use the [.env](./.env) file to configure the environment variables used by tasks.

## Aliases

Tasks have aliases defined, but the commands in this readme will use the full task name for clarity.

## Create a Cluster

You can configure the k3d cluster using the appropriate k3d config file in [configs](./configs/).
The [.env](./.env) value `CLUSTER_NAME` is used to name the cluster and reference the k3d config.

```shell
task create_cluster
```

## Delete a cluster

```shell
task delete_cluster
```

## Delete all clusters

```shell
task delete_all_clusters
```

## Install Raw k8s Manifests into Cluster

Simply add your manifests to [manifests](./manifests/) then run.

```shell
task apply_all_manifests
```

## Installs Apps from Helm Charts

You can define tasks to install apps from Helm charts. Add your custom values file to the [values dir](./values/) and reference
it in your task.

For example:

There's currently a task defined to install Argo Workflows into the k3d cluster.

> This task will also [create a k3d cluster](#create-a-cluster) if one doesn't already exist.

```shell
task install_argo_workflows
```