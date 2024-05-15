# argocd-install

manifest with crd's required for install

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Let's make the service type NodePort to access the UI.

```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```

We'll look at secret for the UI password.

```
# username: admin
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
Port-Forward for Argo UI

```
kubectl port-forward -n argocd service/argocd-server 8080:80
```
