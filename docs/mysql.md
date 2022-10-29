### install
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-mysql bitnami/mysql -n coderun \
    --set auth.rootPassword=mysql_secret_password

### port-forward

kubectl port-forward --address 0.0.0.0 -n coderun service/my-mysql 3306

### tests
docker run -it --rm mysql mysql -h<eth0 ip address> -uroot -pmysql_secret_password -e "show databases;"

### logs

NAME: my-mysql
LAST DEPLOYED: Mon Aug  1 07:08:16 2022
NAMESPACE: coderun
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: mysql
CHART VERSION: 9.2.3
APP VERSION: 8.0.30

** Please be patient while the chart is being deployed **

Tip:

  Watch the deployment status using the command: kubectl get pods -w --namespace coderun

Services:

  echo Primary: my-mysql.coderun.svc.cluster.local:3306

Execute the following to get the administrator credentials:

  echo Username: root
  MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace coderun my-mysql -o jsonpath="{.data.mysql-root-password}" | base64 -d)

To connect to your database:

  1. Run a pod that you can use as a client:

      kubectl run my-mysql-client --rm --tty -i --restart='Never' --image  docker.io/bitnami/mysql:8.0.30-debian-11-r1 --namespace coderun --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --command -- bash

  2. To connect to primary service (read/write):

      mysql -h my-mysql.coderun.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"