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

Tasks have aliases defined, but the commands in this README will use the full task name for clarity.

You can list all of the available tasks to see their aliases.

```shell
task -a
```

## Root Tasks

The tasks defined in the root [Taskfile.yml](./Taskfile.yml) are the tasks directly related to managing the k3d cluster.

### Create a Cluster

You can configure the k3d cluster using the appropriate k3d config file in the [configs dir](./configs/).
The [.env](./.env) value `CLUSTER_NAME` is used to name the cluster and reference the k3d config.

```shell
task create_cluster
```

### Delete a cluster

```shell
task delete_cluster
```

### Delete all clusters

```shell
task delete_all_clusters
```

## DeployTasks

Define tasks in [DeployTasks.yml](./tasks/DeployTasks.yml) that deploy apps/services/etc to a k3d cluster.

Examples:
- Argo Workflows
- Nginx Ingress
- Secrets
- etc.

You can then reference those tasks as `deployTasks:<name_of_task>`.

### Deploy Raw k8s Manifests into Cluster

Simply add your manifests to the [manifests dir](./manifests/) then run.

```shell
task deployTasks:apply_all_manifests
```

### Deploy Apps from Helm Charts

You can define tasks to install apps from Helm charts. Add your custom values file to the [values dir](./values/) and reference
it in your task.

For example:

There's currently a task defined to install Argo Workflows into the k3d cluster.

> This task will fail if a cluster hasn't already been created

```shell
task deployTasks:install_argo_workflows
```

## InstallTasks

Define tasks in [InstallTasks.yml](./tasks/InstallTasks.yml) that install apps/services/etc to your local machine.

Examples:
- orbstack
- kubectl
- helm
- etc.

You can then reference those tasks as `installTasks:<name_of_task>`.

> Most of these are internal tasks and aren't used via the CLI.