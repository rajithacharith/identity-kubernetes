# identity-kubernetes
Simple two pod IS deployment using kubernetes

# Prerequisite
* [kubectl](https://kubernetes.io/docs/tasks/tools/)
* [minikube](https://minikube.sigs.k8s.io/docs/start/)
* virtualbox

# STEPS

1. Start minikube cluster

    `minikube start — kubernetes-version v1.18.1 — vm-driver=virtualbox — cpus 4 — memory 8192`

2. Enable ingress in minikube

    `minikube addons enable ingress`

3. Cluster partitioning by adding a namespace 

    `kubectl apply -f identity-namespace.yaml`

4. Create a service account for wso2is

    `kubectl apply -f identity-svc.yaml`

5. Add a configmap for WSO2 is deployment.toml

    `kubectl apply -f identity-server-conf.yaml`

6. Create a wso2is service using

    `kubectl apply -f identity-wso2is-service.yaml`

7. Create ingress and add ingress rules 

    `kubectl apply -f identity-server-ingress.yaml`

8. Declare the Desired State of A Deployment

    `kubectl apply -f identity-server-deployment.yaml`

9. Add wso2is <minkube ip> to /etc/hosts

    `kubectl get ingress -n wso2`

    Get IP address and update /etc/hosts

10. Go to  https://wso2is/carbon/admin/login.jsp