# Installing Loki Stack
First add Loki’s chart repository to helm

helm repo add grafana https://grafana.github.io/helm-charts


# Then update the chart repository

helm repo update


This command will:

install grafana
install prometheus
install loki
enable persistence for your stack and create a PVC


helm upgrade --install loki grafana/loki-stack  --set grafana.enabled=true,prometheus.enabled=true,prometheus.alertmanager.persistentVolume.enabled=false,prometheus.server.persistentVolume.enabled=false,loki.persistence.enabled=true,loki.persistence.storageClassName=nfs-client,loki.persistence.size=5Gi



# Accessing the Grafana Dashboard


To get the password for the admin user run
kubectl get secret --namespace <YOUR-NAMESPACE> loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo




Ingress with Traefik
If you want to create an IngressRoute and you are using traefik can you apply the following

kubectl apply -f ingress.yml




![image](https://github.com/KarthiCholan/GrafanaLoki/assets/108706606/69c45c15-1902-4e0e-a997-ca3727802427)


LogQL sample queries

Query all logs from the container label

{container="uptime-kuma"} 


query all logs from the container stream and filter on error

{container="uptime-kuma"} |= "error"


query all logs from the pod label of uptime-kuma-8d45g32fd-lk8rl

{pod="uptime-kuma-8d45g32fd-lk8rl"}

