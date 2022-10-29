
# install
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-kafka bitnami/kafka -n coderun

### logs
```
NAME: my-kafka
LAST DEPLOYED: Mon Aug  1 05:42:55 2022
NAMESPACE: coderun
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: kafka
CHART VERSION: 18.0.3
APP VERSION: 3.2.0

** Please be patient while the chart is being deployed **

Kafka can be accessed by consumers via port 9092 on the following DNS name from within your cluster:

    my-kafka.coderun.svc.cluster.local

Each Kafka broker can be accessed by producers via port 9092 on the following DNS name(s) from within your cluster:

    my-kafka-0.my-kafka-headless.coderun.svc.cluster.local:9092

To create a pod that you can use as a Kafka client run the following commands:

    kubectl run my-kafka-client --restart='Never' --image docker.io/bitnami/kafka:3.2.0-debian-11-r12 --namespace coderun --command -- sleep infinity
    kubectl exec --tty -i my-kafka-client --namespace coderun -- bash

    PRODUCER:
        kafka-console-producer.sh \
            
            --broker-list my-kafka-0.my-kafka-headless.coderun.svc.cluster.local:9092 \
            --topic test

    CONSUMER:
        kafka-console-consumer.sh \
            
            --bootstrap-server my-kafka.coderun.svc.cluster.local:9092 \
            --topic test \
            --from-beginning
```
