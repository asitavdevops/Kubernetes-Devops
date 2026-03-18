# Kubernetes-Devops (K8 concepts and All Projects)

**Docker vs Kubernetes – Why Kubernetes is Needed?**
Docker does not support the issues like mention below and which solution provided by K8s
1. **Single host issue**
Docker works on a single host (one server).
If that server goes down → all containers go down.
Note- Kubernetes solves this by using a cluster (group of nodes).
If one node fails → application runs on other nodes (high availability).
**2. No auto-healing**
In Docker, if a container crashes → it will not recover automatically.
Note- Kubernetes provides auto-healing using:
ReplicaSet / Deployment
It automatically restarts or replaces failed containers.

. No auto-scaling
Docker cannot handle traffic increase automatically.

👉 Kubernetes solves this using:

HPA (Horizontal Pod Autoscaler)

It increases or decreases pods based on traffic/load.

4. Lack of enterprise features
Docker alone does not provide:

Load balancing

Rolling updates

Service discovery

👉 Kubernetes provides all these enterprise-level features:

Load balancing

Rolling updates (no downtime deployment)

Service discovery

🔹 Real-world understanding

If I deploy an app using Docker on one server and it crashes → app goes down.

But in Kubernetes → app runs on multiple nodes, so it stays available.

During high traffic (like sale time), Docker cannot scale automatically.

Kubernetes automatically increases pods to handle load.

🔹 Final Interview Line

👉 Docker is used to create containers, but Kubernetes is used to manage containers at scale with features like auto-healing, auto-scaling, and high availability.
