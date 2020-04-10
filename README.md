# HowToStart
Documentation about how codes build kubernetes<br/>
The overall way that things are designed is as follows...<br/>
There are 2 main github organization<br/>
- https://github.com/kubernetes/kuberentes
- https://github.com/kubernetes-sigs/kuberentes-sigs

Some of the main repos in the kubernetes org are the following:<br/>
The main org, kubernetes, has code and documentation supporting the core Kubernetes project that lives in k/k https://github.com/kubernetes/kubernetes<br/>
https://github.com/kubernetes/community has all the documentation about the Kubernetes community, how it works, what sigs there are, what they do, etc, etc.<br/>
https://github.com/kubernetes/website has the kubernetes documentation - how to run it, how to use it, everything living in https://kubernetes.io/<br/>
https://github.com/kubernetes/test-infra has all the documentation and code supporting testing and CI.<br/>
The kubernetes-sigs organization stores all other projects related to kubernetes but not part of or strictly related to core kubernetes. <br/>
https://github.com/kubernetes/component-base in core repo there is imported code of this repo, it contains core package structure of Kubernetes<br/>
## Core code of Kubernetes
- api: contains openapi and api violation of Kubernetes, openapi used to generate violation rules of all Kubernetes components. and reference Github repo is : https://github.com/kubernetes/kube-openapi/tree/master/pkg/generators/rules

- build
- cluster
- cmd path contains cmds(kubelet, kubectl, kube-proxy,..)
- docs
- hack
- logo
- pkg
- plugin
- staging
- test
- vendor
