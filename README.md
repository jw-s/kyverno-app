# Kyverno

[Kyverno](https://kyverno.io) is a Kubernetes Native Policy Management engine. It allows you to:

- Manage policies as Kubernetes resources (no new language required.)
- Validate, mutate, and generate resource configurations.
- Select resources based on labels and wildcards.
- View policy enforcement as events.
- Scan existing resources for violations.

Access the complete user documentation and guides at: https://kyverno.io.

## TL;DR

```console
## Add the Kyverno Helm repository
$ helm repo add kyverno https://kyverno.github.io/kyverno/

## Install the Kyverno Helm chart
$ helm install kyverno --namespace kyverno kyverno/kyverno --create-namespace
```

## Introduction

This chart bootstraps a Kyverno deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Installing the Chart

**Add the Kyverno Helm repository:**

```console
$ helm repo add kyverno https://kyverno.github.io/kyverno/
```

**Create a namespace:**

You can install Kyverno in any namespace. The examples use `kyverno` as the namespace.

```console
$ kubectl create namespace kyverno
```

**Install the Kyverno chart:**

```console
$ helm install kyverno --namespace kyverno kyverno ./charts/kyverno
```

The command deploys Kyverno on the Kubernetes cluster with default configuration. The [installation](https://kyverno.io/docs/installation/) guide lists the parameters that can be configured during installation.

The Kyverno ClusterRole/ClusterRoleBinding that manages webhook configurations must have the suffix `:webhook`. Ex., `*:webhook` or `kyverno:webhook`.
Other ClusterRole/ClusterRoleBinding names are configurable.

## Uninstalling the Chart

To uninstall/delete the `kyverno` deployment:

```console
$ helm delete -n kyverno kyverno
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the kyverno chart and their default values.

| Parameter | Description | Default |
|--|--|--|
| `antiAffinity.enable` | pod antiAffinities toggle. Enabled by default but can be disabled if you want to schedule pods to the same node | `true` |
| `createSelfSignedCert` | generate a self signed cert and certificate authority. Kyverno defaults to using kube-controller-manager CA-signed certificate or existing cert secret if false. | `false` |
| `config.existingConfig` | existing Kubernetes configmap to use for the resource filters configuration | `nil` |
| `config.resourceFilters` | list of resource types to be skipped by kyverno policy engine. See [documentation](https://kyverno.io/docs/installation/#resource-filters) for details | `[Event,*,*][*,kube-system,*][*,kube-public,*][*,kube-node-lease,*][Node,*,*][APIService,*,*][TokenReview,*,*][SubjectAccessReview,*,*][SelfSubjectAccessReview,*,*][*,kyverno,kyverno*][Binding,*,*][ReplicaSet,*,*][ReportChangeRequest,*,*][ClusterReportChangeRequest,*,*]` |
| `config.webhooks` | customize webhook configurations for both MutatingWebhookConfiguration and ValidatingWebhookConfiguration of Kubernetes resources, only `namespaceSelector` can be configured with Kyverno v1.4.0 | `nil` |
| `customLabels` | Additional labels | `{}` |
| `dnsPolicy` | Sets the DNS Policy which determines the manner in which DNS resolution happens across the cluster. For further reference, see [the official Kubernetes docs](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#pod-s-dns-policy) | `ClusterFirst` |
| `envVarsInit` | Extra environment variables to pass to kyverno initContainers |
| `envVars` | Extra environment variables to pass to Kyverno | `{}` |
| `extraArgs` | object for extra arguments to give to the binary (`--set extraArgs={"-v=4"}`) | `{}` |
| `fullnameOverride` | override the expanded name of the chart | `nil` |
| `generatecontrollerExtraResources` | extra resource type Kyverno is allowed to generate | `[]` |
| `hostNetwork` | Use the host network's namespace. Set it to `true` when dealing with a custom CNI over Amazon EKS | `false` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `image.pullSecrets` | Specify image pull secrets | `[]` (does not add image pull secrets to deployed pods) |
| `image.repository` | Image repository | `ghcr.io/kyverno/kyverno` |
| `image.tag` | Image tag | `nil` |
| `initImage.pullPolicy` | Init image pull policy | `nil` |
| `initImage.repository` | Init image repository | `ghcr.io/kyverno/kyvernopre` |
| `initImage.tag` | Init image tag | `nil` |
| `installCRDs` | Install the Kyverno CRDs | `true` |
| `livenessProbe` | liveness probe configuration | `{}` |
| `nameOverride` | override the name of the chart | `nil` |
| `namespace` | namespace the chart deploy to | `nil` |
| `networkPolicy.enabled` | when true, use a NetworkPolicy to grant access to the webhook. | `false` |
| `networkPolicy.ingressFrom` | A list of valid from selectors. | `[]` |
| `nodeAffinity` | node affinities. Empty by default. Can be added for nodeAffinities. | `nil` |
| `nodeSelector` | node labels for pod assignment | `{}` |
| `podAffinity` | pod affinities. Empty by default. Can be added for podAffinities. | `nil` |
| `podAntiAffinity` | pod antiAffinities default values. can be overwrite | `Pod Anti Affinity` |
| `podAnnotations` | annotations to add to each pod | `{}` |
| `podLabels` | additional labels to add to each pod | `{}` |
| `podSecurityContext` | security context for the pod | `{}` |
| `podDisruptionBudget.minAvailable` | Configures the minimum available pods for kyverno disruptions. Cannot used if `maxUnavailable` is set. | `1` |
| `podDisruptionBudget.maxUnavailable` | Configures the maximum unavailable pods for kyverno disruptions. Cannot used if `minAvailable` is set. | `nil` |
| `priorityClassName` | priorityClassName | `nil` |
| `rbac.create` | create ClusterRoles, ClusterRoleBindings, and ServiceAccount | `true` |
| `rbac.serviceAccount.create` | create a ServiceAccount | `true` |
| `rbac.serviceAccount.name` | the ServiceAccount name | `nil` |
| `rbac.serviceAccount.annotations` | annotations for the ServiceAccount | `{}` |
| `readinessProbe` | readiness probe configuration | `{}` |
| `replicaCount` | desired number of pods | `0` |
| `mode` | a mode for Kyverno installation | `standalone` |
| `resources` | pod resource requests and limits | `{}` |
| `securityContext` | security context configuration | `{}` |
| `service.annotations` | annotations to add to the service | `{}` |
| `service.nodePort` | node port | `nil` |
| `service.port` | port for the service | `443` |
| `service.type` | type of service | `ClusterIP` |
| `serviceMonitor.enabled` | create a ServiceMonitor(Requires Prometheus) | `false` |
| `serviceMonitor.namespace` | override namespace for ServiceMonitor (default is same than kyverno) | `false` |
| `serviceMonitor.additionalLabels` | additional labels to add for ServiceMonitor | `nil` |
| `serviceMonitor.interval` | interval to scrape metrics | `30s` |
| `serviceMonitor.scrapeTimeout` | timeout if metrics can't be retrieved in given time interval | `25s` |
| `serviceMonitor.secure` | is TLS required for endpoint | `false` |
| `serviceMonitor.tlsConfig` | TLS Configuration for endpoint | `[]` |
| `testImage.pullPolicy` | image pull policy for test image (defaults to `image.pullPolicy`) | `nil` |
| `testImage.repository` | repository for chart test image | `busybox` |
| `testImage.tag` | tag for chart test image | `nil` |
| `tolerations` | list of node taints to tolerate | `[]` |
| `topologySpreadConstraints` | node/pod topology spread constrains | `[]` |  |
| `webhooksCleanup.enable` | create a helm pre-delete hook to cleanup webhooks | `false`|
| `webhooksCleanup.image` | kubectl image to run commands for deleting webhooks| `bitnami/kubectl:latest`|

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --namespace kyverno kyverno ./charts/kyverno \
  --set=image.tag=v0.0.2,resources.limits.cpu=200m
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --namespace kyverno kyverno ./charts/kyverno -f values.yaml
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## TLS Configuration

If `createSelfSignedCert` is `true`, Helm will take care of the steps of creating an external self-signed certificate described in option 2 of the [installation documentation](https://kyverno.io/docs/installation/#option-2-use-your-own-ca-signed-certificate)

If `createSelfSignedCert` is `false`, Kyverno will generate a self-signed CA and a certificate, or you can provide your own TLS CA and signed-key pair and create the secret yourself as described in the [documentation](https://kyverno.io/docs/installation/#customize-the-installation-of-kyverno).

## Kyverno CLI

See: https://kyverno.io/docs/kyverno-cli/
