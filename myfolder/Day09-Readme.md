Service Mesh:

provide gateway to route traffic for services
Istio tool : popular service mesh tool

envoy: sidecar container/proxy that allows ingress/egress traffic
Istiod: Istio control plane
        provide service discovery
        configuration and certificate management
        components:
        - Pilot: configuring proxies at runtime
        - Citadel: Certificate issuance and rotation
        - Galley: validating, ingesting, aggregating, transforming n distributing config within istio
Operator: operate service mesh (kiali)

https://istio.io/latest/docs/setup/platform-setup/kind/

mkdir istio

https://istio.io/latest/docs/setup/getting-started/

Install zip and extract:
https://github.com/istio/istio/releases/tag/1.29.0

Install Istio:
    istioctl install -f samples/bookinfo/demo-profile-no-gateways.yaml -y

Namespace:
    kubectl label namespace default istio-injection=enabled

Install the Kubernetes Gateway API CRDs
    kubectl get crd gateways.gateway.networking.k8s.io >nul 2>&1 || kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.4.0" | kubectl apply -f -

Deploy Sample application
    kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
    kubectl get pods
    kubectl get svc

Open the application to outside traffic
    kubectl apply -f samples/bookinfo/gateway-api/bookinfo-gateway.yaml
    kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default (change service type to cluster)
    kubectl get gateway

Access the application
    kubectl port-forward svc/bookinfo-gateway-istio 8080:80

View the dashboard
    Install Kiali and the other addons
        kubectl apply -f samples/addons/kiali.yaml
        kubectl rollout status deployment/kiali -n istio-system

    Access Kiali dashboard
        istioctl dashboard kiali


==============================================================
What is Service Mesh?
A service mesh is a dedicated infrastructure layer for handling service-to-service communication in microservices architectures.

Key components:
    Data Plane:  Composed of lightweight sidecar proxies (e.g., Envoy) deployed alongside each application instance. These       proxies handle all network traffic
    Control Plane: Manages and configures the proxies/Policy enforcement/Service discovery

What is the role of the sidecar proxy (e.g., Envoy)?
Answer: The sidecar intercepts all incoming and outgoing network traffic for the service
        apply policies, collect telemetry, enable mTLS, and perform traffic management.

How does a service mesh enable mTLS (Mutual TLS)?
Answer: The control plane issues certificates to each proxy. Proxies then handle encryption, decryption, and certificate rotation or service-to-service communication, ensuring authenticated and encrypted traffic without application-level logic.

What are the key differences between Istio and Linkerd?
Answer: Istio is known for being feature-rich, providing complex traffic management and extensive integration, but it is more complex to manage. Linkerd focuses on simplicity, being lightweight, and performance. 

What is the difference between an API Gateway and a Service Mesh?
Answer: An API Gateway manages traffic entering the cluster from the outside (north-south traffic). A Service Mesh handles communication between services inside the cluster (east-west traffic).
