# Kubernetes Metrics Server

## User guide - 用户指南

You can find the user guide in [the official Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/).<br>
你可以在 [Kubernetes官方文档](https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/) 中找到用户指南。

## Design - 设计

The detailed design of the project can be found in the following docs:<br>
可以在以下文档中找到项目的详细设计：

- [Metrics API](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/resource-metrics-api.md)
- [Metrics Server](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/metrics-server.md)

For the broader view of monitoring in Kubernetes take a look into [Monitoring architecture](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/monitoring_architecture.md)<br>
要更广泛地了解Kubernetes中的监控，请查看 [监控的体系结构](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/monitoring_architecture.md) 。

## Deployment - 部署

Compatibility matrix:<br>
兼容性矩阵

Metrics Server | Metrics API group/version | Supported Kubernetes version
---------------|---------------------------|-----------------------------
0.3.x          | `metrics.k8s.io/v1beta1`  | 1.8+
0.2.x          | `metrics.k8s.io/v1beta1`  | 1.8+
0.1.x          | `metrics/v1alpha1`        | 1.7

In order to deploy metrics-server in your cluster run the following command from the top-level directory of this repository:<br>
要在集群中部署 `metrics-server` ，需要在这个仓库的顶层目录中执行以下命令：

```console
# Kubernetes 1.7
$ kubectl create -f deploy/1.7/

# Kubernetes > 1.8
$ kubectl create -f deploy/1.8+/
```

You can also use this helm chart to deploy the metric-server in your cluster (This isn't supported by the metrics-server maintainers): https://github.com/helm/charts/tree/master/stable/metrics-server<br>
你还可以使用这个 `Helm Chart` 来把 `metrics-server` 部署到你的集群中（ `metrics-server` 维护者不支持这种方式）：https://github.com/helm/charts/tree/master/stable/metrics-server

## Flags - 标记

Metrics Server supports all the standard Kubernetes API server flags, as well as the standard Kubernetes `glog` logging flags.<br>
`metrics-server` 支持所有标准的 `Kubernetes API Server` 标记，以及标准的 `Kubernetes glog` 日志标记。

The most commonly-used ones are:<br>
最常用的如下：

- `--logtostderr`: log to standard error instead of files in the container. You generally want this on.<br>
- `--logtostderr` ：在标准错误中记录日志，而不是在容器文件中。你一般都想要开启这个。

- `--v=<X>`: set log verbosity. It's generally a good idea to run a log level 1 or 2 unless you're encountering errors. At log level 10, large amounts of diagnostic information will be reported, include API request and response bodies, and raw metric results from Kubelet.<br>
- `--v=<X>` ：设置日志信息的复杂度（日志的赘言级别）。通常情况下，把日志级别设置为1或2来运行是比较好的，除非你碰到了问题。日志级别设置为10时，会报告大量的诊断信息，包括API的请求和响应体，以及来自Kubelet的原始指标结果。

- `--secure-port=<port>`: set the secure port. If you're not running as root, you'll want to set this to something other than the default (port 443).<br>
- `--secure-port=<port>` ：设置安全端口。如果你不是以root用户来运行的话，你可能会想把安全端口设置为其他值而不是默认端口443。

- `--tls-cert-file`, `--tls-private-key-file`: the serving certificate and key files. If not specified, self-signed certificates will be generated, but it's recommended that you use non-self-signed certificates in production.<br>
- `--tls-cert-file` 、 `--tls-private-key-file` ：设置服务证书和密钥文件。如果没有指定的话，会生成一个自签名证书，但是在生产环境中建议使用非自签名证书。

Additionally, Metrics Server defines a number of flags for configuring its behavior:<br>
此外，`metrics-server` 还定义了一些用于配置其行为的标记：

- `--metric-resolution=<duration>`: the interval at which metrics will be scraped from Kubelets (defaults to 60s).<br>
- `--metric-resolution=<duration>` ：从 `Kubelet` 中获取指标的时间间隔，默认为60秒。

- `--kubelet-insecure-tls`: skip verifying Kubelet CA certificates. Not recommended for production usage, but can be useful in test clusters with self-signed Kubelet serving certificates.<br>
- `--kubelet-insecure-tls` ：跳过对 `Kubelet CA证书` 的验证。生产环境中不建议这么使用，但是在具有自签名 `Kubelet 服务证书` 的测试集群中非常有用。

- `--kubelet-port`: the port to use to connect to the Kubelet (defaults to the default secure Kubelet port, 10250).<br>
- `--kubelet-port` ：用于连接 `Kubelet` 的端口，默认为 `Kubelet` 的默认安全端口10250。

- `--kubelet-preferred-address-types`: the order in which to consider different Kubelet node address types when connecting to Kubelet. Functions similarly to the flag of the same name on the API server.<br>
- `--kubelet-preferred-address-types` ：连接 `Kubelet` 时不同 `Kubelet` 节点地址类型的顺序。功能类似于API服务器上的同名标记。
