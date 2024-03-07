Here are some guidelines for when to use taint, affinity, and node selector in Kubernetes:

1. A combination of Taints & Tolerations and Node Affinity rules can be used together to completely dedicate nodes for specific pods. We use Taints & Tolerations to prevent other pods from being scheduled on the desired nodes and then we use Node Affinity to have our pods scheduled on the desired nodes.

2. Taint should be used when you want to mark a node as unavailable for certain pods. For example, you can use taint to mark a node as "maintenance" and prevent pods from being scheduled on the node while it is undergoing maintenance.
3. Node affinity should be used when you want to specify which nodes a pod should or should not be scheduled on based on node labels. Node affinity provides more fine-grained control over pod scheduling compared to node selector and allows you to specify complex rules for pod scheduling based on multiple node labels.
4. Pod affinity should be used when you want to specify which pods a pod should or should not be scheduled with based on labels. Pod affinity can be used to ensure that certain pods are co-located on the same node or to ensure that certain pods are separated from each other.
5. Node selector should be used when you want to specify which nodes a pod should be scheduled on based on node labels, but do not need the fine-grained control provided by node affinity. Node selector is a simpler and more primitive mechanism compared to node affinity and is sufficient for many use cases.

In general, you should use taint and affinity when you need to specify complex rules for pod scheduling based on node attributes and use node selector when you only need to specify simple rules based on node labels.