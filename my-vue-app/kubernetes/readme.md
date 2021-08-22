```bash
    # Créez le déploiement 
    kubectl apply -f ./my-vue-app/kubernetes/deployment.yaml
    kubectl apply -f ./my-vue-app/kubernetes/service.yaml
    
    # Pour vérifier si le déploiement, le service ou le pod a été créé
    kubectl get deployments
    kubectl get pods
    kubectl get service
    
    # Installation de Ingress Nginx
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/cloud/deploy.yaml
    kubectl apply -f ./my-vue-app/kubernetes/ingress.yaml
    kubectl get ingress
    
    # Install metrics server
    kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.4.2/components.yaml
    kubectl patch deployment metrics-server -n kube-system --type 'json' -p '[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'
    
    # HPA
    kubectl autoscale deployment react-deployment --cpu-percent=50 --min=1 --max=10 --dry-run -oyaml   
    kubectl get hpa 
    
    # Install dashboard
    helm install prometheus-operator stable/prometheus-operator
    
    # Conntect to dashboard
    kubectl port-forward svc/prometheus-operator-grafana 3001:80
    go to https://localhost:3001   login: admin password: prom-operator
    
    # Delete
    kubectl delete ${TYPE}  ${NAME}
```