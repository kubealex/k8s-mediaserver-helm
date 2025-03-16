# k8s-mediaserver-helm
Repo for k8s-mediaserver helm chart, backing **[k8s-mediaserver-operator](https://github.com/kubealex/k8s-mediaserver-operator)**

## General config

| Config path                           | Meaning                                                                                                     | Default                                         |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| general.ingress_host                  | The hostname to use in ingress definition, this will be the hostname where the applications will be exposed | k8s-mediaserver.k8s.test                        |
| general.plex_ingress_host             | The hostname to use for **PLEX** as it must be exposed on a / dedicated path                                | k8s-plex.k8s.test                               |
| general.jellyfin_ingress_host         | The hostname to use for **JellyFin** as it must be exposed on a / dedicated path                            | k8s-jelly.k8s.test                              |
| general.image_tag                     | The name of the image tag (arm32v7-latest, arm64v8-latest, development)                                     | latest                                          |
| general.pgid                          | The GID for the process                                                                                     | 1000                                            |
| general.puid                          | The UID for the process                                                                                     | 1000                                            |
| general.nodeSelector                  | Default Node Selector for all the pods. Per-service nodeSelectors are merged against this.                  | {}                                              |
| general.storage.customVolume          | Flag if you want to supply your own volume and not use a PVC                                                | false                                           |
| general.storage.pvcName               | Name of the persistenVolumeClaim configured in deployments                                                  | mediaserver-pvc                                 |
| general.storage.accessMode            | Access mode for mediaserver PVC in case of single nodes                                                     | ReadWriteMany                                   |
| general.storage.pvcStorageClass       | Specifies a storageClass for the PVC                                                                        | ""                                              |
| general.storage.size                  | Size of the persistenVolume                                                                                 | 50Gi                                            |
| general.storage.subPaths.tv           | Default subpath for tv series folder on used storage                                                        | media/tv                                        |
| general.storage.subPaths.movies       | Default subpath for movies folder on used storage                                                           | media/movies                                    |
| general.storage.subPaths.downloads    | Default root path for downloads for both sabnzbd and transmission on used storage                           | downloads                                       |
| general.storage.subPaths.transmission | Default subpath for transmission downloads on used storage                                                  | general.storage.subPaths.downloads/transmission |
| general.storage.subPaths.sabnzbd      | Default subpath for sabnzbd downloads on used storage                                                       | general.storage.subPaths.downloads/sabnzbd      |
| general.storage.subPaths.config       | Default subpath for all config files on used storage                                                        | config                                          |
| general.storage.volumes               | Supply custom volume to be mounted for all services                                                         | {}                                              |
| general.ingress.ingressClassName      | Reference an IngressClass resource that contains additional Ingress configuration                           | ""                                              |

### Plex

| Config path                             | Meaning                                                                                                       | Default                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------- |
| plex.enabled                            | Flag if you want to enable Plex                                                                               | true                       |
| plex.claim                              | **IMPORTANT** Token from your account, needed to claim the server                                             | CHANGEME                   |
| plex.replicaCount                       | Number of replicas serving Plex                                                                               | 1                          |
| plex.container.nodeSelector             | Node Selector for the Plex pods                                                                               | {}                         |
| plex.container.port                     | The port in use by the container                                                                              | 32400                      |
| plex.container.image                    | The image used by the container                                                                               | docker.io/linuxserver/plex |
| plex.container.tag                      | The tag used by the container                                                                                 | null                       |
| plex.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                         | ClusterIP                  |
| plex.service.port                       | The port assigned to the service                                                                              | 32400                      |
| plex.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                         | ""                         |
| plex.service.extraLBService             | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                      |
| plex.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer  | null                       |
| plex.ingress.enabled                    | If true, creates the ingress resource for the application                                                     | true                       |
| plex.ingress.annotations                | Additional field for annotations, if needed                                                                   | {}                         |
| plex.ingress.path                       | The path where the application is exposed                                                                     | /plex                      |
| plex.ingress.tls.enabled                | If true, tls is enabled                                                                                       | false                      |
| plex.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                | ""                         |
| plex.resources                          | Limits and Requests for the container                                                                         | {}                         |
| plex.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                         |

### Jellyfin

| Config path                                 | Meaning                                                                                                           | Default                        |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| jellyfin.enabled                            | Flag if you want to enable Jellyfin                                                                               | true                           |
| jellyfin.replicaCount                       | Number of replicas serving Jellyfin                                                                               | 1                              |
| jellyfin.container.nodeSelector             | Node Selector for the Jellyfin pods                                                                               | {}                             |
| jellyfin.container.port                     | The port in use by the container                                                                                  | 8096                           |
| jellyfin.container.image                    | The image used by the container                                                                                   | docker.io/linuxserver/jellyfin |
| jellyfin.container.tag                      | The tag used by the container                                                                                     | null                           |
| jellyfin.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                             | ClusterIP                      |
| jellyfin.service.port                       | The port assigned to the service                                                                                  | 8096                           |
| jellyfin.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                             | ""                             |
| jellyfin.service.extraLBService             | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)      | false                          |
| jellyfin.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer      | null                           |
| jellyfin.ingress.enabled                    | If true, creates the ingress resource for the application                                                         | true                           |
| jellyfin.ingress.annotations                | Additional field for annotations, if needed                                                                       | {}                             |
| jellyfin.ingress.path                       | The path where the application is exposed                                                                         | /jellyfin                      |
| jellyfin.ingress.tls.enabled                | If true, tls is enabled                                                                                           | false                          |
| jellyfin.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                    | ""                             |
| jellyfin.resources                          | Limits and Requests for the container                                                                             | {}                             |
| jellyfin.volume                             | If set, Jellyfin will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                             |

