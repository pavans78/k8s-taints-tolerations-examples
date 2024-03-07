# k8s-taints-tolerations-examples
This repo contains the examples on the Taints and Tolerations. This explains about how the pod will be scheduled into node using the taints conditions.

## Taints:

Taints are applied to nodes in a Kubernetes cluster to repel pods from being scheduled on those nodes, except for pods that explicitly tolerate the taint. Taints are typically used to mark nodes with specific attributes or limitations, such as reserving certain nodes for particular workloads or preventing pods from being placed on nodes with specific hardware characteristics.

To taint a node, use the kubectl taint command. For example, to taint a node with key "gpu" and value "true", use the following command:

`kubectl taint nodes node1 gpu=true:NoSchedule`

Each taint consists of three parts:

`Key`: The key represents the name of the taint and is used to uniquely identify it.

`operator` : The operator will be `Equal` or `Exists`.

`Value`: An optional value associated with the taint key.

`Effect`: The effect determines how the taint affects pod scheduling.

And there are three possible values for the effect:

`NoSchedule`: Pods that do not tolerate this taint are not scheduled on the node; existing Pods are not evicted from the node.

`PreferNoSchedule`: Similar to NoSchedule, but the scheduler tries to avoid placing new pods on the tainted node unless necessary. 

`NoExecute`: 	Pods that do not tolerate this taint are not scheduled on the node; existing Pods are evicted from the node. The Pod is evicted from the node if it is already running on the node, and is not scheduled onto the node if it is not yet running on the node.

## Tolerations:

Tolerations are applied to pods and indicate that the pod can be scheduled on nodes with specific taints. A pod with toleration will only be scheduled on nodes that have a matching taint. By setting tolerations, you can make sure that certain pods are placed on nodes with specific attributes or restrictions, even if those nodes are tainted.

To tolerate a taint, you can specify toleration in the pod specification. For example, the following pod specification tolerates the taint "gpu=true" with a toleration period of 3600 seconds:

``` tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoExecute"
    tolerationSeconds: 3600
```
A toleration with NoExecute effect can specify an optional `tolerationSeconds`` field that dictates how long the pod will stay bound to the node after the taint is added. 

## Taints Effects:
### NoExecute

This affects pods that are already running on the node as follows:
Pods that do not tolerate the taint are evicted immediately
Pods that tolerate the taint without specifying tolerationSeconds in their toleration specification remain bound forever
Pods that tolerate the taint with a specified tolerationSeconds remain bound for the specified amount of time. After that time elapses, the node lifecycle controller evicts the Pods from the node.

### NoSchedule

No new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted.

### PreferNoSchedule

PreferNoSchedule is a "preference" or "soft" version of NoSchedule. The control plane will try to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed.

## Remove Taint

To remove the taint added by the command above, you can run:

`kubectl taint nodes node1 gpu=true:NoSchedule-`

For more information on the node affinity please refer this [link](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

