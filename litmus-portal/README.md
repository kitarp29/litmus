## **ChaosCenter**

ChaosCenter provides console and UI experience for managing, monitoring, and events around chaos workflows. Chaos workflows consist of a sequence of experiments run together to achieve the objective of introducing some kind of fault into an application or the Kubernetes platform.

## **Platforms Support**

- GKE
- EKS
- Okteto Cloud
- AKS
- K3S
- Civo Cloud
- Kublr
- Minikube
- KIND

## **Pre-requisites**

- Kubernetes 1.17 or later.

## **Installation**

#### Applying k8s manifest

> Litmus-2.8.0 (Stable) Cluster Scope manifest

```bash
kubectl apply -f https://raw.githubusercontent.com/litmuschaos/litmus/2.8.0/mkdocs/docs/2.8.0/litmus-2.8.0.yaml
```

Or

> Master (Latest) Cluster scope. Install in litmus namespace by default.

```bash
kubectl apply -f https://raw.githubusercontent.com/litmuschaos/litmus/master/litmus-portal/cluster-k8s-manifest.yml
```

Or

> Master (Latest) Namespaced scope.

```bash
#Create a namespace eg: litmus
kubectl create ns litmus
#Install CRDs, if SELF_AGENT env is set to TRUE
kubectl apply -f https://raw.githubusercontent.com/litmuschaos/litmus/2.8.0/litmus-portal/litmus-portal-crds.yml
#Install ChaosCenter
kubectl apply -f https://raw.githubusercontent.com/litmuschaos/litmus/master/litmus-portal/namespace-k8s-manifest.yml -n litmus
```

#### Configuration Options for Cluster scope.

- `litmus-portal-operations-config` configmap.

  > `AgentNamespace: litmus`

- All environment variables.


#### Retrieving external url to access the litmus portal

##### GKE/Okteto Cloud/EKS

```bash
export NODE_NAME=$(kubectl -n $LITMUS_PORTAL_NAMESPACE get pod  -l "component=litmusportal-frontend" -o=jsonpath='{.items[*].spec.nodeName}')
export EXTERNAL_IP=$(kubectl -n $LITMUS_PORTAL_NAMESPACE get nodes $NODE_NAME -o jsonpath='{.status.addresses[?(@.type=="ExternalIP")].address}')
export NODE_PORT=$(kubectl -n $LITMUS_PORTAL_NAMESPACE get -o jsonpath="{.spec.ports[0].nodePort}" services litmusportal-frontend-service)
echo "URL: http://$EXTERNAL_IP:$NODE_PORT"
```

#### Minikube

```bash
minikube -n $LITMUS_PORTAL_NAMESPACE --url litmusportal-frontend-service
```

Note: Default `username: admin` and `password: litmus`

### **User Guide for Litmus Portal**

Litmus-Portal provides console or UI experience for managing, monitoring, and events round chaos workflows. Chaos workflows consist of a sequence of experiments run together to achieve the objective of introducing some kind of fault into an application or the Kubernetes platform.

View the User Guide <b>[here](https://docs.litmuschaos.io/)</b>

### **Upgrade from 2.7.0 to 2.8.0**

You can upgrade using the steps from [section here](https://docs.litmuschaos.io/docs/user-guides/upgrade)

### **Uninstallation**

You can uninstall using the steps from [section here](http://docs.litmuschaos.io//docs/user-guides/uninstall-litmus)

- <a href="https://github.com/litmuschaos/litmus/wiki/Litmus-Portal-design-specification" target="_blank">Litmus Portal Design Specification</a><br>
- <a href="https://github.com/litmuschaos/litmus/wiki/Litmus-Portal-Development-Guide" target="_blank">Litmus Portal Development Guide</a>
