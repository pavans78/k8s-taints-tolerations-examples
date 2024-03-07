# k8s-taints-tolerations-examples
This repo contains the examples on the Taints and Tolerations. This explains about how the pod will be scheduled into node using the taints conditions.

To taint a node, use the kubectl taint command. For example, to taint a node with key "gpu" and value "true", use the following command:

`kubectl taint nodes node1 gpu=true:NoSchedule`

To tolerate a taint, you can specify toleration in the pod specification. For example, the following pod specification tolerates the taint "gpu=true" with a toleration period of 3600 seconds:

`  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoExecute"
    tolerationSeconds: 3600 `

Each taint consists of three parts:

`Key`: The key represents the name of the taint and is used to uniquely identify it.
`operator` : The operator will be `Equal` or `Exists`
`Value`: An optional value associated with the taint key.
`Effect`: The effect determines how the taint affects pod scheduling.

And there are three possible values for the effect:

`NoSchedule`: Pods that do not tolerate this taint are not scheduled on the node; existing Pods are not evicted from the node.
`PreferNoSchedule`: Similar to NoSchedule, but the scheduler tries to avoid placing new pods on the tainted node unless necessary. 
`NoExecute`: 	The Pod is evicted from the node if it is already running on the node, and is not scheduled onto the node if it is not yet running on the node.

To remove the taint added by the command above, you can run:

`kubectl taint nodes node1 gpu=true:NoSchedule-`

For more information on the node affinity please refer this [link](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
