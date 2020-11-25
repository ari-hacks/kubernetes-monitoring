# Kubernetes Monitoring


### TODOS
 ➜ [Install Prometheus Operator](#install-prometheus)

 ➜ [Configure Grafana Dashboard](#configure-grafana-dashboard)


### Requirements
- Kubernetes/kubectl 
- helm3

Note: This setup is using [kubespray](https://github.com/kubernetes-sigs/kubespray) and the sock shop demo microservice. For cluster setup and microservice deployment instructions [click here](https://github.com/ari-hacks/kubernetes-chaos-sandbox/blob/main/gremlin/README.md#create-kubespray-cluster)

### Install Prometheus

1. Create a namespace for prometheus
   
   ```BASH
    kubectl create namespace monitoring
   ```

2. Get repo info
    ```BASH
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

    helm repo add stable https://charts.helm.sh/stable

    helm repo update
    ```
3. Install prometheus operator with helm charts
   
    ```BASH
    helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring

    ```  

4. Verify pods are running
   
    ```BASH
    kubectl get pods -n monitoring
    ```
5. Access the dashboard
   
   ```BASH
    kubectl port-forward $(kubectl get pods -n monitoring -o name | grep grafana) 8080:3000 -n monitoring
    #defualt login admin | prom-operator
    ```


### Configure Grafana Dashboard

1. Once logged in navigate to the home button and check out the different metrics available
   
    ```BASH
    #ex/
    Kubernetes/Compute Resources/Namespace(Pods)
    ```
