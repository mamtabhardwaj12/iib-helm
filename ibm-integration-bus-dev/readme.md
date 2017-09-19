<!-- Copyright IBM Corporation 2017. All Rights Resevred. -->
# IBM INTEGRATION BUS

![alt text](https://raw.githubusercontent.com/ot4i/iib-helm/master/ibm-integration-bus-dev/IBM_Integration_Bus_Icon.svg?sanitize=true "IBM Integration Bus Logo")

IBM® Integration Bus is a market-leading lightweight enterprise integration engine that offers a fast, simple way for systems and applications to communicate with each other. As a result, it can help you achieve business value, reduce IT complexity and save money. IBM Integration Bus supports a range of integration choices, skills and interfaces to optimize the value of existing technology investments. 

# Introduction

This chart deploys a single IBM Integration Bus for Developers integration node, containing a single integration server into an IBM Cloud Private or other Kubernetes environment.

## Installing the Chart

To install the chart with the release name `foo`:

```bash
helm install --name foo ibm-integration-bus-dev --set license=accept
```

This command accepts the [IBM Integration Bus for Developers license](LICENSE) and deploys an IBM Integration Bus for Developers server on the Kubernetes cluster. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: See all the resources deployed by the chart using `kubectl get all -l release=foo`

## Uninstalling the Chart

To uninstall/delete the `foo` release:

```bash
helm delete foo
```

The command removes all the Kubernetes components associated with the chart.

## Configuration
The following table lists the configurable parameters of the `ibm-mqadvanced-server-dev` chart and their default values.

| Parameter                        | Description                                     | Default                                                    |
| -------------------------------- | ----------------------------------------------- | ---------------------------------------------------------- |
| `license`                        | Set to `accept` to accept the terms of the IBM license  | `Not accepted`                                     |
| `image.repository`               | Image full name including repository            | `ibmcom/iib`                                                |
| `image.tag`                      | Image tag                                       | `10.0.0.10`                                                        |
| `image.pullPolicy`               | Image pull policy                               | `IfNotPresent`                                             |
| `image.pullSecret`               | Image pull secret, if you are using a private Docker registry | `nil`                                        |
| `service.name`                   | Name of the Kubernetes service to create        | `qmgr`                                                     |
| `service.type`                   | Kubernetes service type exposing ports, e.g. `NodePort`       | `NodePort`                                  |
| `resources.limits.cpu`          | Kubernetes CPU limit for the Queue Manager container | `2`                                                   |
| `resources.limits.memory`       | Kubernetes memory limit for the Queue Manager container | `2048Mi`                                              |
| `resources.requests.cpu`        | Kubernetes CPU request for the Queue Manager container | `1`                                                 |
| `resources.requests.memory`     | Kubernetes memory request for the Queue Manager container | `512Mi`                                            |
| `nodename`              | IBM Integration Bus integration node name                           | IIB_NODE                                          |
| `servername`              | IBM Integration Bus integration node name                           | IIB_SERVER                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart.

> **Tip**: You can use the default [values.yaml](values.yaml)

[![Brief introduction to IBM Integration Bus](https://img.youtube.com/vi/qQvT4kJoPTM/0.jpg)](https://www.youtube.com/watch?v=qQvT4kJoPTM)

[View the IBM Integration Bus Dockerfile repository on Github](https://github.com/ot4i/iib-docker)

[Learn more about IBM Integration Bus Docker Tips and Tricks](https://developer.ibm.com/integration/blog/2017/04/04/ibm-integration-bus-docker-tips-tricks/)

[Learn more about IBM Integration Bus and Kubernetes](https://developer.ibm.com/integration/blog/2017/08/21/first-look-using-ibm-integration-bus-kubernetes/)

[Learn more about running IBM Integration Bus in the Bluemix Container Service](https://developer.ibm.com/integration/blog/2016/11/18/run-ibm-integration-bus-in-bluemix-in-3-easy-steps/)

[Learn more about IBM Integration Bus](https://www.ibm.com/support/knowledgecenter/en/SSMKHH_10.0.0/com.ibm.etools.msgbroker.helphome.doc/help_home_msgbroker.htm)

[Learn more about IBM Integration Bus and Docker](https://www.ibm.com/support/knowledgecenter/en/SSMKHH_10.0.0/com.ibm.etools.mft.doc/bz91300_.htm)

_Copyright IBM Corporation 2017. All Rights Reserved._

_The IBM Integration Bus logo is copyright IBM and is provided for use for the purposes of IBM Cloud Private. You will not use the IBM Integration Bus logo in any way that would diminish the IBM or IBM Integration Bus image. IBM reserves the right to end your privilege to use the logo at any time in the future at our sole discretion. Any use of the IBM Integration Bus logo affirms that you agree to adhere to these conditions._
