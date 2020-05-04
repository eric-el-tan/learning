# Architecture
1. [Installation](https://github.com/eric-el-tan/learn-kubernetes/blob/master/01_installation.md)
	1. [Static IP]
	1. [Setup 3 ubuntu]
1. [Issue: Kubernetes Dashboard](https://github.com/eric-el-tan/learn-kubernetes/blob/master/02_issue_dashboard.md)

**Appendix**
1. [Kubernetes Architecture](https://www.edureka.co/blog/kubernetes-architecture)
1. [Kubernetes cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet)
1. [Edit Markdown file](https://guides.github.com/features/mastering-markdown)
1. [Configure new Ubuntu OS](https://github.com/eric-el-tan/learn-kubernetes/blob/master/99_configure_ubuntu.md)


# Useful command
get pods Health check
```bash 
$ kubectl get pods -o wide --all-namespaces
```

get nodes
```bash
$ kubectl get nodes
NAME      STATUS   ROLES    AGE    VERSION
kmaster   Ready    master   162m   v1.18.2
knode1    Ready    <none>   5m5s   v1.18.2
```
get version
```bash
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.2", GitCommit:"52c56ce7a8272c798dbc29846288d7cd9fbae032", GitTreeState:"clean", BuildDate:"2020-04-16T11:56:40Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.2", GitCommit:"52c56ce7a8272c798dbc29846288d7cd9fbae032", GitTreeState:"clean", BuildDate:"2020-04-16T11:48:36Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
```
