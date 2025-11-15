## Deploy GraphPolaris Services on Azure Kubernetes Service (AKS)

This Azure Resource Manager (ARM) template deploys a complete AKS cluster with the GraphPolaris services stack using Helm.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGraphPolaris%2Fgraphpolaris-services%2Frefs%2Fheads%2Fmain%2Fazuredeploy.json)

### What This Template Deploys

1. **Azure Kubernetes Service (AKS) Cluster**
   - Configurable node count (3-10 nodes)
   - Standard LoadBalancer with managed outbound IPs
   - RBAC enabled
   - Kubenet networking

2. **GraphPolaris Services Stack**
   - Automatically installs the GraphPolaris Helm chart
   - Deploys all GraphPolaris microservices
   - Configures required third-party services

### Prerequisites

Before deploying, you'll need:

- An Azure subscription
- Helm OCI registry credentials (registry URL, username, password)
- Helm chart name and version
- Docker registry credentials (base64 encoded docker config JSON) for pulling container images

### Deployment Parameters

The template requires the following parameters:

- **helmRegistry**: Helm OCI registry URL
- **helmRegistryUser**: Helm registry username
- **helmRegistryPassword**: Helm registry password
- **helmChartName**: Name of the Helm chart to install
- **helmChartVersion**: Version of the Helm chart
- **dockerConfigJson**: Base64 encoded docker config JSON for registry credentials

Optional parameters:
- **clusterName**: Name of the AKS cluster (default: auto-generated)
- **nodeCount**: Number of nodes (default: 3, range: 3-10)
- **nodeVmSize**: VM size for nodes (default: Standard_B2s)
- **kubernetesVersion**: Kubernetes version (default: 1.31)
- **servicePrincipalClientId**: Service principal for AKS (optional, uses managed identity if not provided)

### After Deployment

1. The AKS cluster will be created
2. A deployment script will automatically:
   - Install kubectl and Helm if needed
   - Connect to the AKS cluster
   - Login to the Helm registry
   - Install the GraphPolaris services Helm chart
   - Wait for all deployments to be ready
   - Display LoadBalancer service IPs

3. Services will be accessible via LoadBalancer public IPs
   - Check the deployment script outputs for service IPs
   - Or run: `kubectl get svc --all-namespaces -o wide | grep LoadBalancer`

### Connect to Your Cluster

```bash
az aks get-credentials --resource-group <your-resource-group> --name <cluster-name>
```

### Verify Deployment

Check the status of all deployments:
```bash
kubectl get deployments --all-namespaces
```

View LoadBalancer service IPs:
```bash
kubectl get svc --all-namespaces -o wide | grep LoadBalancer
```

Check pod status:
```bash
kubectl get pods --all-namespaces
```
