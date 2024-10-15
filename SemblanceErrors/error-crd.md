@rifaterdemsahin ➜ /workspaces/thanoswithdocker/Code (main) $ kubectl create -f frontend-route.yaml -n monitoring-testing-october24
error: resource mapping not found for name: "monitoring-testing-october24" namespace: "monitoring-testing-october24" from "frontend-route.yaml": no matches for kind "Route" in version "networking.k8s.io/v1"
ensure CRDs are installed first
================
kubectl get crd

@rifaterdemsahin ➜ /workspaces/thanoswithdocker/Code (main) $ kubectl get crd
No resources found
@rifaterdemsahin ➜ /workspaces/thanoswithdocker/Code (main) $ 