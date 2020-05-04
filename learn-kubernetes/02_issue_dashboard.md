## Dashboard problem
chech pods status
```bash
$ kubectl get pods -o wide --all-namespaces
NAMESPACE              NAME                                         READY   STATUS             RESTARTS   AGE    IP                NODE      NOMINATED NODE   READINESS GATES
kubernetes-dashboard   dashboard-metrics-scraper-6b4884c9d5-w4s2k   1/1     Running            1          40h    192.168.195.131   knode1    <none>           <none>
kubernetes-dashboard   kubernetes-dashboard-7b544877d5-6bwgg        0/1     ImagePullBackOff   137        40h    192.168.195.132   knode1    <none>           <none>
```

## See inside a Pod
```bash
$ kubectl describe pod kubernetes-dashboard-7b544877d5-6bwgg -n kubernetes-dashboard
Name:         kubernetes-dashboard-7b544877d5-6bwgg
Namespace:    kubernetes-dashboard
Priority:     0
Node:         knode1/192.168.1.11
Start Time:   Wed, 22 Apr 2020 18:00:09 +1200
Labels:       k8s-app=kubernetes-dashboard
              pod-template-hash=7b544877d5
Annotations:  cni.projectcalico.org/podIP: 192.168.195.132/32
Status:       Running
IP:           192.168.195.132
IPs:
  IP:           192.168.195.132
Controlled By:  ReplicaSet/kubernetes-dashboard-7b544877d5
Containers:
  kubernetes-dashboard:
    Container ID:  docker://89caed2949d1411e329572fb608dc0e2aaac739dfa6036174f54c41ae0191ebc
    Image:         kubernetesui/dashboard:v2.0.0
    Image ID:      docker-pullable://kubernetesui/dashboard@sha256:06868692fb9a7f2ede1a06de1b7b32afabc40ec739c1181d83b5ed3eb147ec6e
    Port:          8443/TCP
    Host Port:     0/TCP
    Args:
      --auto-generate-certificates
      --namespace=kubernetes-dashboard
    State:          Waiting
      Reason:       ImagePullBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Fri, 24 Apr 2020 10:15:37 +1200
      Finished:     Fri, 24 Apr 2020 10:16:07 +1200
    Ready:          False
    Restart Count:  137
    Liveness:       http-get https://:8443/ delay=30s timeout=30s period=10s #success=1 #failure=3
    Environment:    <none>
    Mounts:
      /certs from kubernetes-dashboard-certs (rw)
      /tmp from tmp-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kubernetes-dashboard-token-vrzvm (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             False 
  ContainersReady   False 
  PodScheduled      True 
Volumes:
  kubernetes-dashboard-certs:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  kubernetes-dashboard-certs
    Optional:    false
  tmp-volume:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  kubernetes-dashboard-token-vrzvm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  kubernetes-dashboard-token-vrzvm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  kubernetes.io/os=linux
Tolerations:     node-role.kubernetes.io/master:NoSchedule
                 node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason   Age                    From             Message
  ----     ------   ----                   ----             -------
  Normal   Created  22m (x88 over 15h)     kubelet, knode1  Created container kubernetes-dashboard
  Warning  BackOff  7m2s (x1980 over 15h)  kubelet, knode1  Back-off restarting failed container
  Warning  Failed   114s (x8 over 67m)     kubelet, knode1  Error: ImagePullBackOff
erictan@kmaster ~/.kube> kubectl describe pod dashboard-metrics-scraper-6b4884c9d5-w4s2k -n kubernetes-dashboard
Name:         dashboard-metrics-scraper-6b4884c9d5-w4s2k
Namespace:    kubernetes-dashboard
Priority:     0
Node:         knode1/192.168.1.11
Start Time:   Wed, 22 Apr 2020 18:00:09 +1200
Labels:       k8s-app=dashboard-metrics-scraper
              pod-template-hash=6b4884c9d5
Annotations:  cni.projectcalico.org/podIP: 192.168.195.131/32
              seccomp.security.alpha.kubernetes.io/pod: runtime/default
Status:       Running
IP:           192.168.195.131
IPs:
  IP:           192.168.195.131
Controlled By:  ReplicaSet/dashboard-metrics-scraper-6b4884c9d5
Containers:
  dashboard-metrics-scraper:
    Container ID:   docker://d721c57edcd3f725b053151c119b803cbb043d1d9011dbe3c58a25de544b4405
    Image:          kubernetesui/metrics-scraper:v1.0.4
    Image ID:       docker-pullable://kubernetesui/metrics-scraper@sha256:555981a24f184420f3be0c79d4efb6c948a85cfce84034f85a563f4151a81cbf
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 23 Apr 2020 19:14:30 +1200
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Wed, 22 Apr 2020 18:00:42 +1200
      Finished:     Wed, 22 Apr 2020 21:54:00 +1200
    Ready:          True
    Restart Count:  1
    Liveness:       http-get http://:8000/ delay=30s timeout=30s period=10s #success=1 #failure=3
    Environment:    <none>
    Mounts:
      /tmp from tmp-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kubernetes-dashboard-token-vrzvm (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  tmp-volume:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  kubernetes-dashboard-token-vrzvm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  kubernetes-dashboard-token-vrzvm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  kubernetes.io/os=linux
Tolerations:     node-role.kubernetes.io/master:NoSchedule
                 node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:          <none>
```

