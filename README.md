## Go to Killerkoda playground : https://killercoda.com/playgrounds/scenario/kubernetes

## First create wordpress + mysql application through docker-compose - run this

```code
docker-compose up -d
```

<img width="1339" height="204" alt="image" src="https://github.com/user-attachments/assets/35722598-525a-41a7-b67b-481b1c2d887c" />

<img width="1364" height="526" alt="image" src="https://github.com/user-attachments/assets/7cd73f50-7e0f-4d05-bc44-50a41fcb38a3" />


## Create Service Account (SA + Role + RoleBinding)

```code
kubectl create -f monitoring-sa.yml
```


<img width="1036" height="149" alt="image" src="https://github.com/user-attachments/assets/333f6d0e-baf1-45c4-98c7-0c924d4d08cb" />


## Run Node-Exporter DaemonSet resource

```code
kubectl create -f https://raw.githubusercontent.com/prometheus-operator/kube-prometheus/refs/heads/main/manifests/nodeExporter-daemonset.yaml
```

<img width="1011" height="121" alt="image" src="https://github.com/user-attachments/assets/f701100d-db53-404b-bd67-04649d2880e3" />



