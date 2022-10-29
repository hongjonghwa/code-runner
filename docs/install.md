### os
```sh
sudo hostnamectl set-hostname code-runner
sudo yum update
sudo yum install -y git golang
```

### docker
```sh
sudo yum install -y docker
sudo usermod -aG docker $USER
systemctl enable --now docker
```

### minikube
```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
sudo rpm -Uvh minikube-latest.x86_64.rpm
minikube start
```

### .bashrc
```bash
alias kubectl="minikube kubectl --"
eval $(minikube docker-env)
```

### minikube dashboard
```sh
minikube dashboard --url
# ssh -N -L 39875:127.0.0.1:39875 dev
```



kubectl run --rm -i --tty --image alpine my-shell -- sh
kubectl delete po my-shell
kubectl exec --stdin --tty my-shell -- /bin/sh
kubectl run -i --tty --rm --image stratch my-shell -- bash