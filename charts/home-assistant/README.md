# Home Assistant

This is a helm chart for [Home Assistant](https://www.home-assistant.io/)

## TL;DR;

```console
$ helm repo add captnbp https://TODO
$ helm install my-release captnbp/home-assistant
```

## Introduction

This code is adapted for [the official Home Assistant docker image](https://hub.docker.com/r/homeassistant/home-assistant/)

## Prerequisites

- Kubernetes 1.16+
- Helm 3.2+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm repo add captnbp https://TODO
$ helm install my-release captnbp/home-assistant
```

These commands deploy Home Assistant on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` release:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release. Remove also the chart using `--purge` option:

```console
$ helm delete --purge my-release
```

## Parameters

The following table lists the configurable parameters of the Home Assistant chart and their default values.

| Parameter                                         | Description                                                                                                                                               | Default                                                                                 |
|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `image.registry`                                  | Home Assistant image registry                                                                                                                              | `docker.io`                                                                             |
| `image.repository`                                | Home Assistant image repository                                                                                                                            | `homeassistant/home-assistant`                                                                 |
| `image.tag`                                       | Home Assistant image tag                                                                                                                                   | `1.112.4`                                                                            |
| `image.pullPolicy`                                | Image pull policy                                                                                                                                         | `IfNotPresent`                                                                          |
| `image.pullSecrets`                               | Specify docker-registry secret names as an array                                                                                                          | `[]` (does not add image pull secrets to deployed pods)                                 |
| `nameOverride`                                    | String to partially override Home Assistant.fullname template with a string (will prepend the release name)                                                | `nil`                                                                                   |
| `fullnameOverride`                                | String to fully override Home Assistant.fullname template with a string                                                                                    | `nil`                                                                                   |
| `extraVolumes`                                    | Extra volumes                                                                                                                                             |                                                                                         |
| `extraVolumeMounts`                               | Mount extra volume(s),                                                                                                                                    |                                                                                         |
| `replicas`                                        | Desired number of Home Assistant home-assistant nodes                                                                                                     | `1`                                                                                     |
| `service.type`                                    | Kubernetes Service type (home-assistant nodes)                                                                                                           | `ClusterIP`                                                                             |
| `service.port`                                    | Kubernetes Service port for Home Assistant transport port (home-assistant nodes)                                                                          | `9300`                                                                                  |
| `service.nodePort`                                | Kubernetes Service nodePort (home-assistant nodes)                                                                                                       | `nil`                                                                                   |
| `service.annotations`                             | Annotations for home-assistant nodes service                                                                                                             | `{}`                                                                                    |
| `service.loadBalancerIP`                          | loadBalancerIP if home-assistant nodes service type is `LoadBalancer`                                                                                    | `nil`                                                                                   |
| `resources`                                       | CPU/Memory resource requests/limits for home-assistant nodes pods                                                                                        | `requests: { cpu: "25m", memory: "256Mi" }`                                             |
| `persistence.enabled`                             | Enable persistence using a `PersistentVolumeClaim`                                                                                                        | `true`                                                                                  |
| `persistence.annotations`                         | Persistent Volume Claim annotations                                                                                                                       | `{}`                                                                                    |
| `persistence.storageClass`                        | Persistent Volume Storage Class                                                                                                                           | ``                                                                                      |
| `persistence.existingClaim`                | Existing Persistent Volume Claim                                                                                                                          | `nil`                                                                                   |
| `persistence.existingVolume`               | Existing Persistent Volume for use as volume match label selector to the `volumeClaimTemplate`                                                            | `nil`                                                                                   |
| `persistence.accessModes`                  | Persistent Volume Access Modes                                                                                                                            | `[ReadWriteOnce]`                                                                       |
| `persistence.size`                         | Persistent Volume Size                                                                                                                                    | `8Gi`                                                                                   |
| `securityContext`                          | Enable security context for Home Asssitant pods                                                                                                          | `false`                                                                                  |
| `probes.livenessProbe.enabled`                    | Enable/disable the liveness probe (home-assistant nodes pod)                                                                                             | `true`                                                                                  |
| `probes.livenessProbe.initialDelaySeconds`        | Delay before liveness probe is initiated (home-assistant nodes pod)                                                                                      | `90`                                                                                    |
| `probes.livenessProbe.periodSeconds`              | How often to perform the probe (home-assistant nodes pod)                                                                                                | `10`                                                                                    |
| `probes.livenessProbe.timeoutSeconds`             | When the probe times out (home-assistant nodes pod)                                                                                                      | `5`                                                                                     |
| `probes.livenessProbe.successThreshold`           | Minimum consecutive successes for the probe to be considered successful after having failed (home-assistant nodes pod)                                   | `1`                                                                                     |
| `probes.livenessProbe.failureThreshold`           | Minimum consecutive failures for the probe to be considered failed after having succeeded                                                                 | `5`                                                                                     |
| `probes.readinessProbe.enabled`                   | Enable/disable the readiness probe (home-assistant nodes pod)                                                                                            | `true`                                                                                  |
| `probes.readinessProbe.initialDelaySeconds`       | Delay before readiness probe is initiated (home-assistant nodes pod)                                                                                     | `90`                                                                                    |
| `probes.readinessProbe.periodSeconds`             | How often to perform the probe (home-assistant nodes pod)                                                                                                | `10`                                                                                    |
| `probes.readinessProbe.timeoutSeconds`            | When the probe times out (home-assistant nodes pod)                                                                                                      | `5`                                                                                     |
| `probes.readinessProbe.successThreshold`          | Minimum consecutive successes for the probe to be considered successful after having failed (home-assistant nodes pod)                                   | `1`                                                                                     |
| `probes.readinessProbe.failureThreshold`          | Minimum consecutive failures for the probe to be considered failed after having succeeded                                                                 | `5`                                                                                     |
| `serviceAccount.create`                    | Enable creation of ServiceAccount for the master node                                                                                                     | `false`                                                                                 |
| `serviceAccount.name`                      | Name of the created serviceAccount                                                                                                                        | Generated using the `home-assistant.fullname` template                            |
| `metrics.enabled`                                 | Enable prometheus exporter                                                                                                                                | `false`                                                                                 |
| `metrics.serviceMonitor.enabled`                  | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`)                                                    | `false`                                                                                 |
| `metrics.serviceMonitor.namespace`                | Namespace in which Prometheus is running                                                                                                                  | `nil`                                                                                   |
| `metrics.serviceMonitor.interval`                 | Interval at which metrics should be scraped.                                                                                                              | `nil` (Prometheus Operator default value)                                               |
| `metrics.serviceMonitor.scrapeTimeout`            | Timeout after which the scrape is ended                                                                                                                   | `nil` (Prometheus Operator default value)                                               |
| `metrics.serviceMonitor.selector`                 | Prometheus instance selector labels                                                                                                                       | `nil`                                                                                   |
| `metrics.serviceMonitor.bearerTokenSecret.value`  | Home Assistant Token                                                                                                                                | `nil`                                                                                   |
| `ingress.enabled`              | Enables Ingress | `false` |
| `ingress.annotations`          | Ingress annotations | `{}` |
| `ingress.path`                 | Ingress path | `/` |
| `ingress.hosts`                | Ingress accepted hostnames | `chart-example.local` |
| `ingress.tls`                  | Ingress TLS configuration | `[]` |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install my-release captnbp/home-assistant
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
$ helm install my-release -f values.yaml captnbp/home-assistant
```

> **Tip**: You can use the default [values.yaml](values.yaml).

## Configuration and installation details

## Persistence

By default, the chart mounts a [Persistent Volume](http://kubernetes.io/docs/user-guide/persistent-volumes/) at this location. The volume is created using dynamic volume provisioning. See the [Parameters](#parameters) section to configure the PVC.

## Notable changes
