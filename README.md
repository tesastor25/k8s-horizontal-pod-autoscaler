# Use Horizontal Pod Autoscaler in Kubernetes
#### Steps:
```
wget https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.7/components.yaml
```
#### Please edit component.yaml and add the below lines after image tag:
```
command:
- /metrics-server
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP
```
#### Deploy metrics-server on kubernetes cluster
```
kubectl apply -f components.yaml
```

#### Deploy nginx-deployment.yaml and nginx-svc.yaml

```
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-svc.yaml
```

#### Siege installation on centos:
```
sudo yum install epel-release -y
sudo yum install siege -y
```
#### Apply the HPA on deployment application
```
kubectl autoscale deploy <deployment_name> --min 1 --max 5 --cpu-percent 20
```
#### Verify and Run siege command to simulate traffic on k8s cluster
```
which siege
siege -q -c 5 -t 2m http://k8smaster1:<svc-port-number>
```



