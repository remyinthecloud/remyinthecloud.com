--- 
title: Setting up Prometheus and Grafana Monitoring on Homelab Kubernetes Cluster
tags: [prometheus, grafana, linux, ubuntu, helm, kubernetes, metrics, monitoring, logging]
categories: [prometheus, grafana, homelab]
---

# Goals

1. **Install Helm**  
   - Using Helm will make the next two steps a whole lot simpler. With Helm charts, I can leverage the public Prometheus GitHub community to install and host Prometheus locally on my Kubernetes cluster.

2. **Install Prometheus**  
   - I want to integrate Prometheus to collect key metrics about my Kubernetes cluster. Metrics like CPU usage and uptime are crucial for monitoring system health.

3. **Install Grafana**  
   - Grafana will be used to visualize these metrics in **dashboards** that provide a holistic view of system performance over time.

---

# Helm Installation

I'm following the Helm documentation for installation on my Ubuntu system.  

📌 Official Documentation: [Helm Installation Guide](https://helm.sh/docs/intro/install/)

### Install Helm via Script  

Helm provides an installer script that automatically downloads and installs the latest version.  

Run the following commands:  

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

# Prometheus

## Step 1: Add Helm Prometheus Repo

Run the following command:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

## Step 2: Install Prometheus

1. Install the Prometheus Helm chart:

```bash
helm install prometheus prometheus-community/prometheus --namespace monitoring --create-namespace
```

- **prometheus**: The release name.
- **--namespace monitoring**: Creates a namespace for Prometheus. You can name this whatever you want to group your applications appropriately to your setup.

### Troubleshooting Installation

These are the errors I myself encountered. If you encounter the following error:

```bash
Error: INSTALLATION FAILED: Kubernetes cluster unreachable: Get "http://localhost:8080/version": dial tcp 127.0.0.1:8080: connect: connection refused
```

Try viewing your pods. Walking your through my debugging brain and process:

```bash
kubectl get pods -A
```

If you see like I did:

```bash
WARN[0000] Unable to read /etc/rancher/k3s/k3s.yaml, please start server with --write-kubeconfig-mode or --write-kubeconfig-group to modify kube config permissions
error: error loading config file "/etc/rancher/k3s/k3s.yaml": open /etc/rancher/k3s/k3s.yaml: permission denied
```

This indicates an issue with your kubeconfig file permissions. To resolve I found this helpful code online from [Roggier Dikkes](https://0to1.nl/post/k3s-kubectl-permission/):

```bash
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config && sudo chown $USER ~/.kube/config && sudo chmod 600 ~/.kube/config && export KUBECONFIG=~/.kube/config
```

Add this to your `~/.zshrc` to persist across terminal sessions (helpful so I don't have to run this each time I remote into my server):

```bash
echo 'export KUBECONFIG=~/.kube/config' >> ~/.zshrc
source ~/.zshrc
```

2. Verify installation:

```bash
kubectl get all -n monitoring
```

You should see resources like pods, services, and deployments related to Prometheus.

3. Access Prometheus locally:

- Get the Prometheus server service details:

```bash
kubectl get svc -n monitoring
```

- Port forward the Prometheus server to port `9090`:

```bash
kubectl port-forward svc/prometheus-server -n monitoring 9090:80
```

- Access Prometheus via: `http://localhost:9090`

---

# Grafana (Kube-Prometheus-Stack)

We will use the `kube-prometheus-stack` from the Prometheus community Helm repo to install Grafana.

📌 Helm Repo: [Prometheus Helm Charts](https://prometheus-community.github.io/helm-charts)

## Step 1: Install `kube-prometheus-stack`

```bash
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring
```

Check its status:

```bash
kubectl --namespace monitoring get pods -l "release=kube-prometheus-stack"
```

You should see `kube-prometheus-stack-grafana` running:

```bash
kubectl get pods -n monitoring
```

## Step 2: Port Forward Grafana Application

Forward Grafana to port `3000`:

```bash
kubectl port-forward svc/kube-prometheus-stack-grafana -n monitoring 3000:80
```

## Step 3: Get Grafana Password

Retrieve and decode the password:

```bash
kubectl get secret --namespace monitoring kube-prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 --decode
```

Access Grafana at `http://localhost:3000`

- **Username:** `admin`
- **Password:** (output from the previous command)

## Step 4: Connect Prometheus to Grafana

To connect Prometheus as a data source in Grafana:

1. Navigate to **Connections** → **Data Sources**
2. Search for **Prometheus**
3. Under **Prometheus server URL**, enter:
   - `http://prometheus-server:80` (if accessible within the cluster)
   - Otherwise, use `http://localhost:9090`
4. Click **Save & Test**
5. You should see: `Successfully queried the Prometheus API.`

---

# Next Steps

Now that Prometheus and Grafana are running, explore:

- **Grafana Dashboards**: Import pre-built dashboards or create custom ones.
- **Alerts & Notifications**: Configure Prometheus Alertmanager and Grafana alerts.
- **Web Exposure**: Securely expose Grafana using Ingress and authentication.

🚀 Stay tuned for future updates on making this setup accessible remotely while ensuring security!

** Credits to the [Better Team](https://betterstack.com/community/questions/install-prometheus-and-grafana-on-kubernetes-with-helm/) for a helpful resource in aiding this installation proccess for me.

