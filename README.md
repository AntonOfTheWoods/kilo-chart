# kilo

[kilo](https://kilo.squat.ai) is a multi-cloud network overlay built on WireGuard and designed for Kubernetes.

## TL;DR

```bash
$ helm repo add ??? https://charts.???.???/charts
$ helm install my-release ???/kilo
```

## Introduction

This chart bootstraps a [kilo](https://kilo.squat.ai), [wireguard](http://wireguard.com/)-based network overlay over a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.19+ (only tested on 1.19+, may work with previous versions)
- Helm 2.12+ or Helm 3.0-beta3+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm upgrade --install my-release ???/kilo
```

The command deploys the `kilo` overlay on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the kilo chart and their default values.

| Parameter                                   | Description                                                                                                          | Default                                                      |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `global.imageRegistry`                      | Global Docker Image registry                                                                                         | `nil`                                                        |
| `global.imagePullSecrets`                   | Global Docker registry secret names as an array                                                                      | `[]` (does not add image pull secrets to deployed pods)      |
| `global.storageClass`                       | Global storage class for dynamic provisioning                                                                        | `nil`                                                        |

### Common parameters

| Parameter                                   | Description                                                                                                          | Default                                                      |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `nameOverride`                              | String to partially override kilo.fullname                                                                        | `nil`                                                        |
| `fullnameOverride`                          | String to fully override kilo.fullname                                                                            | `nil`                                                        |
| `clusterDomain`                             | Default Kubernetes cluster domain                                                                                    | `cluster.local`                                              |
| `commonLabels`                              | Labels to add to all deployed objects                                                                                | `nil`                                                        |
| `commonAnnotations`                         | Annotations to add to all deployed objects                                                                           | `[]`                                                         |
| `schedulerName`                             | Name of the scheduler (other than default) to dispatch pods                                                          | `nil`                                                        |
| `extraDeploy`                               | Array of extra objects to deploy with the release (evaluated as a template)                                          | `nil`                                                        |

### kilo common parameters

| Parameter                                   | Description                                                                                                          | Default                                                      |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `image.registry`                            | kilo image registry                                                                                               | `docker.io`                                                  |
| `image.repository`                          | kilo image name                                                                                                   | `???/kilo`                                            |
| `image.tag`                                 | kilo image tag                                                                                                    | `{TAG_NAME}`                                                 |
| `image.pullPolicy`                          | kilo image pull policy                                                                                            | `IfNotPresent`                                               |
| `image.pullSecrets`                         | Specify docker-registry secret names as an array                                                                     | `[]` (does not add image pull secrets to deployed pods)      |
| `image.debug`                               | Specify if debug logs should be enabled                                                                              | `false`                                                      |

### kilo daemon parameters

| Parameter                                    | Description                                                                                                          | Default                                                      |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `kdaemon.command`                            | Override default container command on kilo kdaemon container(s) (useful when using custom images)                 | `nil`                                                        |
| `kdaemon.args`                               | Override default container args on kilo kdaemon container(s) (useful when using custom images)                    | `nil`                                                        |
| `kdaemon.configuration`                      | kilo kdaemon configuration to be injected as ConfigMap                                                            | Check `values.yaml` file                                     |
| `kdaemon.existingConfigmap`                  | Name of existing ConfigMap with kilo kdaemon configuration                                                        | `nil`                                                        |
| `kdaemon.podAnnotations`                     | Additional pod annotations for kilo kdaemon pods                                                                  | `{}` (evaluated as a template)                               |
| `kdaemon.podLabels`                          | Additional pod labels for kilo kdaemon pods                                                                       | `{}` (evaluated as a template)                               |
| `kdaemon.podAffinityPreset`                  | kilo kdaemon pod affinity preset. Ignored if `kdaemon.affinity` is set. Allowed values: `soft` or `hard`          | `""`                                                         |
| `kdaemon.podAntiAffinityPreset`              | kilo kdaemon pod anti-affinity preset. Ignored if `kdaemon.affinity` is set. Allowed values: `soft` or `hard`     | `soft`                                                       |
| `kdaemon.nodeAffinityPreset.type`            | kilo kdaemon node affinity preset type. Ignored if `kdaemon.affinity` is set. Allowed values: `soft` or `hard`    | `""`                                                         |
| `kdaemon.nodeAffinityPreset.key`             | kilo kdaemon node label key to match Ignored if `kdaemon.affinity` is set.                                        | `""`                                                         |
| `kdaemon.nodeAffinityPreset.values`          | kilo kdaemon node label values to match. Ignored if `kdaemon.affinity` is set.                                    | `[]`                                                         |
| `kdaemon.affinity`                           | Affinity for kilo kdaemon pods assignment                                                                         | `{}` (evaluated as a template)                               |
| `kdaemon.nodeSelector`                       | Node labels for kilo kdaemon pods assignment                                                                      | `{}` (evaluated as a template)                               |
| `kdaemon.tolerations`                        | Tolerations for kilo kdaemon pods assignment                                                                      | `[]` (evaluated as a template)                               |
| `kdaemon.podSecurityContext.enabled`         | Enable security context for kilo kdaemon pods                                                                     | `true`                                                       |
| `kdaemon.podSecurityContext.fsGroup`         | Group ID for the mounted volumes' filesystem                                                                         | `1001`                                                       |
| `kdaemon.containerSecurityContext.enabled`   | kilo kdaemon container securityContext                                                                            | `true`                                                       |
| `kdaemon.containerSecurityContext.runAsUser` | User ID for the kilo kdaemon container                                                                            | `1001`                                                       |
| `kdaemon.resources.limits`                   | The resources limits for kilo kdaemon containers                                                                  | `{}`                                                         |
| `kdaemon.resources.requests`                 | The requested resources for kilo kdaemon containers                                                               | `{}`                                                         |
| `kdaemon.extraEnvVars`                       | Extra environment variables to be set on kilo kdaemon containers                                                  | `{}`                                                         |
| `kdaemon.extraEnvVarsCM`                     | Name of existing ConfigMap containing extra env vars for kilo kdaemon containers                                  | `nil`                                                        |
| `kdaemon.extraEnvVarsSecret`                 | Name of existing Secret containing extra env vars for kilo kdaemon containers                                     | `nil`                                                        |
| `kdaemon.extraFlags`                         | kilo kdaemon additional command line flags                                                                        | `nil`                                                        |
| `kdaemon.initContainers`                     | Add additional init containers for the kilo kdaemon pod(s)                                                        | `{}` (evaluated as a template)                               |
| `kdaemon.sidecars`                           | Add additional sidecar containers for the kilo kdaemon pod(s)                                                     | `{}` (evaluated as a template)                               |
| `kdaemon.extraVolumeMounts`                  | Optionally specify extra list of additional volumeMounts for the kilo kdaemon container(s)                        | `{}`                                                         |
| `kdaemon.extraVolumes`                       | Optionally specify extra list of additional volumes to the kilo kdaemon pod(s)                                    | `{}`                                                         |

### RBAC parameters

| Parameter                                   | Description                                                                                                          | Default                                                      |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `serviceAccount.create`                     | Enable the creation of a ServiceAccount for kilo pods                                                             | `true`                                                       |
| `serviceAccount.name`                       | Name of the created ServiceAccount                                                                                   | Generated using the `kilo.fullname` template              |
| `serviceAccount.annotations`                | Annotations for kilo Service Account                                                                              | `{}` (evaluated as a template)                               |
| `rbac.create`                               | Weather to create & use RBAC resources or not                                                                        | `true`                                                      |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install my-release \
  --set kdaemon.args=\{--mesh-granularity=full,--subnet=10.5.0.0/16\} \
    ???/kilo
```

The above command adds the two parameters necessary to activate full mesh between all nodes of the cluster and changes the subnet from the default `10.4.0.1/16`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install my-release -f values.yaml ???/kilo
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

We will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Change kilo version

To modify the kilo version used in this chart you can specify a [valid image tag](https://hub.docker.com/r/squat/kilo/tags/) using the `image.tag` parameter. For example, `image.tag=X.Y.Z`. This approach is also applicable to other images like exporters.

### Sidecars and Init Containers

If you have a need for additional containers to run within the same pod as kilo, you can do so via the `sidecars` config parameter. Simply define your container according to the Kubernetes container spec.

```yaml
sidecars:
  - name: your-image-name
    image: your-image
    imagePullPolicy: Always
    ports:
      - name: portname
       containerPort: 1234
```

Similarly, you can add extra init containers using the `initContainers` parameter.

```yaml
initContainers:
  - name: your-image-name
    image: your-image
    imagePullPolicy: Always
    ports:
      - name: portname
        containerPort: 1234
```

## Chart origins and copyright
This chart was developed from the [bitnami template](https://github.com/bitnami/charts/tree/b3a95b701b611ab51924ae5665bcc8cd5ac56898/template). That code is made available by [bitnami](https://github.com/bitnami/) under an Apache License, Version 2.0.

Modifications to that code are made available under the GNU AFFERO GENERAL PUBLIC LICENSE, Version 3.

## Troubleshooting

First of all, start with the documentation mean for how to deal with common errors related to Bitnami’s Helm charts in [this troubleshooting guide](https://docs.bitnami.com/general/how-to/troubleshoot-helm-chart-issues).

If you can't solve your issue, then please create one on this repository.

## Upgrading

FIXME: Can we upgrade?
