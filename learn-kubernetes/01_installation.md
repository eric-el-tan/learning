# Installation
reference: [Text](https://www.edureka.co/blog/install-kubernetes-on-ubuntu) / [Video](https://www.youtube.com/watch?v=UWg3ORRRF60)
1. [Prerequisites to install Kubernetes](#Prerequisites-to-install-Kubernetes)
1. [Setting up Kubernetes environment](#Setting-up-kubernetes-environment)
1. [Installing Kubeadm Kubelet and Kubectl](#Installing-Kubeadm-Kubelet-Kubectl)
1. [Starting Kubernetes Cluster](#Starting-Kubernetes-Cluster) (Master only)
1. [Joining the cluster](#Joining-Cluster) (Node only)

## Prerequisites to install Kubernetes
Master:	2 GB RAM, 2 Cores of CPU
Slave/ Node: 1 GB RAM, 1 Core of CPU

## Setting up Kubernetes environment
```bash
$ sudo su
# apt-get update
```
Turn Off Swap Space
```bash
# swapoff -a
# nano /etc/fstab
# UUID=...
```
Update the hostname
```bash
# nano /etc/hostname
kmaster
```
Setting Static IP Addresses [with internet (Ubt16)](https://askubuntu.com/questions/264768/how-to-configure-static-ip-in-ubuntu-running-on-virtual-box) [with dns](https://help.slingshot.co.nz/hc/en-us/articles/115005082373-What-are-Slingshot-s-DNS-addresses-) or [Ubt18](https://askubuntu.com/questions/1073031/ubuntu-18-04-internet-connection-not-working-using-vmware-fusion)
```bash 
# nano /etc/network/interfaces
auto enp0s3
iface enp0s3 inet static
address <IP-Address-Of-VM>
netmask 255.255.255.0
gateway <IP-Address-Of-ROUTER>
dns-nameservers <IP-Address-Of-PRIMARY_DNS> <IP-Address-Of-ALTERNATIVE_DNS>
```
i.e.
```bash
auto enp0s3
iface enp0s3 inet static
address 192.168.1.99
netmask 255.255.255.0
gateway 192.168.1.1
dns-nameservers 202.180.64.10 202.180.64.11
```
if not working, may try this
```bash
auto enp0s3
iface enp0s3 inet dhcp
```
then, restart network
```
sudo /etc/init.d/networking restart
sudo lshw -C network
ping www.google.com
```

Update The Hosts File With IPs Of Master & Node
```bash
	# ifconfig
		
	# nano /etc/hosts
	192.168.1.99	kmaster
	192.168.1.11	knode1
	192.168.1.12	knode2

```
Install OpenSSH-Server
```bash
# apt-get install openssh-server 
```
Run the following commands before installing the Kubernetes environment.
```bash
# apt-get update && apt-get install -y apt-transport-https curl
# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
# cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
# apt-get update
```

## Installing Kubeadm Kubelet Kubectl
```
# apt-get install -y kubelet kubeadm kubectl 
```

Updating Kubernetes Configuration
```bash
# nano /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
```

```bash
# Note: This dropin only works with kubeadm and kubelet v1.11+
[Service]
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/boo$
Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"

# add this line
Environment="cgroup-driver=systemd/cgroup-driver=cgroupfs"

# This is a file that "kubeadm init" and "kubeadm join" generates at runtime, p$
EnvironmentFile=-/var/lib/kubelet/kubeadm-flags.env
# This is a file that the user can use for overrides of the kubelet args as a l$
# the .NodeRegistration.KubeletExtraArgs object in the configuration files inst$
EnvironmentFile=-/etc/default/kubelet
ExecStart=
ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBEL$
```


## Starting Kubernetes Cluster
**On Master only**

#### Step 1: start cluster (run as root)
```bash
$ sudo su
# kubeadm init --apiserver-advertise-address=<ip-address-of-kmaster-vm> --pod-network-cidr=192.168.0.0/16
```
i.e.
```bash
# kubeadm init --apiserver-advertise-address=192.168.1.99 --pod-network-cidr=192.168.0.0/16

W0422 04:34:36.113526    3932 configset.go:202] WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
[init] Using Kubernetes version: v1.18.2
[preflight] Running pre-flight checks
	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [kmaster kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.1.99]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [kmaster localhost] and IPs [192.168.1.99 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [kmaster localhost] and IPs [192.168.1.99 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
W0422 04:35:51.026411    3932 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[control-plane] Creating static Pod manifest for "kube-scheduler"
W0422 04:35:51.028052    3932 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 27.006442 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node kmaster as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node kmaster as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: 0haev9.z0x82jnn9fot5lsk
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.1.99:6443 --token 0haev9.z0x82jnn9fot5lsk \
    --discovery-token-ca-cert-hash sha256:15ac39f66e190c02a9cb1e26c19059c6982352aa91e6b7edb605ddf35f5dd996 
```

#### Step 2: config file (run as a non-root user)
```bash
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

(...) is not supported. In fish, please use '(id)'.
fish: sudo chown $(id -u):$(id -g) $HOME/.kube/config

$ sudo chown (id -u):(id -g) $HOME/.kube/config
```

**Health check** verify if kubectl is working or not
```bash
$ kubectl get pods -o wide --all-namespaces

NAMESPACE     NAME                              READY   STATUS    RESTARTS   AGE     IP             NODE      NOMINATED NODE   READINESS GATES
kube-system   coredns-66bff467f8-5qrlh          0/1     Pending   0          5m6s    <none>         <none>    <none>           <none>
kube-system   coredns-66bff467f8-tqfvx          0/1     Pending   0          5m6s    <none>         <none>    <none>           <none>
kube-system   etcd-kmaster                      1/1     Running   0          5m16s   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-apiserver-kmaster            1/1     Running   0          5m16s   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-controller-manager-kmaster   1/1     Running   0          5m16s   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-proxy-stw7l                  1/1     Running   0          5m6s    192.168.1.99   kmaster   <none>           <none>
kube-system   kube-scheduler-kmaster            1/1     Running   0          5m16s   192.168.1.99   kmaster   <none>           <none>
```

#### Step 3: install pod network
You will notice from the previous command, that all the pods are running except one: ‘kube-dns’. For resolving this we will install a pod network. To install the CALICO pod network, run the following command:

[use Calico v3.10](https://docs.projectcalico.org/v3.10/getting-started/kubernetes/installation/calico) ref: [yml](https://github.com/eric-el-tan/learn-kubernetes/blob/master/calico.yaml) 
```bash
curl <url> -O
```

```bash
$ kubectl apply -f https://docs.projectcalico.org/v3.10/manifests/calico.yaml

configmap/calico-config configured
customresourcedefinition.apiextensions.k8s.io/felixconfigurations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamblocks.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/blockaffinities.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamhandles.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamconfigs.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/bgppeers.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/bgpconfigurations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ippools.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/hostendpoints.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/clusterinformations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/globalnetworkpolicies.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/globalnetworksets.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/networkpolicies.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/networksets.crd.projectcalico.org created
clusterrole.rbac.authorization.k8s.io/calico-kube-controllers configured
clusterrolebinding.rbac.authorization.k8s.io/calico-kube-controllers configured
clusterrole.rbac.authorization.k8s.io/calico-node created
clusterrolebinding.rbac.authorization.k8s.io/calico-node created
daemonset.apps/calico-node created
serviceaccount/calico-node created
deployment.apps/calico-kube-controllers created
serviceaccount/calico-kube-controllers unchanged
```
**Health check** again, verify if dns is working or not
```bash
$ kubectl get pods -o wide --all-namespaces

NAMESPACE     NAME                                      READY   STATUS              RESTARTS   AGE   IP             NODE      NOMINATED NODE   READINESS GATES
kube-system   calico-kube-controllers-dc4469c7f-h92f2   0/1     ContainerCreating   0          48s   <none>         kmaster   <none>           <none>
kube-system   calico-node-zv2j5                         0/1     PodInitializing     0          47s   192.168.1.99   kmaster   <none>           <none>
kube-system   coredns-66bff467f8-5qrlh                  0/1     ContainerCreating   0          29m   <none>         kmaster   <none>           <none>
kube-system   coredns-66bff467f8-tqfvx                  0/1     ContainerCreating   0          29m   <none>         kmaster   <none>           <none>
kube-system   etcd-kmaster                              1/1     Running             0          29m   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-apiserver-kmaster                    1/1     Running             0          29m   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-controller-manager-kmaster           1/1     Running             0          29m   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-proxy-stw7l                          1/1     Running             0          29m   192.168.1.99   kmaster   <none>           <none>
kube-system   kube-scheduler-kmaster                    1/1     Running             0          29m   192.168.1.99   kmaster   <none>           <none>
```

#### Step 4: install dashboard
ref: [use dashboard 1.18.2](https://github.com/kubernetes/dashboard) [yml](https://github.com/eric-el-tan/learn-kubernetes/blob/master/kubernetes-dashboard.yaml) 
```bash
$ kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
secret/kubernetes-dashboard-certs created
serviceaccount/kubernetes-dashboard created
role.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
deployment.apps/kubernetes-dashboard created
service/kubernetes-dashboard created
```

**Health check** again, verify if dashboard is working or not
```bash
$ kubectl get pods -o wide --all-namespaces

NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE   IP              NODE      NOMINATED NODE   READINESS GATES
kube-system   calico-kube-controllers-dc4469c7f-h92f2   1/1     Running   0          18m   192.168.189.3   kmaster   <none>           <none>
kube-system   calico-node-zv2j5                         1/1     Running   0          18m   192.168.1.99    kmaster   <none>           <none>
kube-system   coredns-66bff467f8-5qrlh                  1/1     Running   0          46m   192.168.189.2   kmaster   <none>           <none>
kube-system   coredns-66bff467f8-tqfvx                  1/1     Running   0          46m   192.168.189.1   kmaster   <none>           <none>
kube-system   etcd-kmaster                              1/1     Running   0          46m   192.168.1.99    kmaster   <none>           <none>
kube-system   kube-apiserver-kmaster                    1/1     Running   0          46m   192.168.1.99    kmaster   <none>           <none>
kube-system   kube-controller-manager-kmaster           1/1     Running   0          46m   192.168.1.99    kmaster   <none>           <none>
kube-system   kube-proxy-stw7l                          1/1     Running   0          46m   192.168.1.99    kmaster   <none>           <none>
kube-system   kube-scheduler-kmaster                    1/1     Running   0          46m   192.168.1.99    kmaster   <none>           <none>
kube-system   kubernetes-dashboard-975499656-74796      1/1     Running   0          11m   192.168.189.4   kmaster   <none>           <none>
```
Your dashboard is now ready with it’s the pod in the running state.
**Unfortunately, in my experience, v1.10.1 only work for a while, then the kubernetes dashboard has error and crash endlessly**

#### Step 5: visable dashboard
By default dashboard will not be visible on the Master VM. Run the following command in the command line:

Start dashboard in **new terminal**
```bash
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```
Then you will get something like this:

To view the dashboard in the browser, navigate to the following address in the browser of your Master VM: http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

You will then be prompted with this page, to enter the credentials:

![sample image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/05/kubernetes-dashboard.png)


#### Step 6: create the service account for the dashboard and get it’s credentials
In this step, we will create the service account for the dashboard and get it’s credentials.
**Note: Run all these commands in a new terminal, or your kubectl proxy command will stop.**

1. This command will create a service account for dashboard in the default namespace
```bash
$ kubectl create serviceaccount dashboard -n default
serviceaccount/dashboard created
```
2. This command will add the cluster binding rules to your dashboard account
```bash
$ kubectl create clusterrolebinding dashboard-admin -n default --clusterrole=cluster-admin --serviceaccount=default:dashboard
clusterrolebinding.rbac.authorization.k8s.io/dashboard-admin created
```

3. This command will give you the token required for your dashboard login
```bash
$ kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
$(...) is not supported. In fish, please use '(kubectl)'.
fish: kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
$ kubectl get secret (kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
```
You should get the token like this:
```bash
eyJhbGciOiJSUzI1NiIsImtpZCI6IlRwQmFzYjhEMllFeS00Q2ZyVGVETXBDazlTQXoyMGw2cnpTMzhvYmprVGsifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRhc2hib2FyZC10b2tlbi1qeDVidCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJkYXNoYm9hcmQiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI3NWVkYmRjOS1hYjVlLTRiZmUtYTFkOS01Njc3ZjllNzgyNjgiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpkYXNoYm9hcmQifQ.cpJ1JiPG2GWv-5B1fTokCOuD16kOIATmDYvDS--4Tb6tDztZaiO2aUaCR8-SRhtyBHOKixSEl2dB16Ik6blCLOb9P_ihnJWNl_QX6vgPT3PaTZJMEP1btIcWtb610isdHDP_LzVBThOcEDBqD0Zd21yUQi5WgMO5GaGgWu6F1bq2bP2deqjBHY601Df8KKKfapfLMJ1_RBQKYVBHmGTmIGTwGXdQfJWZXrZ6wrdJ4n3MubDcMhLQcNPgoc5LJvbNqGapWRYsEVKAglvosNuBGEO6-6Ad-y3ZhTvUjzp-BgeI-jpe7XcUJJi6L_vpRP5HQRs7nOregSRKkB0Rcax0mg⏎                          
```

4. Copy this token and paste it in Dashboard Login Page, by selecting token option

![sample image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/05/dashboard-token-entry.png)

Error: kubernetes dashboard the server could not find the requested resource
https://github.com/kubernetes-sigs/kubespray/issues/5347

## Joining Cluster

Steps For Only Kubernetes Node VM (knode)
It is time to get your node, to join the cluster! This is probably the only step that you will be doing on the node, after installing kubernetes on it.

Run the join command that you saved, when you ran ‘kubeadm init’ command on the master.

Note: Run this command with “sudo”. see Step 1.

```bash
sudo kubeadm join 192.168.1.99:6443 \
--token 0haev9.z0x82jnn9fot5lsk \
--discovery-token-ca-cert-hash sha256:15ac39f66e190c02a9cb1e26c19059c6982352aa91e6b7edb605ddf35f5dd996 

[sudo] password for erictan: 
W0422 07:13:30.414307   11180 join.go:346] [preflight] WARNING: JoinControlPane.controlPlane settings will be ignored when control-plane flag is not set.
[preflight] Running pre-flight checks
	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```
