# learn-jenkins

following tutorial of [in28minutes](https://github.com/in28minutes/devops-master-class)


## install docker-compose

- from [docs.docker.com](https://docs.docker.com/compose/install),[how to install docker-compose in Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04)

> sudo curl -L https://github.com/docker/compose/releases/download/1.25.5/docker-compose-Linux-x86_64 -o /usr/local/bin/docker-compose
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   638  100   638    0     0     39      0  0:00:16  0:00:16 --:--:--   184
100 16.7M  100 16.7M    0     0   421k      0  0:00:40  0:00:40 --:--:-- 2240k
```
> sudo chmod +x /usr/local/bin/docker-compose
> docker-compose --version
```
docker-compose version 1.25.5, build 8a1c60f6
```

## install jenkins

ref: [docker image](https://hub.docker.com/r/jenkins/jenkins), [github](https://github.com/jenkinsci/docker/blob/master/README.md)

> cd /var/local/git/eric/devops-master-class/jenkins
> docker-compose up

```
Pulling jenkins (jenkins/jenkins:lts)...
lts: Pulling from jenkins/jenkins
3192219afd04: Pull complete
17c160265e75: Pull complete
cc4fe40d0e61: Pull complete
9d647f502a07: Pull complete
d108b8c498aa: Pull complete
1bfe918b8aa5: Pull complete
dafa1a7c0751: Pull complete
204b3ae87dcc: Pull complete
e7df9c239d2f: Pull complete
6bc3c4bab84d: Pull complete
0fddb90aaa59: Pull complete
f2fe379c9cae: Pull complete
41f205609aa3: Pull complete
44894459a77c: Pull complete
33abd1ee296e: Pull complete
0246d2531788: Pull complete
0265cbd0a929: Pull complete
ea9bcd7318c4: Pull complete
688e1959a331: Pull complete
Digest: sha256:af0110d8f70d2fbaf9429c321dc4e3bc5aae12f708c655f4018e7ed4be0974f5
Status: Downloaded newer image for jenkins/jenkins:lts
Creating jenkins ... done
Attaching to jenkins
jenkins    | Running from: /usr/share/jenkins/jenkins.war
jenkins    | webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")
jenkins    | 2020-04-24 16:29:01.908+0000 [id=1]	INFO	org.eclipse.jetty.util.log.Log#initialized: Logging initialized @726ms to org.eclipse.jetty.util.log.JavaUtilLog
jenkins    | 2020-04-24 16:29:02.138+0000 [id=1]	INFO	winstone.Logger#logInternal: Beginning extraction from war file
jenkins    | 2020-04-24 16:29:05.827+0000 [id=1]	WARNING	o.e.j.s.handler.ContextHandler#setContextPath: Empty contextPath
jenkins    | 2020-04-24 16:29:05.941+0000 [id=1]	INFO	org.eclipse.jetty.server.Server#doStart: jetty-9.4.27.v20200227; built: 2020-02-27T18:37:21.340Z; git: a304fd9f351f337e7c0e2a7c28878dd536149c6c; jvm 1.8.0_242-b08
jenkins    | 2020-04-24 16:29:06.559+0000 [id=1]	INFO	o.e.j.w.StandardDescriptorProcessor#visitServlet: NO JSP Support for /, did not find org.eclipse.jetty.jsp.JettyJspServlet
jenkins    | 2020-04-24 16:29:06.643+0000 [id=1]	INFO	o.e.j.s.s.DefaultSessionIdManager#doStart: DefaultSessionIdManager workerName=node0
jenkins    | 2020-04-24 16:29:06.644+0000 [id=1]	INFO	o.e.j.s.s.DefaultSessionIdManager#doStart: No SessionScavenger set, using defaults
jenkins    | 2020-04-24 16:29:06.649+0000 [id=1]	INFO	o.e.j.server.session.HouseKeeper#startScavenging: node0 Scavenging every 600000ms
jenkins    | 2020-04-24 16:29:07.278+0000 [id=1]	INFO	hudson.WebAppMain#contextInitialized: Jenkins home directory: /var/jenkins_home found at: EnvVars.masterEnvVars.get("JENKINS_HOME")
jenkins    | 2020-04-24 16:29:07.488+0000 [id=1]	INFO	o.e.j.s.handler.ContextHandler#doStart: Started w.@64f857e7{Jenkins v2.222.1,/,file:///var/jenkins_home/war/,AVAILABLE}{/var/jenkins_home/war}
jenkins    | 2020-04-24 16:29:07.545+0000 [id=1]	INFO	o.e.j.server.AbstractConnector#doStart: Started ServerConnector@50378a4{HTTP/1.1, (http/1.1)}{0.0.0.0:8080}
jenkins    | 2020-04-24 16:29:07.546+0000 [id=1]	INFO	org.eclipse.jetty.server.Server#doStart: Started @6365ms
jenkins    | 2020-04-24 16:29:07.548+0000 [id=21]	INFO	winstone.Logger#logInternal: Winstone Servlet Engine running: controlPort=disabled
jenkins    | 2020-04-24 16:29:10.793+0000 [id=28]	INFO	jenkins.InitReactorRunner$1#onAttained: Started initialization
jenkins    | 2020-04-24 16:29:10.893+0000 [id=30]	INFO	jenkins.InitReactorRunner$1#onAttained: Listed all plugins
jenkins    | 2020-04-24 16:29:13.626+0000 [id=28]	INFO	jenkins.InitReactorRunner$1#onAttained: Prepared all plugins
jenkins    | 2020-04-24 16:29:13.636+0000 [id=32]	INFO	jenkins.InitReactorRunner$1#onAttained: Started all plugins
jenkins    | 2020-04-24 16:29:13.646+0000 [id=35]	INFO	jenkins.InitReactorRunner$1#onAttained: Augmented all extensions
jenkins    | 2020-04-24 16:29:15.293+0000 [id=37]	INFO	jenkins.InitReactorRunner$1#onAttained: System config loaded
jenkins    | 2020-04-24 16:29:15.294+0000 [id=37]	INFO	jenkins.InitReactorRunner$1#onAttained: System config adapted
jenkins    | 2020-04-24 16:29:15.294+0000 [id=37]	INFO	jenkins.InitReactorRunner$1#onAttained: Loaded all jobs
jenkins    | 2020-04-24 16:29:15.295+0000 [id=29]	INFO	jenkins.InitReactorRunner$1#onAttained: Configuration for all jobs updated
jenkins    | 2020-04-24 16:29:15.353+0000 [id=50]	INFO	hudson.model.AsyncPeriodicWork#lambda$doRun$0: Started Download metadata
jenkins    | 2020-04-24 16:29:15.382+0000 [id=50]	INFO	hudson.util.Retrier#start: Attempt #1 to do the action check updates server
jenkins    | 2020-04-24 16:29:16.994+0000 [id=35]	INFO	o.s.c.s.AbstractApplicationContext#prepareRefresh: Refreshing org.springframework.web.context.support.StaticWebApplicationContext@3abf6234: display name [Root WebApplicationContext]; startup date [Fri Apr 24 16:29:16 UTC 2020]; root of context hierarchy
jenkins    | 2020-04-24 16:29:16.995+0000 [id=35]	INFO	o.s.c.s.AbstractApplicationContext#obtainFreshBeanFactory: Bean factory for application context [org.springframework.web.context.support.StaticWebApplicationContext@3abf6234]: org.springframework.beans.factory.support.DefaultListableBeanFactory@3f0c43b7
jenkins    | 2020-04-24 16:29:17.010+0000 [id=35]	INFO	o.s.b.f.s.DefaultListableBeanFactory#preInstantiateSingletons: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@3f0c43b7: defining beans [authenticationManager]; root of factory hierarchy
jenkins    | 2020-04-24 16:29:17.287+0000 [id=35]	INFO	o.s.c.s.AbstractApplicationContext#prepareRefresh: Refreshing org.springframework.web.context.support.StaticWebApplicationContext@517f82dd: display name [Root WebApplicationContext]; startup date [Fri Apr 24 16:29:17 UTC 2020]; root of context hierarchy
jenkins    | 2020-04-24 16:29:17.288+0000 [id=35]	INFO	o.s.c.s.AbstractApplicationContext#obtainFreshBeanFactory: Bean factory for application context [org.springframework.web.context.support.StaticWebApplicationContext@517f82dd]: org.springframework.beans.factory.support.DefaultListableBeanFactory@58e6a2d0
jenkins    | 2020-04-24 16:29:17.289+0000 [id=35]	INFO	o.s.b.f.s.DefaultListableBeanFactory#preInstantiateSingletons: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@58e6a2d0: defining beans [filter,legacy]; root of factory hierarchy
jenkins    | 2020-04-24 16:29:17.749+0000 [id=35]	INFO	jenkins.install.SetupWizard#init: 
jenkins    | 
jenkins    | *************************************************************
jenkins    | *************************************************************
jenkins    | *************************************************************
jenkins    | 
jenkins    | Jenkins initial setup is required. An admin user has been created and a password generated.
jenkins    | Please use the following password to proceed to installation:
jenkins    | 
jenkins    | 7f239acdf0824edea2f37f3af98d5bbc
jenkins    | 
jenkins    | This may also be found at: /var/jenkins_home/secrets/initialAdminPassword
jenkins    | 
jenkins    | *************************************************************
jenkins    | *************************************************************
jenkins    | *************************************************************
jenkins    | 
jenkins    | 2020-04-24 16:29:27.605+0000 [id=35]	INFO	jenkins.InitReactorRunner$1#onAttained: Completed initialization
jenkins    | 2020-04-24 16:29:27.626+0000 [id=20]	INFO	hudson.WebAppMain$3#run: Jenkins is fully up and running
jenkins    | 2020-04-24 16:29:28.229+0000 [id=50]	INFO	h.m.DownloadService$Downloadable#load: Obtained the updated data file for hudson.tasks.Maven.MavenInstaller
jenkins    | 2020-04-24 16:29:28.230+0000 [id=50]	INFO	hudson.util.Retrier#start: Performed the action check updates server successfully at the attempt #1
jenkins    | 2020-04-24 16:29:28.235+0000 [id=50]	INFO	hudson.model.AsyncPeriodicWork#lambda$doRun$0: Finished Download metadata. 12,870 ms
```

#### problem: if it failed to download, try fix by this
Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection
fix dns
```
sudo nano /etc/resolv.conf

before:
nameserver 127.0.0.53

after:
nameserver 8.8.8.8
nameserver 8.8.4.4
nameserver 127.0.0.53
```

## setup

- login - http://localhost:8081/login?from=%2F

- copy and paste password 

    - e.g. 0c104b63001c41aebe4e238f0f7d104f

- auto installing plugins

- prepare a sample github repository to be built by jenkins
    - https://github.com/eric-el-tan/jenkins-devops-microservices.git





remove docker-compose
```
rm $(which docker-compose)
```
If you get a permission denied error then you will need to prepend sudo:
```
sudo rm $(which docker-compose)
```
To verify that it was successful, run the following command which should return nothing:
```
which docker-compose
```


## problem Permission: Docker
- [permission problem, need restart](https://blog.51cto.com/daibaiyang119/2436987)
- [Docker in a Docker, need further configure](https://support.cloudbees.com/hc/en-us/articles/360001566111-Set-up-a-Docker-in-Docker-Agent-Template)