### Sonarr

| Config path                               | Meaning                                                                                                       | Default                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| sonarr.enabled                            | Flag if you want to enable Sonarr                                                                             | true                         |
| sonarr.container.port                     | The port in use by the container                                                                              | 8989                         |
| sonarr.container.nodeSelector             | Node Selector for the Sonarr pods                                                                             | {}                           |
| sonarr.container.image                    | The image used by the container                                                                               | docker.io/linuxserver/sonarr |
| sonarr.container.tag                      | The tag used by the container                                                                                 | null                         |
| sonarr.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                         | ClusterIP                    |
| sonarr.service.port                       | The port assigned to the service                                                                              | 8989                         |
| sonarr.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                         | ""                           |
| sonarr.service.extraLBService             | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                        |
| sonarr.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer  | null                         |
| sonarr.ingress.enabled                    | If true, creates the ingress resource for the application                                                     | true                         |
| sonarr.ingress.annotations                | Additional field for annotations, if needed                                                                   | {}                           |
| sonarr.ingress.path                       | The path where the application is exposed                                                                     | /sonarr                      |
| sonarr.ingress.tls.enabled                | If true, tls is enabled                                                                                       | false                        |
| sonarr.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                | ""                           |
| sonarr.resources                          | Limits and Requests for the container                                                                         | {}                           |
| sonarr.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                           |

### Radarr

| Config path                               | Meaning                                                                                                       | Default                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| radarr.enabled                            | Flag if you want to enable Radarr                                                                             | true                         |
| radarr.container.port                     | The port in use by the container                                                                              | 7878                         |
| radarr.container.nodeSelector             | Node Selector for the Radarr pods                                                                             | {}                           |
| radarr.container.image                    | The image used by the container                                                                               | docker.io/linuxserver/radarr |
| radarr.container.tag                      | The tag used by the container                                                                                 | null                         |
| radarr.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                         | ClusterIP                    |
| radarr.service.port                       | The port assigned to the service                                                                              | 7878                         |
| radarr.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                         | ""                           |
| radarr.service.extraLBService             | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                        |
| radarr.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer  | null                         |
| radarr.ingress.enabled                    | If true, creates the ingress resource for the application                                                     | true                         |
| radarr.ingress.annotations                | Additional field for annotations, if needed                                                                   | {}                           |
| radarr.ingress.path                       | The path where the application is exposed                                                                     | /radarr                      |
| radarr.ingress.tls.enabled                | If true, tls is enabled                                                                                       | false                        |
| radarr.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                | ""                           |
| radarr.resources                          | Limits and Requests for the container                                                                         | {}                           |
| radarr.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                           |

