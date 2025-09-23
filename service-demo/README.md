Kubernetes Services – Complete Guide
📖 Overview

In Kubernetes, a Service is an abstraction that defines a logical set of Pods and a policy by which to access them.
Since Pods are ephemeral and their IP addresses can change, Services provide a stable network identity (DNS name & IP) to reliably communicate between microservices.

⚡ Why Services?

Pods are short-lived and can be rescheduled → IPs keep changing.

Services ensure discoverability & reliability.

They support load balancing, scaling, and service discovery.

🔑 Types of Kubernetes Services
1. ClusterIP (Default Service Type)

Exposes the Service inside the cluster only.

Cannot be accessed directly from outside.

Useful for internal microservice communication.

✅ Use Case

A backend database (MySQL, MongoDB) accessible only to application Pods.

Example: frontend → backend API communication.

📜 Example YAML
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP

2. NodePort

Exposes the Service on a static port (30000–32767) on each Node’s IP.

External traffic → NodeIP:NodePort → Service → Pod.

Usually used for development & testing, not production.

✅ Use Case

Exposing a demo app on Minikube (http://<NodeIP>:<NodePort>).

Running services locally for debugging.

📜 Example YAML
apiVersion: v1
kind: Service
metadata:
  name: nodeport-service
spec:
  selector:
    app: demo
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30080
  type: NodePort

3. LoadBalancer

Exposes the Service externally using cloud provider’s Load Balancer.

Allocates a public IP that routes traffic → NodePort → Pods.

Used in production deployments on cloud (AWS, GCP, Azure).

✅ Use Case

A web application exposed to the internet with auto-scaling.

Example: myapp.example.com available worldwide.

📜 Example YAML
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
spec:
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 8080
  type: LoadBalancer

4. ExternalName

Maps a Service to an external DNS name.

No proxying, just a CNAME record in DNS.

Used to integrate with external services (like SaaS or external DB).

✅ Use Case

Pointing to an external MySQL DB, mysql.example.com.

Accessing third-party APIs from within the cluster.

📜 Example YAML
apiVersion: v1
kind: Service
metadata:
  name: external-db
spec:
  type: ExternalName
  externalName: mysql.example.com
  ports:
    - port: 3306

🔄 Real-Time Example Flow
Scenario: E-Commerce App (Minikube + Cloud)

Frontend (React/Angular) → exposed via LoadBalancer (public access).

Backend (Spring Boot/Node.js API) → exposed via ClusterIP (internal-only).

Payments Gateway (External API) → connected via ExternalName.

Testing Service (Minikube local run) → exposed via NodePort.

🛠️ Demo Commands
Check Services
kubectl get svc

Port Forward for Local Debugging
kubectl port-forward svc/backend-service 8080:80

Curl Inside Cluster (Testing Service-to-Service)
kubectl run curl --rm -it --image=curlimages/curl --restart=Never -- sh
# Inside container
curl http://backend-service:80

🚀 Summary
Service Type	Scope	External Access	Typical Use Case
ClusterIP	Internal	❌	Backend DB, Internal APIs
NodePort	Node-level	✅ (NodeIP:Port)	Local testing with Minikube
LoadBalancer	Cloud Provider LB	✅	Production web apps
ExternalName	DNS Alias	✅ (External DNS)	SaaS APIs, External DBs