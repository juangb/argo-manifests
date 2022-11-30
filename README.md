# argo-manifests
Testing sync waves

# Commands

## KIND
kind get clusters
kind create cluster --name cluster-2
kubectl config use-context kind-cluster-2

## Install ArgoCD
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl port-forward svc/argocd-server -n argocd 8080:443

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d | xargs -0 argocd login localhost:8080 --insecure --username admin --password 

argocd cluster add kind-cluster-1 --name cluster-1
