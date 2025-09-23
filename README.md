Kubernetes Objects 
https://kubernetes.io/docs/concepts/overview/working-with-objects/
	•	A Kubernetes Object is a persistent record in the Kubernetes cluster.
	•	It defines the desired state of some part of the system (what should be running, how many replicas, configuration, etc.).
	•	Objects are stored in the cluster’s database (etcd) and managed by the Kubernetes API server.
	•	Every object has:
	•	Spec → what you want (desired state)
	•	Status → what is actually running (current state)

Examples of Kubernetes Objects:
	•	Workload: Pod, ReplicaSet, Deployment, StatefulSet, DaemonSet
	•	Networking: Service, Ingress, NetworkPolicy
	•	Config & Storage: ConfigMap, Secret, PersistentVolume, PersistentVolumeClaim
	•	Cluster/Namespace: Node, Namespace, Role, RoleBinding


-------
Pods
 https://kubernetes.io/docs/concepts/workloads/pods/
	•	A Pod is the smallest deployable unit in Kubernetes.
	•	It is a wrapper around one or more containers.
	•	Containers in a Pod:
	•	Share the same network namespace (IP, port space)
	•	Can share storage volumes
	•	Pods are ephemeral: if a Pod dies, Kubernetes can create a new one, but it will have a new identity (new IP).
	•	Higher-level controllers like Deployments or ReplicaSets are used to manage Pods automatically.

Key points:
	•	Kubernetes does not run containers directly → it runs Pods.
	•	Most Pods run a single container, but multi-container Pods are used for tightly coupled tasks (e.g., main app + sidecar logger).