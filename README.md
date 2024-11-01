# Kubernetes Demos and Assignments 

This repository contains Kubernetes demos and assignments from my training at the National Telecommunication Institute (NTI). 

## Lab 1 - Kubernetes Basics

1. Install a Kubernetes cluster (use Minikube or [killercoda Kubernetes Playground](https://killercoda.com/playgrounds/scenario/kubernetes)).
![l1](/Lab%201%20-%20Kubernetes%20Basics/1.png)
2. Create a pod named `redis` using the `redis` image.
![l1](/Lab%201%20-%20Kubernetes%20Basics/2.png)
3. Create a pod named `nginx` using the image `nginx123` with a pod-definition YAML file.
![l1](/Lab%201%20-%20Kubernetes%20Basics/3.png)
4. Check the status of the `nginx` pod.
![l1](/Lab%201%20-%20Kubernetes%20Basics/4.png)
5. Update the `nginx` pod's image to `nginx` and check the status again.
![l1](/Lab%201%20-%20Kubernetes%20Basics/5.png)
6. Determine the number of ReplicaSets in the system.
![l1](/Lab%201%20-%20Kubernetes%20Basics/6.png)
7. Create a ReplicaSet named `replica-set-1` with the `busybox` image and 3 replicas.
![l1](/Lab%201%20-%20Kubernetes%20Basics/7.png)
8. Scale `replica-set-1` to 5 pods.
![l1](/Lab%201%20-%20Kubernetes%20Basics/8.png)
9. Verify the number of ready pods in `replica-set-1`.
![l1](/Lab%201%20-%20Kubernetes%20Basics/9.png)
10. Delete one pod from `replica-set-1` and check the pod count again. Explain why there are still 5 pods.
![l1](/Lab%201%20-%20Kubernetes%20Basics/10.png)
11. Determine the count of Deployments and ReplicaSets in the system.
![l1](/Lab%201%20-%20Kubernetes%20Basics/11.png)
12. Create a Deployment named `deployment-1` with the `busybox` image and 3 replicas.
![l1](/Lab%201%20-%20Kubernetes%20Basics/12.png)
13. Check the count of Deployments and ReplicaSets now.
![l1](/Lab%201%20-%20Kubernetes%20Basics/13.png)
14. Verify the number of ready pods in `deployment-1`.
![l1](/Lab%201%20-%20Kubernetes%20Basics/14.png)
15. Update `deployment-1`'s image to `nginx` and verify the ready pod count.
![l1](/Lab%201%20-%20Kubernetes%20Basics/15.png)
16. Run `kubectl describe deployment deployment-1` to view events. Note the deployment strategy.
![l1](/Lab%201%20-%20Kubernetes%20Basics/16.png)
17. Roll back the upgrade of `deployment-1`. Check the image used in `deployment-1`.
![l1](/Lab%201%20-%20Kubernetes%20Basics/17.png)
18. Create a Deployment named `nginx-deployment` with the image `nginx:latest`, app labels `app: nginx-app` and `type: front-end`, container name `nginx-container`, and 3 replicas.
![l1](/Lab%201%20-%20Kubernetes%20Basics/18.png)

---

## Lab 2 - Namespaces and Resource Management

1. List the existing namespaces.
![l2](Lab 2 - Namespaces and Resource Management\2.png)
2. Find the number of pods in the `kube-system` namespace.
3. Create a Deployment in the `finance` namespace with:
   - Name: `beta`
   - Image: `redis`
   - Replicas: 2
   - Resource Requests: CPU: `500m`, Memory: `1G`
   - Resource Limits: CPU: `1`, Memory: `2G`
4. Label the master node with `color=blue`.
5. Create a Deployment named `blue` with the `nginx` image, 3 replicas, and Node Affinity to the master node with `color=blue`.
6. Create a namespace `iti` with a resource quota limiting pods to `2`.
7. In the `iti` namespace, create a Deployment named `nginx` with the `nginx` image and 3 replicas. Check the created pod count and explain.
8. Set a LimitRange for the `gold` namespace with memory limits (`500 Mi`) and requests (`200 Mi`).
9. Create a pod named `ingot` in the `gold` namespace.

---

## Lab 3 - DaemonSets and Services

1. List all DaemonSets across namespaces.
2. Identify DaemonSets in the `kube-system` namespace.
3. Check the image used by the `kube-proxy` DaemonSet.
4. Deploy a DaemonSet with the following:
   - Name: `elasticsearch`
   - Namespace: `kube-system`
   - Image: `k8s.gcr.io/fluentd-elasticsearch:1.20`
5. Deploy a pod `nginx-pod` with the `nginx:alpine` image and label `tier=backend`.
6. Deploy a test pod with the `nginx:alpine` image.
7. Create a service `backend-service` to expose the backend app on port `80`.
8. Curl `backend-service` from the test pod and note the response.
9. Deploy a Deployment named `web-app` with the `nginx` image and 2 replicas.
10. Expose `web-app` as a NodePort service `web-app-service` on port `80` and node port `30082`.
11. Access the `web-app` via the node.
12. Count the static pods in the cluster.
13. Identify the nodes running the static pods.

---

## Lab 4 - ConfigMaps, Secrets, and Persistent Storage

1. Count the existing ConfigMaps.
2. Create a ConfigMap named `webapp-config-map` with data `APP_COLOR=darkblue`.
3. Create a pod `webapp-color` using the `nginx` image and attach the ConfigMap.
4. Count the existing secrets.
5. Check the number of keys in the `default-token` secret.
6. Create a pod `db-pod` with the `mysql:5.7` image and check its status.
7. Explain why `db-pod` status is not ready.
8. Create a secret `db-secret` with:
   - `MYSQL_DATABASE`: `sql01`
   - `MYSQL_USER`: `user1`
   - `MYSQL_PASSWORD`: `password`
   - `MYSQL_ROOT_PASSWORD`: `password123`
9. Configure `db-pod` to use the `db-secret` for environment variables.
10. Create a multi-container pod `yellow` with:
    - `lemon` container (image: `busybox`)
    - `gold` container (image: `redis`)
11. Create a pod `red` with `redis` image and an init container that uses `busybox` and sleeps for 20 seconds.
12. Create a pod `print-envars-greeting` with:
    - Container name: `print-env-container` (image: `bash`)
    - Environment variables: `GREETING=Welcome to`, `COMPANY=DevOps`, `GROUP=Industries`
    - Command to echo `"$(GREETING) $(COMPANY) $(GROUP)"`
    - Use `kubectl logs` to view output.
13. Locate the default kubeconfig file.
14. Check the clusters defined in the kubeconfig file.
15. Identify the user configured in the current context.
16. Create a PersistentVolume with:
    - Name: `pv-log`
    - Storage: `100Mi`
    - Access Modes: `ReadWriteMany`
    - Host Path: `/pv/log`
17. Create a PersistentVolumeClaim:
    - Name: `claim-log-1`
    - Storage Request: `50Mi`
    - Access Modes: `ReadWriteMany`
18. Create a pod `webapp` with `nginx` image using the `claim-log-1` PersistentVolumeClaim mounted at `/var/log/nginx`.

---

## Lab 5 - Multi-Container Pods and Shared Storage

1. Create a pod with 3 containers:
   - Configure the first two containers to write to a shared file.
   - Configure the third container to read and display the file content using `cat`.
   - Use an ephemeral or persistent volume as necessary.

## Setup Instructions

To run the demos, ensure you have Docker and Docker Compose installed. Clone the repository and navigate to the directory:

```bash
git clone https://github.com/Tarek-Ehab/NTI-Kubernetes-Demos.git
cd NTI-Docker-Demos