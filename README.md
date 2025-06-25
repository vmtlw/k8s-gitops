```
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard
echo $(kubectl get secret -n kubernetes-dashboard admin-user -o jsonpath="{.data.token}" | base64 -d)

added in kubespray
helm repo add jetstack https://charts.jetstack.io --force-update
helm install cert-manager --namespace cert-manager --version v1.18.1 jetstack/cert-manager --create-namespace

kubectl create namespace argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm install argo-cd argo/argo-cd --version 8.1.1 --create-namespace --namespace argo-cd
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

helm repo add uptime-kuma https://dirsigler.github.io/uptime-kuma-helm
helm install uptime-kuma uptime-kuma/uptime-kuma --version 2.21.3 --namespace uptime-kuma --create-namespace

helm repo add nextcloud https://nextcloud.github.io/helm/
helm repo update
helm install nextcloud nextcloud/nextcloud --namespace nextcloud --create-namespace --set nextcloud.host=cloud.vmtlw.ru
ingress:
  annotations:
    nginx.ingress.kubernetes.io/affinity: cookie


helm install forgejo oci://code.forgejo.org/forgejo-helm/forgejo --version 12.5.2 --namespace forgejo --create-namespace

helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana --namespace monitoring
echo $(kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode)


helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus -n monitoring
apt install apache2-utils
htpasswd -c auth admin
kubectl create secret generic basic-auth --from-file=auth --namespace monitoring

helm install minio oci://registry-1.docker.io/bitnamicharts/minio  --namespace minio --create-namespace
kubectl get secret --namespace default minio -o jsonpath="{.data.root-user}" | base64 -d
kubectl get secret --namespace default minio -o jsonpath="{.data.root-password}" | base64 -d


чтобы virth   работал с заранее созданными вами интерфейсом br0 можно выполнить 
virsh net-define /tmp/br0.xml
virsh net-start br0
virsh net-autostart br0
virsh net-list --all
```
