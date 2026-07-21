Your Kubernetes Lab Setup
1. WSL (Windows Subsystem for Linux) ✅

Installed on: Windows

Purpose:

Provides a real Ubuntu Linux environment inside Windows.
This is where you'll write YAML files and run Linux commands.


2. Ubuntu (WSL Distribution) ✅

Installed inside: WSL


3. Docker Desktop ✅

Installed on: Windows

Purpose:

Provides the container runtime.
Minikube uses Docker Desktop to run the Kubernetes node.

Think of Docker Desktop as:

"The software that runs containers."

Without Docker Desktop, Minikube cannot create the Kubernetes node.

4. Minikube ✅

Installed on: Windows

Purpose:

Creates a single-node Kubernetes cluster on your laptop.

When you ran:

minikube start

Minikube created:

Kubernetes Cluster
        │
        ▼
Node (minikube)

This is your practice cluster.

5. kubectl (Ubuntu) ✅

Installed on: Ubuntu (WSL)

6. kubeconfig Configuration ✅

This was the final step.

We configured Ubuntu's kubectl to connect to the Minikube cluster running on Windows.

Without this configuration:

Ubuntu kubectl ❌ ----> Kubernetes Cluster

After configuration:

Ubuntu kubectl ✅ ----> Minikube Cluster
Final Architecture
+------------------------------------------------------+
|                 Windows 11                           |
|                                                      |
|  +------------------+                                |
|  | Docker Desktop   |                                |
|  +------------------+                                |
|           |                                          |
|           v                                          |
|  +------------------+                                |
|  |   Minikube       |                                |
|  | (Kubernetes)     |                                |
|  +------------------+                                |
|                                                      |
|      WSL                                              |
|      +----------------------------+                  |
|      | Ubuntu                     |                  |
|      |                            |                  |
|      | kubectl                    |                  |
|      | vi / nano                  |                  |
|      | YAML files                 |                  |
|      | Git                        |                  |
|      +----------------------------+                  |
+------------------------------------------------------+
Your Daily Workflow
Before starting
1. Start Docker Desktop
2. Open Ubuntu
3. minikube start
4. kubectl get nodes
During practice
Ubuntu Terminal

vi pod.yaml
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod nginx
kubectl logs nginx
After practice
minikube stop

That's it.

Responsibilities of Each Component
Component	Purpose
Windows-Hosts Docker Desktop and Minikube
Docker- Desktop	Runs containers and the Minikube node
Minikube-Creates a local Kubernetes cluster
WSL-Runs Ubuntu inside Windows
Ubuntu-	Your Linux working environment
kubectl-Communicates with the Kubernetes API server
YAML files-	Describe the Kubernetes resources you want



My suggestion is to save this explanation as ~/kubernetes/README.md in your Ubuntu workspace. Whenever you feel confused about the setup, you can quickly refer back to it. It will also serve as a nice reference if you rebuild your lab in the future. 🚀
