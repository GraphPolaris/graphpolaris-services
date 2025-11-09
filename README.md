## Deploy AKS Cluster with Nginx HelloWorld

Deploy a basic Azure Kubernetes Service (AKS) cluster with a simple Nginx HelloWorld page accessible to the internet.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGraphPolaris%2Fgraphpolaris-services%2Frefs%2Fheads%2Fmain%2Fazuredeploy.json)

After deployment:
1. The AKS cluster will be created
2. A deployment script will automatically deploy an Nginx HelloWorld application
3. The application will be accessible via a LoadBalancer public IP
4. Check the deployment script outputs or run: `kubectl get svc nginx-hello-service -n nginx-hello`

To connect to your cluster:
```bash
az aks get-credentials --resource-group <your-resource-group> --name <cluster-name>
```