### Jackett

| Config path                                | Meaning                                                                                                         | Default                       |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| jackett.enabled                            | Flag if you want to enable Jackett                                                                              | true                          |
| jackett.container.port                     | The port in use by the container                                                                                | 9117                          |
| jackett.container.nodeSelector             | Node Selector for the Jackett pods                                                                              | {}                            |
| jackett.container.image                    | The image used by the container                                                                                 | docker.io/linuxserver/jackett |
| jackett.container.tag                      | The tag used by the container                                                                                   | null                          |
| jackett.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                           | ClusterIP                     |
| jackett.service.port                       | The port assigned to the service                                                                                | 9117                          |
| jackett.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                           | ""                            |
| jackett.service.extraLBService             | If true, it creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false                         |
| jackett.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer    | null                          |
| jackett.ingress.enabled                    | If true, creates the ingress resource for the application                                                       | true                          |
| jackett.ingress.annotations                | Additional field for annotations, if needed                                                                     | {}                            |
| jackett.ingress.path                       | The path where the application is exposed                                                                       | /jackett                      |
| jackett.ingress.tls.enabled                | If true, tls is enabled                                                                                         | false                         |
| jackett.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                  | ""                            |
| jackett.resources                          | Limits and Requests for the container                                                                           | {}                            |
| jackett.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config   | {}                            |

### Prowlarr

| Config path                                 | Meaning                                                                                                         | Default                        |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| prowlarr.enabled                            | Flag if you want to enable Prowlarr                                                                             | true                           |
| prowlarr.container.port                     | The port in use by the container                                                                                | 9117                           |
| prowlarr.container.nodeSelector             | Node Selector for the Prowlarr pods                                                                             | {}                             |
| prowlarr.container.image                    | The image used by the container                                                                                 | docker.io/linuxserver/prowlarr |
| prowlarr.container.tag                      | The tag used by the container                                                                                   | develop                        |
| prowlarr.service.type                       | The kind of Service (ClusterIP/NodePort/LoadBalancer)                                                           | ClusterIP                      |
| prowlarr.service.port                       | The port assigned to the service                                                                                | 9117                           |
| prowlarr.service.nodePort                   | In case of service.type NodePort, the nodePort to use                                                           | ""                             |
| prowlarr.service.extraLBService             | If true, it creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false                          |
| prowlarr.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer    | null                           |
| prowlarr.ingress.enabled                    | If true, creates the ingress resource for the application                                                       | true                           |
| prowlarr.ingress.annotations                | Additional field for annotations, if needed                                                                     | {}                             |
| prowlarr.ingress.path                       | The path where the application is exposed                                                                       | /prowlarr                      |
| prowlarr.ingress.tls.enabled                | If true, tls is enabled                                                                                         | false                          |
| prowlarr.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                  | ""                             |
| prowlarr.resources                          | Limits and Requests for the container                                                                           | {}                             |
| prowlarr.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config   | {}                             |

### Transmission

