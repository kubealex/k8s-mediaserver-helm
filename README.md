# k8s-mediaserver-helm
Repo for k8s-mediaserver helm chart, backing **[k8s-mediaserver-operator](https://github.com/kubealex/k8s-mediaserver-operator)**

# General config

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| general.ingress_host | The hostname to use in ingress definition, this will be the hostname where the applications will be exposed  | k8s-mediaserver.k8s.test |
| general.plex_ingress_host | The hostname to use for **PLEX** as it must be exposed on a / dedicated path  | k8s-plex.k8s.test |
| general.image_tag | The name of the image tag (arm32v7-latest, arm64v8-latest, development)  | latest |
| general.pgid | The GID for the process | 1000 |
| general.puid | The UID for the process | 1000 |
| general.nodeSelector | Node Selector for all the pods | {} |
| general.storage.customVolume | Flag if you want to supply your own volume and not use a PVC | false |
| general.storage.pvcName  | Name of the persistenVolumeClaim configured in deployments | mediaserver-pvc |
| general.storage.pvcStorageClass  | Specifies a storageClass for the PVC | "" |
| general.storage.size | Size of the persistenVolume | 50Gi |
| general.storage.subPaths.tv | Default subpath for tv series folder on used storage | media/tv |
| general.storage.subPaths.movies | Default subpath for movies folder on used storage | media/movies |
| general.storage.subPaths.downloads | Default root path for downloads for both sabnzbd and transmission on used storage | downloads |
| general.storage.subPaths.transmission | Default subpath for transmission downloads on used storage | general.storage.subPaths.downloads/transmission |
| general.storage.subPaths.sabnzbd | Default subpath for sabnzbd downloads on used storage | general.storage.subPaths.downloads/sabnzbd |
| general.storage.subPaths.config | Default subpath for all config files on used storage | config |
| general.storage.volumes | Supply custom volume to be mounted for all services | {} |

# Plex

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| plex.enabled | Flag if you want to enable plex | true | 
| plex.claim | **IMPORTANT** Token from your account, needed to claim the server | CHANGEME |
| plex.replicaCount | Number of replicas serving plex | 1 | 
| plex.container.port | The port in use by the container | 32400 | 
| plex.service.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) | ClusterIP |
| plex.service.port | The port assigned to the service | 32400 |
| plex.service.nodePort | In case of service.type NodePort, the nodePort to use | "" |
| plex.service.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| plex.ingress.enabled | If true, creates the ingress resource for the application | true |
| plex.ingress.annotations | Additional field for annotations, if needed | {} |
| plex.ingress.path | The path where the application is exposed | /plex |
| plex.ingress.tls.enabled | If true, tls is enabled | false |
| plex.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |
| plex.resources | Limits and Requests for the container | {} | 

# Sonarr

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| sonarr.enabled | Flag if you want to enable sonarr | true | 
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
| sonarr.resources | Limits and Requests for the container | {} |

# Radarr

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| radarr.enabled | Flag if you want to enable radarr | true | 
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
| radarr.resources | Limits and Requests for the container | {} |

# Jackett

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| jackett.enabled | Flag if you want to enable jackett | true | 
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
| jackett.resources | Limits and Requests for the container | {} |

# Transmission

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| transmission.enabled | Flag if you want to enable transmission | true | 
| transmission.container.port.utp | The port in use by the container | 9091 | 
| transmission.container.port.peer | The port in use by the container for peer connection | 51413 | 
| transmission.service.utp.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) for transmission itself | ClusterIP |
| transmission.service.utp.port | The port assigned to the service for transmission itself | 9091 |
| transmission.service.utp.nodePort | In case of service.type NodePort, the nodePort to use for transmission itself | "" |
| transmission.service.utp.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| transmission.service.peer.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) for peer port | ClusterIP |
| transmission.service.peer.port | The port assigned to the service for peer port | 51413 |
| transmission.service.peer.nodePort | In case of service.type NodePort, the nodePort to use for peer port | "" |
| transmission.service.peer.nodePortUDP | In case of service.type NodePort, the nodePort to use for peer port UDP service | "" |
| transmission.service.peer.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| transmission.ingress.enabled | If true, creates the ingress resource for the application | true |
| transmission.ingress.annotations | Additional field for annotations, if needed | {} |
| transmission.ingress.path | The path where the application is exposed | /transmission |
| transmission.ingress.tls.enabled | If true, tls is enabled | false |
| transmission.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" |
| transmission.config.auth.enabled | Enables authentication for transmission | false |
| transmission.config.auth.username | Username for transmission | "" |
| transmission.config.auth.password | Password for transmission | "" | 
| transmission.resources | Limits and Requests for the container | {} |

# Sabnzbd

| Config path | Meaning | Default | 
| ------------ | ------------ | ------------ |
| sabnzbd.enabled | Flag if you want to enable sabnzbd | true | 
| sabnzbd.container.port.http | The port in use by the container | 8080 | 
| sabnzbd.container.port.https | The port in use by the container for peer connection | 9090 | 
| sabnzbd.service.http.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) for sabnzbd itself | ClusterIP |
| sabnzbd.service.http.port | The port assigned to the service for sabnzbd itself | 9091 |
| sabnzbd.service.http.nodePort | In case of service.type NodePort, the nodePort to use for sabnzbd itself | "" |
| sabnzbd.service.http.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| sabnzbd.service.https.type | The kind of Service (ClusterIP/NodePort/LoadBalancer) for https port | ClusterIP |
| sabnzbd.service.https.port | The port assigned to the service for peer port | 51413 |
| sabnzbd.service.https.nodePort | In case of service.type NodePort, the nodePort to use for https port | "" |
| sabnzbd.service.https.extraLBService | If true, creates an additional LoadBalancer service with '-lb' suffix (requires a cloud provider or metalLB) | false | 
| sabnzbd.ingress.enabled | If true, creates the ingress resource for the application | true |
| sabnzbd.ingress.annotations | Additional field for annotations, if needed | {} |
| sabnzbd.ingress.path | The path where the application is exposed | /sabnzbd |
| sabnzbd.ingress.tls.enabled | If true, tls is enabled | false |
| sabnzbd.ingress.tls.secretName | Name of the secret holding certificates for the secure ingress | "" | 
| sabnzbd.resources | Limits and Requests for the container | {} |

## About the project

This project is intended as an exercise, and absolutely for fun. Don't use it to commit piracy. 

Also feel free to contribute and extend it!

