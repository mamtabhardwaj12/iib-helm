# IBM INTEGRATION BUS

IBM® Integration Bus is a market-leading lightweight enterprise integration engine that offers a fast, simple way for systems and applications to communicate with each other. As a result, it can help you achieve business value, reduce IT complexity and save money.
IBM Integration Bus supports a range of integration choices, skills and interfaces to optimize the value of existing technology investments. 
[Test]
(https://www.youtube.com/embed/qQvT4kJoPTM)

Learn more about IBM Integration Bus at the following link: [https://www.ibm.com/support/knowledgecenter/en/SSMKHH_10.0.0/com.ibm.etools.msgbroker.helphome.doc/help_home_msgbroker.htm]
(https://www.ibm.com/support/knowledgecenter/en/SSMKHH_10.0.0/com.ibm.etools.msgbroker.helphome.doc/help_home_msgbroker.htm).

## TL;DR;

```bash
$ helm install incubating/iib
```

# Quick Start

1. Create a Persistent Volume which will be utilized for storage

The MQ chart requires access to storage in order to persist the database, which is performed through the Kubernetes Volume Claim mechanism. The storage can be allocated in the private cloud admin console. 

For minikube, use the following command to allocate a Persistent Volume directly on the minikube virtual machine: 

```cat <<EOF | kubectl create -f -
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv0001
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 5Gi
  hostPath:
    path: /data/pv0001/
EOF
```

2. Install the chart

```helm install --set license=accept mq```

Parameters
------------
The helm chart has the following Values that can be overriden using the install `--set` parameter. For example:

`helm install --set queuemanger.name=ExampleOverride chart/qmgr`

| Value                     | Description                                   | Default          |
|---------------------------|-----------------------------------------------|------------------|
| image.repository          | The image to use for this deployment          | ibmcom/mq        |
| image.tag                 | The image tag to use for this deployment      | latest           |
| queuemanger.name          | name of queue manager                         | qm1              |
| resources.storage.size    | Size of storage to use for Queue Manager data | 128M             |
| resources.storage.class   | Storage class to use for Queue Manager        | ibmc-file-bronze |
| resources.limits.cpu      | Container CPU limit                           | 100m             |
| resources.limits.memory   | Container memory limit                        | 512Mi            |
| resources.requests.cpu    | Container CPU requested                       | 100m             |
| resources.requests.memory | Container Memory requested                    | 512Mi            |

Accessing the pod (Queue Manager or MQ Console) from outside
-----------------------
The chart currently uses a service of type NodePort which randomly assigns a port in the kubernetes clusters and maps it to the pod. In fact it does this twice, once for port `1414` which the Queue Manager listens on and once for `9443` which the MQ Console listens on for HTTPS traffic (not http, very important as when you try to navigate to the console you must use https)

Once you know your public IP you need to find out what ports we're listening on execute the following command to find out what your service is called:

`kubectl get services`

Once you know the name of your service execute the following command to get the details of that service:

`kubectl describe service <service Name>`

```
Name:			listening-lion-qmgr
Namespace:		default
Labels:			chart=qmgr-0.1.0
Selector:		app=listening-lion-qmgr
Type:			NodePort
IP:			10.10.10.7
Port:			qmgr-1	1414/TCP
NodePort:		qmgr-1	30492/TCP
Endpoints:		172.30.92.78:1414
Port:			qmgr-2	9443/TCP
NodePort:		qmgr-2	31326/TCP
Endpoints:		172.30.92.78:9443
Session Affinity:	None
No events.
```

The bit we're interested in is the NodePort which for the example above shows that if we wanted to connect to the console we would need to connect to `https://<publicIP>:31326/ibmmq/console` and if we wanted to connect to the queue manager we'd use `<publicIP>(30492)`.

_Copyright IBM Corporation 2017. All Rights Reserved._
