Kubernetes Objects 
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

--------
Kubernetes Deployments

What is a Deployment?

A Deployment in Kubernetes is a higher-level object that manages Pods (and ReplicaSets.)
It provides a declarative way to describe your application’s desired state (for example, “I want 3 Pods running Nginx version 1.25”) and lets Kubernetes handle creating, updating, and maintaining that state automatically.

Why use a Deployment?
	•	Self-healing → If a Pod crashes (for any reason), Kubernetes replaces it automatically.
	•	Scaling → Easily increase or decrease the number of replicas.
	•	Rolling Updates → Update Pods to a new version with zero downtime.
	•	Rollbacks → Revert to a previous working version if something goes wrong.
	•	Declarative Management → You declare what you want, Kubernetes ensures it runs that way.


Key Concepts
	•	ReplicaSets: A Deployment manages ReplicaSets, which ensure a specific number of identical Pods are running at any given time.
	•	Rolling Updates: When you update the Deployment (for example, with a new container image), Kubernetes gradually replaces old Pods with new ones.
	•	Rollback: If an update fails, you can roll back to a previous version quickly.
	•	Scaling: You can change the number of replicas on demand to handle more or less traffic.

⸻

Common Use Cases
	•	Running stateless applications (web servers, APIs, microservices).
	•	Managing frequent application updates with zero downtime.
	•	Ensuring high availability by running multiple replicas of the same app.
	•	Integrating into CI/CD pipelines for automated deployments.

Official Kubernetes documentations:  

👉https://kubernetes.io/docs/concepts/workloads/pods/  

👉https://kubernetes.io/docs/concepts/overview/working-with-objects/  

👉https://kubernetes.io/docs/concepts/workloads/controllers/deployment/  
