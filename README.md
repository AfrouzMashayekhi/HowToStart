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

- build, build kubernetes using docker for different OS or golang installtion on your local machine.
- cluster it's deprecated path that contain cluster config(networking, DNS, nodes, and control plane components)
- cmd path contains cmds(kubelet, kubectl, kube-proxy,..) base code
- hack lots of scripts for e2e test verifcation, update and generate other path contents.
- pkg all go packages that used in kubernetes
- plugin  ?
- staging it is a staging area for Kubernetes and all Kubernetes repositories
- test all the kubernetes test  e2e node, e2e kubeadm, integrations..
- third_party forked repos that use in kuber? and other third_party repos.
- translation a workflow for adding translition to Kubernetes componenets
- vendor ?
### Staging Path
In this path you will find everything =))
First of all I tried to find where is "event" kind so I find staging/src/k8s.io/api/events/v1beta1 it's logical event is a kind so in api repo at events find events/v1beta1 let see what this little black box has

we want to resolve [this issue](https://github.com/kubernetes/kubernetes/issues/89689) so we want `firstTimestamp` field
so we have 
```
type Event struct {
...
	DeprecatedFirstTimestamp metav1.Time `json:"deprecatedFirstTimestamp,omitempty" protobuf:"bytes,13,opt,name=deprecatedFirstTimestamp"`
	// Deprecated field assuring backward compatibility with core.v1 Event type
	// +optional
	DeprecatedLastTimestamp metav1.Time `json:"deprecatedLastTimestamp,omitempty" protobuf:"bytes,14,opt,name=deprecatedLastTimestamp"`
	// Deprecated field assuring backward compatibility with core.v1 Event type
	// +optional
	DeprecatedCount int32 `json:"deprecatedCount,omitempty" protobuf:"varint,15,opt,name=deprecatedCount"`
}
```
lets find out where is default-schduler:(
I found another path which make diffrent events https://github.com/kubernetes/client-go/blob/master/tools/record/event.go
now what should I do :(
