# OpenStack Cloud Controller Manager - OpenStack云控制器管理器

Thank you for visiting the `openstack-cloud-controller-manager` repository!<br>
感谢你访问 [`openstack-cloud-controller-manager`](https://github.com/kubernetes/cloud-provider-openstack) 仓库！

OpenStack Cloud Controller Manager - An external cloud controller manager for running kubernetes in an OpenStack cluster.<br>
OpenStack云控制器管理器 - 用于在OpenStack集群中运行Kubernetes的外置云控制器管理器。

## Introduction - 简介

External cloud providers were introduced as an Alpha feature in Kubernetes release 1.6.<br>
在Kubernetes 1.6版本中外置云提供器是作为Alpha特性来介绍的。

This repository contains an implementation of external cloud provider for OpenStack clusters.<br>
这个仓库中包含了OpenStack集群的外置云提供器的实现。

An external cloud provider is a kubernetes controller that runs cloud provider-specific loops required for the functioning of kubernetes.<br>
外置云提供器是一个Kubernetes控制器，这个控制器运行了Kubernetes工作所需的云控制器特定的循环。

These loops were originally a part of the `kube-controller-manager`, but they were tightly coupling the `kube-controller-manager` to cloud-provider specific code.<br>
这些循环原先是 `kube-controller-manager` 的一部分，但是这些循环紧紧地耦合了 `kube-controller-manager` 和云提供器特定的代码。

In order to free the kubernetes project of this dependency, the `cloud-controller-manager` was introduced.<br>
为了让Kubernetes项目摆脱这种依赖，于是就引入了 `cloud-controller-manager` 。

`cloud-controller-manager` allows cloud vendors and kubernetes core to evolve independent of each other.<br>
`cloud-controller-manager` 允许云供应商和Kubernetes内核独立发展。

In prior releases, the core Kubernetes code was dependent upon cloud provider-specific code for functionality.<br>
在以前的版本中，Kubernetes核心代码功能依赖云提供器特定的代码。

In future releases, code specific to cloud vendors should be maintained by the cloud vendor themselves, and linked to `cloud-controller-manager` while running Kubernetes.<br>
在未来的版本中，云供应商特定的代码应该由云供应商自己来维护，并在运行Kubernetes时连接到 `cloud-controller-manager` 。

As such, you must disable these controller loops in the `kube-controller-manager` if you are running the `openstack-cloud-controller-manager`.<br>
因此，如果你要运行 `openstack-cloud-controller-manager` 的话，你必须在 `kube-controller-manager` 中禁用这些控制器循环。

You can disable the controller loops by setting the `--cloud-provider` flag to `external` when starting the kube-controller-manager.<br>
你可以在启动 `kube-controller-manager` 时，通过把 `--cloud-provider` 标记设置为 `external` 来禁用控制器循环。

For more details, please see:<br>
更多详情，请参阅：

- <https://github.com/kubernetes/community/blob/master/keps/sig-cloud-provider/0002-cloud-controller-manager.md>
- <https://kubernetes.io/docs/tasks/administer-cluster/running-cloud-controller/#running-cloud-controller-manager>
- <https://kubernetes.io/docs/tasks/administer-cluster/developing-cloud-controller-manager/>

## Examples - 示例

Here are some examples of how you could leverage `openstack-cloud-controller-manager`:<br>
以下是一些使用 `openstack-cloud-controller-manager` 的示例：

- [loadbalancers](examples/loadbalancers/)

## Developing - 开发

`make` will build, test, and package this project.<br>
`make` 将会构建、测试并打包这个项目。

This project uses [go dep](https://golang.github.io/dep/) for dependency management.<br>
这个项目使用 [go dep](https://golang.github.io/dep/) 来管理依赖。

If you don't have a Go Environment setup, we also offer the ability to run make in a Docker Container.<br>
如果你没有设置Go环境，我们还提供了在Docker容器中运行make的功能。

The only requirement for this is that you have Docker installed and configured (of course).<br>
当然，其唯一要求是你已经安装并配置了Docker。

You don't need to have a Golang environment setup, and you don't need to follow rules in terms of directory structure for the code checkout.<br>
你不需要设置Golang环境，也不需要遵循代码签出的目录结构方面的规则。

To use this method, just call the `hack/make.sh` script with the desired argument: `hack/make.sh build` for example will run `make build` in a container.<br>
要使用这种方式，只需要使用期望的参数来调用 `hack/make.sh` 脚本，例如： `hack/make.sh build` 将会在容器中运行 `make build` 。

NOTE You MUST run the script from the root source directory as shown above, attempting to do something like `cd hack && make.sh build` will not work because we won't bind mount the source files into the container.<br>
注意：你必须在上述所示的源代码根目录中运行脚本，尝试执行像 `cd hack && make.sh build` 这样的操作是行不通的，因为我们不会把源文件绑定到容器中。

## License - 许可

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.<br>

You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)<br>

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.<br>

See the License for the specific language governing permissions and limitations under the License.<br>
