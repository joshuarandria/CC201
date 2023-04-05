kubectl config get-clusters
kubectl config get-contexts
kubectl get pods
export MY_NAMESPACE=sn-labs-$USERNAME

docker build -t us.icr.io/$MY_NAMESPACE/hello-world:1 . && docker push us.icr.io/$MY_NAMESPACE/hello-world:1

kubectl run hello-world --image us.icr.io/$MY_NAMESPACE/hello-world:1 --overrides='{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"icr"}]}}}}'

kubectl get pods -o wide
kubectl describe pod hello-world
kubectl delete pod hello-world
kubectl create -f hello-world-create.yaml
kubectl apply -f hello-world-apply.yaml
kubectl get deployments
kubectl delete pod <pod_name> && kubectl get pods
kubectl expose deployment/hello-world
kubectl get services

# In another Terminal
kubectl proxy
(kill the terminal with ctrl+c when finished)

# Back in the first Terminal
curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy

for i in `seq 10`; do curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy; done

kubectl delete deployment/hello-world service/hello-world