| Config path                                     | Meaning                                                                                                       | Default                            |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| transmission.enabled                            | Flag if you want to enable Transmission                                                                       | true                               |
| transmission.container.port.utp                 | The port in use by the container                                                                              | 9091                               |
| transmission.container.nodeSelector             | Node Selector for the Transmission pods                                                                       | {}                                 |
| transmission.container.port.peer                | The port in use by the container for peer connection                                                          | 51413                              |
| transmission.container.image                    | The image used by the container                                                                               | docker.io/linuxserver/transmission |
| transmission.container.tag                      | The tag used by the container                                                                                 | null                               |
| transmission.service.utp.type                   | The kind of Service (ClusterIP/NodePort/LoadBalancer) for Transmission itself                                 | ClusterIP                          |
| transmission.service.utp.port                   | The port assigned to the service for Transmission itself                                                      | 9091                               |
| transmission.service.utp.nodePort               | In case of service.type NodePort, the nodePort to use for Transmission itself                                 | ""                                 |
| transmission.service.utp.extraLBService         | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                              |
| transmission.service.peer.type                  | The kind of Service (ClusterIP/NodePort/LoadBalancer) for peer port                                           | ClusterIP                          |
| transmission.service.peer.port                  | The port assigned to the service for peer port                                                                | 51413                              |
| transmission.service.peer.nodePort              | In case of service.type NodePort, the nodePort to use for peer port                                           | ""                                 |
| transmission.service.peer.nodePortUDP           | In case of service.type NodePort, the nodePort to use for peer port UDP service                               | ""                                 |
| transmission.service.peer.extraLBService        | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                              |
| transmission.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer  | null                               |
| transmission.ingress.enabled                    | If true, creates the ingress resource for the application                                                     | true                               |
| transmission.ingress.annotations                | Additional field for annotations, if needed                                                                   | {}                                 |
| transmission.ingress.path                       | The path where the application is exposed                                                                     | /transmission                      |
| transmission.ingress.tls.enabled                | If true, tls is enabled                                                                                       | false                              |
| transmission.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                | ""                                 |
| transmission.config.auth.enabled                | Enables authentication for Transmission                                                                       | false                              |
| transmission.config.auth.username               | Username for Transmission                                                                                     | ""                                 |
| transmission.config.auth.password               | Password for Transmission                                                                                     | ""                                 |
| transmission.resources                          | Limits and Requests for the container                                                                         | {}                                 |
| transmission.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                                 |

### Sabnzbd

| Config path                                | Meaning                                                                                                       | Default                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| sabnzbd.enabled                            | Flag if you want to enable Sabnzbd                                                                            | true                          |
| sabnzbd.container.nodeSelector             | Node Selector for the Sabnzbd pods                                                                            | {}                            |
| sabnzbd.container.port.http                | The port in use by the container                                                                              | 8080                          |
| sabnzbd.container.port.https               | The port in use by the container for peer connection                                                          | 9090                          |
| sabnzbd.container.image                    | The image used by the container                                                                               | docker.io/linuxserver/sabnzbd |
| sabnzbd.container.tag                      | The tag used by the container                                                                                 | null                          |
| sabnzbd.service.http.type                  | The kind of Service (ClusterIP/NodePort/LoadBalancer) for Sabnzbd itself                                      | ClusterIP                     |
| sabnzbd.service.http.port                  | The port assigned to the service for Sabnzbd itself                                                           | 9091                          |
| sabnzbd.service.http.nodePort              | In case of service.type NodePort, the nodePort to use for Sabnzbd itself                                      | ""                            |
| sabnzbd.service.http.extraLBService        | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                         |
| sabnzbd.service.https.type                 | The kind of Service (ClusterIP/NodePort/LoadBalancer) for https port                                          | ClusterIP                     |
| sabnzbd.service.https.port                 | The port assigned to the service for peer port                                                                | 51413                         |
| sabnzbd.service.https.nodePort             | In case of service.type NodePort, the nodePort to use for https port                                          | ""                            |
| sabnzbd.service.https.extraLBService       | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB)  | false                         |
| sabnzbd.service.extraLBService.annotations | Instead of using extraLBService as a bool, you can use it as a map to define annotations on the loadbalancer  | null                          |
| sabnzbd.ingress.enabled                    | If true, creates the ingress resource for the application                                                     | true                          |
| sabnzbd.ingress.annotations                | Additional field for annotations, if needed                                                                   | {}                            |
| sabnzbd.ingress.path                       | The path where the application is exposed                                                                     | /sabnzbd                      |
| sabnzbd.ingress.tls.enabled                | If true, tls is enabled                                                                                       | false                         |
| sabnzbd.ingress.tls.secretName             | Name of the secret holding certificates for the secure ingress                                                | ""                            |
| sabnzbd.resources                          | Limits and Requests for the container                                                                         | {}                            |
| sabnzbd.volume                             | If set, Plex will create a PVC for it's config volume, else it will be put on general.storage.subPaths.config | {}                            |


## About the project

This project is intended as an exercise, and absolutely for fun. Don't use it to commit piracy.

Also feel free to contribute and extend it!

