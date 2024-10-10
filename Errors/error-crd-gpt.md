The error you encountered indicates that Kubernetes could not find the Route resource in the networking.k8s.io/v1 API version. The resource Route is not a standard Kubernetes object under the default Kubernetes APIs but is typically used in OpenShift environments (OpenShift Route) or other similar platforms.

To resolve this issue, follow these steps:

1. Check if you are using OpenShift:

If you’re using OpenShift, you should ensure that the OpenShift Routes are available by confirming the relevant Custom Resource Definitions (CRDs). You can verify CRDs with:

kubectl get crd

If you don’t see anything, you likely don’t have the required CRD installed or you’re not using an OpenShift environment.

2. Use Ingress Instead of Route in Kubernetes:

If you’re using pure Kubernetes (like in Minikube or other K8s distributions), replace Route with Ingress in your YAML file, as Ingress is the Kubernetes equivalent of routing HTTP traffic.

Here’s how you might update your frontend-route.yaml to use Ingress instead of Route:

Example YAML for Ingress:

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: frontend-ingress
  namespace: monitoring-testing-october24
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: frontend.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend-service
            port:
              number: 80

3. Ensure Ingress Controller is Installed:

To use Ingress, ensure that your Kubernetes cluster has an ingress controller installed (like NGINX Ingress). If not, you can install one with Minikube, for example:

minikube addons enable ingress

For other environments, you might need to install an ingress controller manually.

4. OpenShift Route (if using OpenShift):

If you’re using OpenShift, ensure the Route CRD is installed, as OpenShift uses the Route object for HTTP routing. The Route object is not part of vanilla Kubernetes and is part of OpenShift’s extended features.

Check if you’re in an OpenShift environment with:

oc version

Let me know if you’re using OpenShift, and I can assist you in setting up the CRDs or modifying the configuration for your environment. get crd