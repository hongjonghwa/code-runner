# Start minikube
minikube start

# Set docker env
eval $(minikube docker-env)             # unix shells
minikube docker-env | Invoke-Expression # PowerShell

# Build image
docker build -t foo:0.0.1 .

# Run in minikube
kubectl run hello-foo --image=foo:0.0.1 --image-pull-policy=Never

# Check that it's running
kubectl get pods



# test
kubectl run --rm -i --tty --image alpine my-shell -- sh
kubectl delete po my-shell
kubectl exec --stdin --tty my-shell -- /bin/sh
kubectl run -i --tty --rm --image stratch my-shell -- bash