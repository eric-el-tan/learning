# [Uninstall](https://stackoverflow.com/questions/44698283/how-to-completely-uninstall-kubernetes)

```bash
kubeadm reset
sudo apt-get purge kubeadm kubectl kubelet kubernetes-cni kube*   
sudo apt-get autoremove  
sudo rm -rf ~/.kube
```

> kubeadm reset

```bash
[reset] Reading configuration from the cluster...
[reset] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
W0507 10:43:11.588600   15880 reset.go:99] [reset] Unable to fetch the kubeadm-config ConfigMap from cluster: failed to get config map: Get https://192.168.1.14:6443/api/v1/namespaces/kube-system/configmaps/kubeadm-config?timeout=10s: dial tcp 192.168.1.14:6443: connect: no route to host
[reset] WARNING: Changes made to this host by 'kubeadm init' or 'kubeadm join' will be reverted.
[reset] Are you sure you want to proceed? [y/N]: y
[preflight] Running pre-flight checks
W0507 10:43:30.470871   15880 removeetcdmember.go:79] [reset] No kubeadm config, using etcd pod spec to get data directory
[reset] Stopping the kubelet service
[reset] Unmounting mounted directories in "/var/lib/kubelet"
[reset] Deleting contents of config directories: [/etc/kubernetes/manifests /etc/kubernetes/pki]
[reset] Deleting files: [/etc/kubernetes/admin.conf /etc/kubernetes/kubelet.conf /etc/kubernetes/bootstrap-kubelet.conf /etc/kubernetes/controller-manager.conf /etc/kubernetes/scheduler.conf]
[reset] Deleting contents of stateful directories: [/var/lib/etcd /var/lib/kubelet /var/lib/dockershim /var/run/kubernetes /var/lib/cni]

The reset process does not clean CNI configuration. To do so, you must remove /etc/cni/net.d

The reset process does not reset or clean up iptables rules or IPVS tables.
If you wish to reset iptables, you must do so manually by using the "iptables" command.

If your cluster was setup to utilize IPVS, run ipvsadm --clear (or similar)
to reset your system's IPVS tables.

The reset process does not clean your kubeconfig files and you must remove them manually.
Please, check the contents of the $HOME/.kube/config file.
```

> sudo apt-get purge kubeadm kubectl kubelet kubernetes-cni kube*   

```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  conntrack cri-tools ebtables ethtool socat
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  kubeadm* kubectl* kubelet* kubernetes-cni*
0 upgraded, 0 newly installed, 4 to remove and 326 not upgraded.
1 not fully installed or removed.
After this operation, 247 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 139335 files and directories currently installed.)
Removing kubeadm (1.18.1-00) ...
Removing kubectl (1.18.1-00) ...
Removing kubelet (1.18.1-00) ...
Removing kubernetes-cni (0.7.5-00) ...
Setting up initramfs-tools (0.130ubuntu3.8) ...
update-initramfs: deferring update (trigger activated)
(Reading database ... 139316 files and directories currently installed.)
Purging configuration files for kubelet (1.18.1-00) ...
Purging configuration files for kubeadm (1.18.1-00) ...
Processing triggers for initramfs-tools (0.130ubuntu3.8) ...
update-initramfs: Generating /boot/initrd.img-5.0.0-23-generic
/usr/sbin/mkinitramfs: 1: /usr/sbin/mkinitramfs: getopt: Exec format error
W: non-GNU getopt
update-initramfs: failed for /boot/initrd.img-5.0.0-23-generic with 1.
dpkg: error processing package initramfs-tools (--configure):
 installed initramfs-tools package post-installation script subprocess returned error exit status 1
E: Sub-process /usr/bin/dpkg returned an error code (1)

```


> sudo apt-get autoremove  
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  conntrack cri-tools ebtables ethtool socat
0 upgraded, 0 newly installed, 5 to remove and 326 not upgraded.
1 not fully installed or removed.
After this operation, 28.0 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 139314 files and directories currently installed.)
Removing conntrack (1:1.4.4+snapshot20161117-6ubuntu2) ...
Removing cri-tools (1.13.0-00) ...
Removing ebtables (2.0.10.4-3.5ubuntu2.18.04.3) ...
Removing ethtool (1:4.15-0ubuntu1) ...
Removing socat (1.7.3.2-2ubuntu2) ...
Setting up initramfs-tools (0.130ubuntu3.8) ...
update-initramfs: deferring update (trigger activated)
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for initramfs-tools (0.130ubuntu3.8) ...
update-initramfs: Generating /boot/initrd.img-5.0.0-23-generic
/usr/sbin/mkinitramfs: 1: /usr/sbin/mkinitramfs: getopt: Exec format error
W: non-GNU getopt
update-initramfs: failed for /boot/initrd.img-5.0.0-23-generic with 1.
dpkg: error processing package initramfs-tools (--configure):
 installed initramfs-tools package post-installation script subprocess returned error exit status 1
Errors were encountered while processing:
 initramfs-tools
E: Sub-process /usr/bin/dpkg returned an error code (1)
```
> sudo rm -rf ~/.kube