## Delete the deployment of kubernetes-dashboard
```bash
$ kubectl delete deployments kubernetes-dashboard -n kube-system
deployment.apps "kubernetes-dashboard" deleted
```
Install v2.0.0 dashboard, compatible with 1.18
```bash
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml

namespace/kubernetes-dashboard created
serviceaccount/kubernetes-dashboard created
service/kubernetes-dashboard created
secret/kubernetes-dashboard-certs created
secret/kubernetes-dashboard-csrf created
secret/kubernetes-dashboard-key-holder created
configmap/kubernetes-dashboard-settings created
role.rbac.authorization.k8s.io/kubernetes-dashboard created
clusterrole.rbac.authorization.k8s.io/kubernetes-dashboard created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
deployment.apps/kubernetes-dashboard created
service/dashboard-metrics-scraper created
deployment.apps/dashboard-metrics-scraper created
```
URL:
https://x.x.x.x:6443/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login


## delete namespaces kubernetes-dashboard

```bash
$ kubectl -n kubernetes-dashboard delete pod,svc --all
pod "dashboard-metrics-scraper-6b4884c9d5-w4s2k" deleted
pod "kubernetes-dashboard-7b544877d5-6bwgg" deleted
service "dashboard-metrics-scraper" deleted
service "kubernetes-dashboard" deleted

$ kubectl get pods -o wide --all-namespaces
NAMESPACE              NAME                                         READY   STATUS    RESTARTS   AGE    IP                NODE      NOMINATED NODE   READINESS GATES
kubernetes-dashboard   dashboard-metrics-scraper-6b4884c9d5-wvtvj   1/1     Running   0          23s    192.168.195.134   knode1    <none>           <none>
kubernetes-dashboard   kubernetes-dashboard-7b544877d5-tznjk        1/1     Running   0          23s    192.168.195.133   knode1    <none>           <none>
```

even if you delete pods and service, it will restart again and again, you have to **delete deployment**. please refer here for more detail [Kubernetes pod gets recreated when deleted] (https://stackoverflow.com/questions/40686151/kubernetes-pod-gets-recreated-when-deleted)
```bash
$ kubectl get deployments --all-namespaces
NAMESPACE              NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-dashboard   dashboard-metrics-scraper   0/1     1            0           43h
kubernetes-dashboard   kubernetes-dashboard        0/1     1            0           43h

$ kubectl delete -n kubernetes-dashboard deployment kubernetes-dashboard
deployment.apps "kubernetes-dashboard" deleted

$ kubectl delete -n kubernetes-dashboard deployment dashboard-metrics-scraper
deployment.apps "dashboard-metrics-scraper" deleted
```
not yet tried
```bash
kubectl logs -n kubernetes-dashboard kubernetes-metrics-scraper-86456cdd8f-5jbtv | more
kubectl -n kubernetes-dashboard get endpoints -o wide
```
