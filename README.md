# k8s-mediaserver-helm
Repo for k8s-mediaserver helm chart, backing **[k8s-mediaserver-operator](https://github.com/kubealex/k8s-mediaserver-operator)**

# General config

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| general.ingress_host | The hostname to use in ingress definition, this will be the hostname where the applications will be exposed  | k8s-mediaserver.k8s.test |
| general.plex_ingress_host | The hostname to use for **PLEX** as it must be exposed on a / dedicated path  | k8s-plex.k8s.test |
| general.pgid | The GID for the process | 1000 |
| general.puid | The UID for the process | 1000 |
| general.nodeSelector | Node Selector for all the pods | {} |
| general.storage.nfs  | Specifies if the PV should be configured as a NFS export | false |
| general.storage.nfsPath  | If PV type is NFS, specifies the path of the export | "" |
| general.storage.nfsServer  | If PV type is NFS, specifies the server exporting the volume | "" |
| general.storage.pvcName  | Name of the persistenVolumeClaim configured in deployments | mediaserver-pvc |
| general.storage.pvcStorageClass  | Specifies a storageClass for the PVC | {} |
| general.storage.size | Size of the persistenVolume | 50Gi |

# Plex

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
|plex.claim | **IMPORTANT** Token from your account, needed to claim the server | CHANGEME |
|plex.replicaCount | Number of replicas serving plex | 1 | 
|plex.container.port | The port in use by the container | 32400 | 
|plex.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
|plex.service.port | The port assigned to the service | 32400 |
|plex.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
|plex.service.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
|plex.ingress.enabled | If true, creates the ingress resource for the application | true |
|plex.ingress.annotations | Additional field for annotations, if needed | {} |
|plex.ingress.path | The path where the application is exposed | /plex |
|plex.ingress.tls.enabled | If true, tls is enabled | false |
|plex.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |

# Sonarr

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| sonarr.container.port | The port in use by the container | 8989 | 
| sonarr.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
| sonarr.service.port | The port assigned to the service | 8989 |
| sonarr.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
| sonarr.service.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false 
| sonarr.ingress.enabled | If true, creates the ingress resource for the application | true |
| sonarr.ingress.annotations | Additional field for annotations, if needed | {} |
| sonarr.ingress.path | The path where the application is exposed | /sonarr |
| sonarr.ingress.tls.enabled | If true, tls is enabled | false |
| sonarr.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |

# Radarr

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| radarr.container.port | The port in use by the container | 7878 | 
| radarr.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
| radarr.service.port | The port assigned to the service | 7878 |
| radarr.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
| radarr.service.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| radarr.ingress.enabled | If true, creates the ingress resource for the application | true |
| radarr.ingress.annotations | Additional field for annotations, if needed | {} |
| radarr.ingress.path | The path where the application is exposed | /radarr  |
| radarr.ingress.tls.enabled | If true, tls is enabled | false |
| radarr.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |

# Jackett

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| jackett.container.port | The port in use by the container | 9117 | 
| jackett.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
| jackett.service.port | The port assigned to the service | 9117 |
| jackett.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
| jackett.service.extraLBService | If true, it creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| jackett.ingress.enabled | If true, creates the ingress resource for the application | true |
| jackett.ingress.annotations | Additional field for annotations, if needed | {} |
| jackett.ingress.path | The path where the application is exposed | /jackett |
| jackett.ingress.tls.enabled | If true, tls is enabled | false |
| jackett.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |

# Transmission

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| transmission.container.port | The port in use by the container | 9091 | 
| transmission.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
| transmission.service.port | The port assigned to the service | 9091 |
| transmission.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
| transmission.service.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| transmission.ingress.enabled | If true, creates the ingress resource for the application | true |
| transmission.ingress.annotations | Additional field for annotations, if needed | {} |
| transmission.ingress.path | The path where the application is exposed | /transmission |
| transmission.ingress.tls.enabled | If true, tls is enabled | false |
| transmission.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |

## About the project

This project is intended as an exercise, and absolutely for fun. Don't use it to commit piracy. 

Also feel free to contribute and extend it!

