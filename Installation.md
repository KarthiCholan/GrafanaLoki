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



