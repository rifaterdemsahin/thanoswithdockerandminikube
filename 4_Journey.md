Thanos and Helm Chart Testing Project

This project is designed to test the deployment and functionality of Thanos using Bitnami Helm charts.

## Table of Contents

- Prerequisites
- Installation
- Usage
- Testing
- Contributing
- License

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Kubernetes cluster (v1.19+)
- Helm (v3.0+)
- kubectl (v1.19+)

## Installation

1. **Add Bitnami Helm Repository:**

    ```sh
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm repo update
    ```

    ```
        @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ helm repo add bitnami https://charts.bitnami.com/bitnami
        "bitnami" has been added to your repositories
        @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ helm repo update
        Hang tight while we grab the latest from your chart repositories...
        ...Successfully got an update from the "bitnami" chart repository
        Update Complete. ⎈Happy Helming!⎈
        @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ 
    ```

2. **Install Thanos using Bitnami Helm Chart:**

    ```sh
         Cd 4_Symbols
         minikube start
         kubectl create namespace monitoring-testing-october24
         helm install my-release oci://registry-1.docker.io/bitnamicharts/thanos --values 1_values.yaml --namespace monitoring-testing-october24
         helm uninstall my-release 
         kubectl get pods -n monitoring-testing-october24
    ```

# Output

    ```sh
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube/4_Symbols (main) $ kubectl create namespace monitoring-testing-october24
    namespace/monitoring-testing-october24 created
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube/4_Symbols (main) $ helm install my-release oci://registry-1.docker.io/bitnamicharts/thanos --values 1_values.yaml --namespace monitoring-testing-october24
    Pulled: registry-1.docker.io/bitnamicharts/thanos:15.7.28
    Digest: sha256:4f8897dd464327693cbecc524082282face70e5142e41fadd6a8db1ddfc97987
    NAME: my-release
    LAST DEPLOYED: Tue Oct 15 19:13:29 2024
    NAMESPACE: monitoring-testing-october24
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    CHART NAME: thanos
    CHART VERSION: 15.7.28
    APP VERSION: 0.36.1

    ** Please be patient while the chart is being deployed **

    Thanos chart was deployed enabling the following components:
    - Thanos Query

    Thanos Query can be accessed through following DNS name from within your cluster:

        my-release-thanos-query.monitoring-testing-october24.svc.cluster.local (port 9090)

    To access Thanos Query from outside the cluster execute the following commands:

    1. Get the Thanos Query URL by running these commands:

        export SERVICE_PORT=$(kubectl get --namespace monitoring-testing-october24 -o jsonpath="{.spec.ports[0].port}" services my-release-thanos-query)
        kubectl port-forward --namespace monitoring-testing-october24 svc/my-release-thanos-query ${SERVICE_PORT}:${SERVICE_PORT} &
        echo "http://127.0.0.1:${SERVICE_PORT}"

    2. Open a browser and access Thanos Query using the obtained URL.

    WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
      - query.resources
      - queryFrontend.resources
    +info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube/4_Symbols (main) $ 
    ```

## Usage

Once Thanos is installed, you can interact with it using `kubectl` and Helm commands. For example:
If you want labels add the labels
- **Check the status of the Thanos pods:**

    ```sh
    kubectl get pods -n monitoring-testing-october24
    ```
    ## Output

    ```sh
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube/4_Symbols (main) $ kubectl get pods -n monitoring-testing-october24
    NAME                                                READY   STATUS    RESTARTS   AGE
    my-release-thanos-query-6cf69d9499-zdvq9            1/1     Running   0          10m
    my-release-thanos-query-frontend-55c47f5b95-9txh5   1/1     Running   0          10m
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube/4_Symbols (main) $ 
    ```



- **Access Thanos Query UI:**

    ```sh
    kubectl get svc -n monitoring-testing-october24
    kubectl port-forward svc/my-release-thanos-query 9090:9090 -n monitoring-testing-october24
    ```

    ## Output

    ```sh
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ kubectl get svc -n monitoring-testing-october24
    NAME                               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE
    my-release-thanos-query            ClusterIP   10.105.173.208   <none>        9090/TCP    14m
    my-release-thanos-query-frontend   ClusterIP   10.108.97.142    <none>        9090/TCP    14m
    my-release-thanos-query-grpc       ClusterIP   10.110.250.28    <none>        10901/TCP   14m
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ kubectl port-forward svc/my-release-thanos-query 9090:9090 -n monitoring-testing-october24
    Forwarding from 127.0.0.1:9090 -> 10902
    Forwarding from [::1]:9090 -> 10902
    ```

    ## Browse
    
    ```
    Then open your browser and go to loadbalances codeppaces url in the ports
    example : https://fuzzy-broccoli-vwrx9j76wqfww5-9090.app.github.dev/stores
    Ingress and service magic
    ```

## Testing

To test the Thanos deployment, you can use the following steps:

1. **Run basic tests:**

    ```sh
    kubectl get all -n monitoring-testing-october24
    ```
    ## Output

    ```sh
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ kubectl get all -n monitoring-testing-october24
    NAME                                                    READY   STATUS    RESTARTS   AGE
    pod/my-release-thanos-query-6cf69d9499-zdvq9            1/1     Running   0          22m
    pod/my-release-thanos-query-frontend-55c47f5b95-9txh5   1/1     Running   0          22m

    NAME                                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE
    service/my-release-thanos-query            ClusterIP   10.105.173.208   <none>        9090/TCP    22m
    service/my-release-thanos-query-frontend   ClusterIP   10.108.97.142    <none>        9090/TCP    22m
    service/my-release-thanos-query-grpc       ClusterIP   10.110.250.28    <none>        10901/TCP   22m

    NAME                                               READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/my-release-thanos-query            1/1     1            1           22m
    deployment.apps/my-release-thanos-query-frontend   1/1     1            1           22m

    NAME                                                          DESIRED   CURRENT   READY   AGE
    replicaset.apps/my-release-thanos-query-6cf69d9499            1         1         1       22m
    replicaset.apps/my-release-thanos-query-frontend-55c47f5b95   1         1         1       22m
    @rifaterdemsahin ➜ /workspaces/thanoswithdockerandminikube (main) $ 
    ```

    2. **Check logs for any errors:**

    ```sh
    kubectl logs -p my-release-thanos-query-6cf69d9499-zdvq9 -n monitoring-testing-october24
    ```

. REceive router
. Front end route to get installed
cd /workspaces/thanoswithdocker/Code

Openshift uses the route
   kubectl create -f frontend-route.yaml -n monitoring-testing-october24
   kubectl create -f receive-route.yaml -n monitoring-testing-october24

Minikube uses > port forwarding 
   kubectl create -f receive-config.yaml -n monitoring-testing-october24

. Install Certificates

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
```

Feel free to customize this template to better fit your project's specific needs. If you have any other requirements or need further assistance, just let me know!

-------------------------------------------------------------------------------------------

