# SonarQube

See how well other do on [SonarCloud](https://sonarcloud.io/explore/projects?languages=java&sort=-analysis_date)

## Install via Docker

- [Release 7.9 LTS Upgrade Notes](https://docs.sonarqube.org/latest/setup/upgrade-notes): The SonarQube server now requires Java 11. Analyses may continue to use Java 8 if necessary.
```
WrapperSimpleApp: Encountered an error running main: java.lang.IllegalStateException: SonarQube requires Java 11 to run
java.lang.IllegalStateException: SonarQube requires Java 11 to run
	at com.google.common.base.Preconditions.checkState(Preconditions.java:508)
```

- [started SonarQube in 2 mins](https://docs.sonarqube.org/latest/setup/get-started-2-minutes), [DockerHub](https://hub.docker.com/_/sonarqube?tab=tags)
> docker pull sonarqube
```
Using default tag: latest
latest: Pulling from library/sonarqube
cbdbe7a5bc2a: Pull complete 
02126857e210: Pull complete 
b35a2496a4dd: Pull complete 
3416b2d4ddcd: Pull complete 
a10cefb8b455: Pull complete 
Digest: sha256:f104e353d89542b69cf1e8d7ff7ccf93ed785397d3cee3168e66997f07bd869e
Status: Downloaded newer image for sonarqube:latest
docker.io/library/sonarqube:latest
```
> docker images
```
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
android/login-svc           latest              9c3f6224a11e        11 hours ago        688MB
sonarqube                   latest              d05d6af6a6b7        7 days ago          457MB

```
- start server
> docker run -d --name sonarqube -p 9000:9000 sonarqube:latest
```
eceef9b99ce38818e51a6bc319d7d1189c991d4ab9821c1a0e7e4aec0880ad67
```
> docker container ls -a
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
eceef9b99ce3        sonarqube:latest    "bin/run.sh bin/sona…"   16 minutes ago      Up 15 minutes       0.0.0.0:9000->9000/tcp   sonarqube
d5ff8d9795dc        android/login-svc   "java -jar login-svc…"   11 hours ago        Up 11 hours         0.0.0.0:8080->8080/tcp   login-svc
```


> docker logs --tail 1000 sonarqube
```
2020.05.16 14:49:29 INFO  app[][o.s.a.AppFileSystem] Cleaning or creating temp directory /opt/sonarqube/temp
2020.05.16 14:49:29 INFO  app[][o.s.a.es.EsSettings] Elasticsearch listening on /127.0.0.1:9001
2020.05.16 14:49:30 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='es', ipcIndex=1, logFilenamePrefix=es]] from [/opt/sonarqube/elasticsearch]: /opt/sonarqube/elasticsearch/bin/elasticsearch
2020.05.16 14:49:30 INFO  app[][o.s.a.SchedulerImpl] Waiting for Elasticsearch to be up and running
2020.05.16 14:49:30 INFO  app[][o.e.p.PluginsService] no modules loaded
2020.05.16 14:49:30 INFO  app[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.transport.Netty4Plugin]
OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
2020.05.16 14:49:43 INFO  es[][o.e.e.NodeEnvironment] using [1] data paths, mounts [[/ (overlay)]], net usable_space [64gb], net total_space [195.8gb], types [overlay]
2020.05.16 14:49:43 INFO  es[][o.e.e.NodeEnvironment] heap size [494.9mb], compressed ordinary object pointers [true]
2020.05.16 14:49:43 INFO  es[][o.e.n.Node] node name [sonarqube], node ID [ITgXpcQQSdi-G7mbD3ByTw]
2020.05.16 14:49:43 INFO  es[][o.e.n.Node] version[6.8.4], pid[36], build[default/tar/bca0c8d/2019-10-16T06:19:49.319352Z], OS[Linux/5.0.0-23-generic/amd64], JVM[AdoptOpenJDK/OpenJDK 64-Bit Server VM/11.0.6/11.0.6+10]
2020.05.16 14:49:43 INFO  es[][o.e.n.Node] JVM arguments [-XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -Des.networkaddress.cache.ttl=60, -Des.networkaddress.cache.negative.ttl=10, -XX:+AlwaysPreTouch, -Xss1m, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djna.nosys=true, -XX:-OmitStackTraceInFastThrow, -Dio.netty.noUnsafe=true, -Dio.netty.noKeySetOptimization=true, -Dio.netty.recycler.maxCapacityPerThread=0, -Dlog4j.shutdownHookEnabled=false, -Dlog4j2.disable.jmx=true, -Djava.io.tmpdir=/opt/sonarqube/temp, -XX:ErrorFile=../logs/es_hs_err_pid%p.log, -Xmx512m, -Xms512m, -XX:+HeapDumpOnOutOfMemoryError, -Des.path.home=/opt/sonarqube/elasticsearch, -Des.path.conf=/opt/sonarqube/temp/conf/es, -Des.distribution.flavor=default, -Des.distribution.type=tar]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [analysis-common]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [lang-painless]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [mapper-extras]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [parent-join]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [percolator]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [reindex]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [repository-url]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] loaded module [transport-netty4]
2020.05.16 14:49:44 INFO  es[][o.e.p.PluginsService] no plugins loaded
2020.05.16 14:49:47 WARN  es[][o.e.d.c.s.Settings] [http.enabled] setting was deprecated in Elasticsearch and will be removed in a future release! See the breaking changes documentation for the next major version.
2020.05.16 14:49:49 INFO  es[][o.e.d.DiscoveryModule] using discovery type [zen] and host providers [settings]
2020.05.16 14:49:50 INFO  es[][o.e.n.Node] initialized
2020.05.16 14:49:50 INFO  es[][o.e.n.Node] starting ...
2020.05.16 14:49:50 INFO  es[][o.e.t.TransportService] publish_address {127.0.0.1:9001}, bound_addresses {127.0.0.1:9001}
2020.05.16 14:49:50 WARN  es[][o.e.b.BootstrapChecks] max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
2020.05.16 14:49:53 INFO  es[][o.e.c.s.MasterService] zen-disco-elected-as-master ([0] nodes joined), reason: new_master {sonarqube}{ITgXpcQQSdi-G7mbD3ByTw}{38sUEsGQR8iwJohkpEwoWQ}{127.0.0.1}{127.0.0.1:9001}{rack_id=sonarqube}
2020.05.16 14:49:53 INFO  es[][o.e.c.s.ClusterApplierService] new_master {sonarqube}{ITgXpcQQSdi-G7mbD3ByTw}{38sUEsGQR8iwJohkpEwoWQ}{127.0.0.1}{127.0.0.1:9001}{rack_id=sonarqube}, reason: apply cluster state (from master [master {sonarqube}{ITgXpcQQSdi-G7mbD3ByTw}{38sUEsGQR8iwJohkpEwoWQ}{127.0.0.1}{127.0.0.1:9001}{rack_id=sonarqube} committed version [1] source [zen-disco-elected-as-master ([0] nodes joined)]])
2020.05.16 14:49:53 INFO  es[][o.e.n.Node] started
2020.05.16 14:49:53 INFO  es[][o.e.g.GatewayService] recovered [0] indices into cluster_state
2020.05.16 14:50:00 INFO  app[][o.s.a.SchedulerImpl] Process[es] is up
2020.05.16 14:50:00 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='web', ipcIndex=2, logFilenamePrefix=web]] from [/opt/sonarqube]: /opt/java/openjdk/bin/java -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djava.io.tmpdir=/opt/sonarqube/temp -XX:-OmitStackTraceInFastThrow --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED -Xmx512m -Xms128m -XX:+HeapDumpOnOutOfMemoryError -Dhttp.nonProxyHosts=localhost|127.*|[::1] -cp ./lib/common/*:/opt/sonarqube/lib/jdbc/h2/h2-1.4.199.jar org.sonar.server.app.WebServer /opt/sonarqube/temp/sq-process15900636389806209833properties
2020.05.16 14:50:05 INFO  web[][o.s.p.ProcessEntryPoint] Starting web
2020.05.16 14:50:08 INFO  web[][o.a.t.u.n.NioSelectorPool] Using a shared selector for servlet write/read
2020.05.16 14:50:09 INFO  web[][o.e.p.PluginsService] no modules loaded
2020.05.16 14:50:10 INFO  web[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.join.ParentJoinPlugin]
2020.05.16 14:50:10 INFO  web[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.percolator.PercolatorPlugin]
2020.05.16 14:50:10 INFO  web[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.transport.Netty4Plugin]
2020.05.16 14:50:12 INFO  web[][o.s.s.e.EsClientProvider] Connected to local Elasticsearch: [127.0.0.1:9001]
2020.05.16 14:50:12 INFO  web[][o.s.s.p.LogServerVersion] SonarQube Server / 8.3.1.34397 / 054c18b025be038b6343115894bf3ade0508f1e9
2020.05.16 14:50:13 INFO  web[][o.s.s.p.d.EmbeddedDatabase] Starting embedded database on port 9092 with url jdbc:h2:tcp://127.0.0.1:9092/sonar
2020.05.16 14:50:13 INFO  web[][o.s.s.p.d.EmbeddedDatabase] Embedded database started. Data stored in: /opt/sonarqube/data
2020.05.16 14:50:13 INFO  web[][o.sonar.db.Database] Create JDBC data source for jdbc:h2:tcp://127.0.0.1:9092/sonar
2020.05.16 14:50:13 WARN  web[][o.s.db.dialect.H2] H2 database should be used for evaluation purpose only.
2020.05.16 14:50:14 INFO  web[][o.s.s.p.ServerFileSystemImpl] SonarQube home: /opt/sonarqube
2020.05.16 14:50:14 INFO  web[][o.s.s.u.SystemPasscodeImpl] System authentication by passcode is disabled
2020.05.16 14:50:15 INFO  web[][o.s.s.p.d.m.h.MigrationHistoryTableImpl] Creating table schema_migrations
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin C# Code Quality and Security / 8.6.1.17183 / e9f4299031df68d8c4be6ba670fd4c0395eebf76
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin Git / 1.11.1.2008 / 204dc9b2cc33ec6b780303f926234eed26aea67d
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin JaCoCo / 1.1.0.898 / f65b288e6c2888393bd7fb72ad7ac1425f88eebf
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin Java Code Quality and Security / 6.3.0.21585 / ecf8f9f571691771e6789b8e59ff5e6b4ef36ad8
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarCSS / 1.2.0.1325 / 8dc9fe17b6230c20715d3b4cb34e0b6d02151afd
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarFlex / 2.5.1.1831 / a0c44437f6abb0feec76edd073f91fec64db2a6c
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarGo / 1.6.0.719 / edcc6a9e42fcdd30bb6f84a779c6cd7009ec72fd
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarHTML / 3.2.0.2082 / 997a51b39c4d0a5399c73a8fb729030a69eb392b
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarJS / 6.2.0.12043 / 8b9c1eb83d6ecfd2eda2cc3798e593900b6735fd
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarKotlin / 1.5.0.315 / 4ff3a145a58f3f84f1b39846a205a129d742e993
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarPHP / 3.3.0.5166 / 88e11dffb965aeef9d5bdd6d8413f394d35fecba
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarPython / 2.8.0.6204 / 5600d1ed780882d2362bedb3604dbad7ea63eb27
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarRuby / 1.5.0.315 / 4ff3a145a58f3f84f1b39846a205a129d742e993
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarScala / 1.5.0.315 / 4ff3a145a58f3f84f1b39846a205a129d742e993
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarTS / 2.1.0.4359 / 268ba9581b700c4fb2bc194d4069d283da915213
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin SonarXML / 2.0.1.2020 / c5b84004face582d56f110e24c29bf9c6a679e69
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin Svn / 1.9.0.1295 / 942e075773975354e32691a60bfd968065703e04
2020.05.16 14:50:15 INFO  web[][o.s.s.p.ServerPluginRepository] Deploy plugin VB.NET Code Quality and Security / 8.6.1.17183 / e9f4299031df68d8c4be6ba670fd4c0395eebf76
2020.05.16 14:50:16 INFO  web[][o.s.s.p.d.m.AutoDbMigration] Automatically perform DB migration on fresh install
2020.05.16 14:50:16 INFO  web[][DbMigrations] Executing DB migrations...
2020.05.16 14:50:16 INFO  web[][DbMigrations] #1 'Create initial schema'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #1 'Create initial schema': success | time=393ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #2 'Populate initial schema'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #2 'Populate initial schema': success | time=88ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3000 'Set Organizations#guarded column nullable'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3000 'Set Organizations#guarded column nullable': success | time=5ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3001 'Create ProjectQualityGates table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3001 'Create ProjectQualityGates table': success | time=14ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3002 'Make index on DEPRECATED_RULE_KEYS.RULE_ID non unique'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3002 'Make index on DEPRECATED_RULE_KEYS.RULE_ID non unique': success | time=14ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3003 'Populate ProjectQualityGate table from Properties table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3003 'Populate ProjectQualityGate table from Properties table': success | time=15ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3004 'Rename ANALYSIS_PROPERTIES.SNAPSHOT_UUID to ANALYSIS_UUID'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3004 'Rename ANALYSIS_PROPERTIES.SNAPSHOT_UUID to ANALYSIS_UUID': success | time=15ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3005 'Remove default quality gate property from Properties table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3005 'Remove default quality gate property from Properties table': success | time=7ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3006 'Create NEW_CODE_PERIOD table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3006 'Create NEW_CODE_PERIOD table': success | time=16ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3007 'Populate NEW_CODE_PERIOD table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3007 'Populate NEW_CODE_PERIOD table': success | time=13ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3008 'Remove leak period properties'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3008 'Remove leak period properties': success | time=7ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3009 'Remove GitHub login generation strategy property'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3009 'Remove GitHub login generation strategy property': success | time=7ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3100 'Create ALM_SETTINGS table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3100 'Create ALM_SETTINGS table': success | time=12ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3101 'Create PROJECT_ALM_SETTINGS table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3101 'Create PROJECT_ALM_SETTINGS table': success | time=19ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3102 'Migrate property 'sonar.alm.github.app.privateKey.secured' to 'sonar.alm.github.app.privateKeyContent.secured''...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3102 'Migrate property 'sonar.alm.github.app.privateKey.secured' to 'sonar.alm.github.app.privateKeyContent.secured'': success | time=30ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3103 'Migrate GitHub ALM settings from PROPERTIES to ALM_SETTINGS tables'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3103 'Migrate GitHub ALM settings from PROPERTIES to ALM_SETTINGS tables': success | time=42ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3104 'Migrate Bitbucket ALM settings from PROPERTIES to ALM_SETTINGS tables'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3104 'Migrate Bitbucket ALM settings from PROPERTIES to ALM_SETTINGS tables': success | time=25ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3105 'Migrate Azure ALM settings from PROPERTIES to ALM_SETTINGS tables'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3105 'Migrate Azure ALM settings from PROPERTIES to ALM_SETTINGS tables': success | time=11ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3106 'Delete 'sonar.pullrequest.provider' property'...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3106 'Delete 'sonar.pullrequest.provider' property': success | time=12ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3107 'Migrate default branches to keep global setting'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3107 'Migrate default branches to keep global setting': success | time=19ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3108 'Add EXCLUDE_FROM_PURGE column'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3108 'Add EXCLUDE_FROM_PURGE column': success | time=25ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3109 'Populate EXCLUDE_FROM_PURGE column'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3109 'Populate EXCLUDE_FROM_PURGE column': success | time=8ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3110 'Remove 'sonar.branch.longLivedBranches.regex''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3110 'Remove 'sonar.branch.longLivedBranches.regex'': success | time=9ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3111 'Rename 'sonar.dbcleaner.daysBeforeDeletingInactiveShortLivingBranches' setting'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3111 'Rename 'sonar.dbcleaner.daysBeforeDeletingInactiveShortLivingBranches' setting': success | time=6ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3112 'Migrate short and long living branches types to common BRANCH type'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3112 'Migrate short and long living branches types to common BRANCH type': success | time=7ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3113 'Migrate short and long living branches types to common BRANCH type in ce tasks table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3113 'Migrate short and long living branches types to common BRANCH type in ce tasks table': success | time=9ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3200 'Drop 'In Review' Security Hotspots status '...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3200 'Drop 'In Review' Security Hotspots status ': success | time=18ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3201 'Migrate Manual Vulnerabilities to Security Hotspots '...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3201 'Migrate Manual Vulnerabilities to Security Hotspots ': success | time=11ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3202 'Remove 'newsbox.dismiss.hotspots' user property'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3202 'Remove 'newsbox.dismiss.hotspots' user property': success | time=5ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3203 'Ensure Security Hotspots have status TO_REVIEW'...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3203 'Ensure Security Hotspots have status TO_REVIEW': success | time=15ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3204 'Rename table 'PROJECTS' to 'COMPONENTS''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3204 'Rename table 'PROJECTS' to 'COMPONENTS'': success | time=4ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3205 'Add PROJECTS table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3205 'Add PROJECTS table': success | time=12ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3206 'Populate PROJECTS table'...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 projects processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3206 'Populate PROJECTS table': success | time=13ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3207 'Drop 'TAGS' column from COMPONENTS table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3207 'Drop 'TAGS' column from COMPONENTS table': success | time=41ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3208 'Remove old Security Review Rating measures'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3208 'Remove old Security Review Rating measures': success | time=5ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3209 'Create ALM_PATS table'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3209 'Create ALM_PATS table': success | time=19ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3210 'Add index on ALM_slug'...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3210 'Add index on ALM_slug': success | time=9ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3211 'Delete conditions using 'security_hotspots' and 'new_security_hotspots' metrics'...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3211 'Delete conditions using 'security_hotspots' and 'new_security_hotspots' metrics': success | time=13ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3300 'Add 'summary_comment_enabled' boolean column to 'project_alm_settings''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3300 'Add 'summary_comment_enabled' boolean column to 'project_alm_settings'': success | time=28ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3301 'Enable 'summary_comment_enabled' for GitHub based projects'...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3301 'Enable 'summary_comment_enabled' for GitHub based projects': success | time=10ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3302 'Add 'component_uuid' column to 'properties''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3302 'Add 'component_uuid' column to 'properties'': success | time=12ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3303 'Migrate 'resource_id' to 'component_uuid' in 'properties''...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3303 'Migrate 'resource_id' to 'component_uuid' in 'properties'': success | time=16ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3304 'Remove column 'resource_id' in 'properties''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3304 'Remove column 'resource_id' in 'properties'': success | time=18ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3305 'Add 'component_uuid' column to 'group_roles''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3305 'Add 'component_uuid' column to 'group_roles'': success | time=16ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3306 'Migrate 'resource_id' to 'component_uuid' in 'group_roles''...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3306 'Migrate 'resource_id' to 'component_uuid' in 'group_roles'': success | time=11ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3307 'Remove column 'resource_id' in 'group_roles''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3307 'Remove column 'resource_id' in 'group_roles'': success | time=12ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3308 'Add 'component_uuid' column to 'user_roles''...
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3308 'Add 'component_uuid' column to 'user_roles'': success | time=13ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3309 'Migrate 'resource_id' to 'component_uuid' in 'user_roles''...
2020.05.16 14:50:17 INFO  web[][o.s.s.p.d.m.s.MassUpdate] 0 rows processed (0 items/sec)
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3309 'Migrate 'resource_id' to 'component_uuid' in 'user_roles'': success | time=9ms
2020.05.16 14:50:17 INFO  web[][DbMigrations] #3310 'Remove column 'resource_id' in 'user_roles''...
2020.05.16 14:50:18 INFO  web[][DbMigrations] #3310 'Remove column 'resource_id' in 'user_roles'': success | time=10ms
2020.05.16 14:50:18 INFO  web[][DbMigrations] #3311 'Remove column 'id' in 'components''...
2020.05.16 14:50:18 INFO  web[][DbMigrations] #3311 'Remove column 'id' in 'components'': success | time=36ms
2020.05.16 14:50:18 INFO  web[][DbMigrations] Executed DB migrations: success | time=1238ms
2020.05.16 14:50:18 INFO  web[][o.s.s.p.Platform] Database has been automatically updated
2020.05.16 14:50:18 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.platform.web.WebServiceFilter@12b694f9 [pattern=UrlPattern{inclusions=[/api/system/migrate_db.*, ...], exclusions=[/api/components/update_key, ...]}]
2020.05.16 14:50:18 INFO  web[][o.s.s.a.EmbeddedTomcat] HTTP connector enabled on port 9000
2020.05.16 14:50:19 INFO  web[][o.s.s.p.UpdateCenterClient] Update center: https://update.sonarsource.org/update-center.properties (no proxy)
2020.05.16 14:50:21 INFO  web[][o.s.s.e.IndexCreator] Create index [metadatas]
2020.05.16 14:50:21 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [metadatas] creating index, cause [api], templates [], shards [1]/[0], mappings []
2020.05.16 14:50:21 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[metadatas][0]] ...]).
2020.05.16 14:50:21 INFO  web[][o.s.s.e.IndexCreator] Create type metadatas/metadata
2020.05.16 14:50:21 INFO  es[][o.e.c.m.MetaDataMappingService] [metadatas/wSNZ16T6T6-SgtNuCl4BJg] create_mapping [metadata]
2020.05.16 14:50:22 INFO  web[][o.s.s.e.IndexCreator] Create index [components]
2020.05.16 14:50:22 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [components] creating index, cause [api], templates [], shards [5]/[0], mappings []
2020.05.16 14:50:22 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[components][4]] ...]).
2020.05.16 14:50:22 INFO  web[][o.s.s.e.IndexCreator] Create type components/auth
2020.05.16 14:50:22 INFO  es[][o.e.c.m.MetaDataMappingService] [components/0saypa3FTTmvGcWKholeTw] create_mapping [auth]
2020.05.16 14:50:22 INFO  web[][o.s.s.e.IndexCreator] Create index [projectmeasures]
2020.05.16 14:50:22 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [projectmeasures] creating index, cause [api], templates [], shards [5]/[0], mappings []
2020.05.16 14:50:23 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[projectmeasures][4]] ...]).
2020.05.16 14:50:23 INFO  web[][o.s.s.e.IndexCreator] Create type projectmeasures/auth
2020.05.16 14:50:23 INFO  es[][o.e.c.m.MetaDataMappingService] [projectmeasures/1cOBtKH2RjCVm17eorobsA] create_mapping [auth]
2020.05.16 14:50:23 INFO  web[][o.s.s.e.IndexCreator] Create index [rules]
2020.05.16 14:50:23 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [rules] creating index, cause [api], templates [], shards [2]/[0], mappings []
2020.05.16 14:50:24 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[rules][1]] ...]).
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create type rules/rule
2020.05.16 14:50:24 INFO  es[][o.e.c.m.MetaDataMappingService] [rules/rD54GtOxQweRSOFQhoRa7Q] create_mapping [rule]
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create index [issues]
2020.05.16 14:50:24 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [issues] creating index, cause [api], templates [], shards [5]/[0], mappings []
2020.05.16 14:50:24 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[issues][4]] ...]).
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create type issues/auth
2020.05.16 14:50:24 INFO  es[][o.e.c.m.MetaDataMappingService] [issues/ghIaeeGkTS26QEz8OUflrw] create_mapping [auth]
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create index [users]
2020.05.16 14:50:24 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [users] creating index, cause [api], templates [], shards [1]/[0], mappings []
2020.05.16 14:50:24 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[users][0]] ...]).
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create type users/user
2020.05.16 14:50:24 INFO  es[][o.e.c.m.MetaDataMappingService] [users/N80nS6WgQkWLRnu7u_lM-w] create_mapping [user]
2020.05.16 14:50:24 INFO  web[][o.s.s.e.IndexCreator] Create index [views]
2020.05.16 14:50:25 INFO  es[][o.e.c.m.MetaDataCreateIndexService] [views] creating index, cause [api], templates [], shards [5]/[0], mappings []
2020.05.16 14:50:25 INFO  es[][o.e.c.r.a.AllocationService] Cluster health status changed from [YELLOW] to [GREEN] (reason: [shards started [[views][4]] ...]).
2020.05.16 14:50:25 INFO  web[][o.s.s.e.IndexCreator] Create type views/view
2020.05.16 14:50:25 INFO  es[][o.e.c.m.MetaDataMappingService] [views/8z0lOIN7TzWiwTuFPjGvGA] create_mapping [view]
2020.05.16 14:50:25 INFO  web[][o.s.s.s.LogServerId] Server ID: BF41A1F2-AXId9uFML5Z3utAYfBhM
2020.05.16 14:50:25 WARN  web[][o.s.s.a.LogOAuthWarning] For security reasons, OAuth authentication should use HTTPS. You should set the property 'Administration > Configuration > Server base URL' to a HTTPS URL.
2020.05.16 14:50:25 WARN  web[][o.s.a.s.w.WebService$Action] The response example is not set on action api/plugins/download
2020.05.16 14:50:25 WARN  web[][o.s.a.s.w.WebService$Action] The response example is not set on action api/permissions/search_templates
2020.05.16 14:50:25 INFO  web[][o.s.s.t.TelemetryDaemon] Sharing of SonarQube statistics is enabled.
2020.05.16 14:50:25 INFO  web[][o.s.s.n.NotificationDaemon] Notification service started (delay 60 sec.)
2020.05.16 14:50:25 INFO  web[][o.s.s.s.GeneratePluginIndex] Generate scanner plugin index
2020.05.16 14:50:25 INFO  web[][o.s.s.s.RegisterPlugins] Register plugins
2020.05.16 14:50:25 INFO  web[][o.s.s.s.RegisterMetrics] Register metrics
2020.05.16 14:50:25 INFO  web[][o.s.s.q.RegisterQualityGates] Built-in quality gate's conditions of [Sonar way] has been updated
2020.05.16 14:50:25 INFO  web[][o.s.s.r.RegisterRules] Register rules
2020.05.16 14:50:39 WARN  web[][o.s.s.r.i.RuleIndexer] Rule java:S2647 with CWEs '311, 522' maps to multiple SQ Security Categories: auth, insecure-conf
2020.05.16 14:50:40 WARN  web[][o.s.s.r.i.RuleIndexer] Rule java:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:42 WARN  web[][o.s.s.r.i.RuleIndexer] Rule csharpsquid:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:42 WARN  web[][o.s.s.r.i.RuleIndexer] Rule typescript:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:42 WARN  web[][o.s.s.r.i.RuleIndexer] Rule typescript:S1523 with CWEs '95, 470' maps to multiple SQ Security Categories: rce, object-injection
2020.05.16 14:50:43 WARN  web[][o.s.s.r.i.RuleIndexer] Rule vbnet:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:44 WARN  web[][o.s.s.r.i.RuleIndexer] Rule python:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:45 WARN  web[][o.s.s.r.i.RuleIndexer] Rule javascript:S1523 with CWEs '95, 470' maps to multiple SQ Security Categories: rce, object-injection
2020.05.16 14:50:45 WARN  web[][o.s.s.r.i.RuleIndexer] Rule javascript:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:46 WARN  web[][o.s.s.r.i.RuleIndexer] Rule php:S4787 with CWEs '321, 322, 323, 324, 522, 325, 326, 327' maps to multiple SQ Security Categories: weak-cryptography, auth
2020.05.16 14:50:46 WARN  web[][o.s.s.r.i.RuleIndexer] Rule php:S1523 with CWEs '95, 470' maps to multiple SQ Security Categories: rce, object-injection
2020.05.16 14:50:50 INFO  web[][o.s.s.q.BuiltInQProfileRepositoryImpl] Load quality profiles
2020.05.16 14:50:52 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register quality profiles
2020.05.16 14:50:52 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile css/Sonar way
2020.05.16 14:50:53 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile scala/Sonar way
2020.05.16 14:50:53 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile jsp/Sonar way
2020.05.16 14:50:53 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile go/Sonar way
2020.05.16 14:50:54 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile kotlin/Sonar way
2020.05.16 14:50:54 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile js/Sonar way
2020.05.16 14:50:54 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile js/Sonar way Recommended
2020.05.16 14:50:54 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile py/Sonar way
2020.05.16 14:50:55 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile ruby/Sonar way
2020.05.16 14:50:55 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile cs/Sonar way
2020.05.16 14:50:55 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile java/Sonar way
2020.05.16 14:50:56 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile web/Sonar way
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile xml/Sonar way
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile flex/Sonar way
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile php/Sonar way
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile php/PSR-2
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile php/Drupal
2020.05.16 14:50:57 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile vbnet/Sonar way
2020.05.16 14:50:58 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile ts/Sonar way
2020.05.16 14:50:58 INFO  web[][o.s.s.q.RegisterQualityProfiles] Register profile ts/Sonar way recommended
2020.05.16 14:50:58 INFO  web[][o.s.s.s.RegisterPermissionTemplates] Register permission templates
2020.05.16 14:50:58 INFO  web[][o.s.s.s.RenameDeprecatedPropertyKeys] Rename deprecated property keys
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.platform.web.WebServiceFilter@4c7dd6d5 [pattern=UrlPattern{inclusions=[/api/issues/delete_comment.*, ...], exclusions=[/api/authentication/login.*, ...]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.platform.web.WebServiceReroutingFilter@286fbe74 [pattern=UrlPattern{inclusions=[/api/components/bulk_update_key, ...], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.authentication.InitFilter@4b7ba6fb [pattern=UrlPattern{inclusions=[/sessions/init/*], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.authentication.OAuth2CallbackFilter@530b7920 [pattern=UrlPattern{inclusions=[/oauth2/callback/*], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.authentication.ws.LoginAction@7f1b32a0 [pattern=UrlPattern{inclusions=[/api/authentication/login], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.authentication.ws.LogoutAction@66defea1 [pattern=UrlPattern{inclusions=[/api/authentication/logout], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.p.w.MasterServletFilter] Initializing servlet filter org.sonar.server.authentication.ws.ValidateAction@213e82e2 [pattern=UrlPattern{inclusions=[/api/authentication/validate], exclusions=[]}]
2020.05.16 14:50:58 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [users/user] ...
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [30s] to [-1]
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [30s] to [-1]
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [-1] to [30s]
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [-1] to [30s]
2020.05.16 14:50:58 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [users/user] done | time=272ms
2020.05.16 14:50:58 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [components/auth/component] ...
2020.05.16 14:50:58 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [components/auth/component] done | time=118ms
2020.05.16 14:50:58 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [views/view] ...
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [30s] to [-1]
2020.05.16 14:50:58 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [30s] to [-1]
2020.05.16 14:50:59 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [-1] to [30s]
2020.05.16 14:50:59 INFO  es[][o.e.c.s.IndexScopedSettings] updating [index.refresh_interval] from [-1] to [30s]
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [views/view] done | time=231ms
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [issues/auth/issue] ...
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [issues/auth/issue] done | time=119ms
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of types [components/auth],[projectmeasures/auth],[issues/auth] ...
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of types [components/auth],[projectmeasures/auth],[issues/auth] done | time=137ms
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [projectmeasures/auth/projectmeasure] ...
2020.05.16 14:50:59 INFO  web[][o.s.s.e.IndexerStartupTask] Indexing of type [projectmeasures/auth/projectmeasure] done | time=96ms
2020.05.16 14:50:59 INFO  web[][o.s.s.q.ProjectsInWarningDaemon] Counting number of projects in warning is enabled.
2020.05.16 14:50:59 INFO  web[][o.s.s.p.p.PlatformLevelStartup] Running Community Edition
2020.05.16 14:50:59 INFO  web[][o.s.s.p.Platform] WebServer is operational
2020.05.16 14:50:59 INFO  web[][o.s.s.q.ProjectsInWarningDaemon] Counting number of projects in warning will be disabled as there are no more projects in warning.
2020.05.16 14:50:59 INFO  app[][o.s.a.SchedulerImpl] Process[web] is up
2020.05.16 14:50:59 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='ce', ipcIndex=3, logFilenamePrefix=ce]] from [/opt/sonarqube]: /opt/java/openjdk/bin/java -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djava.io.tmpdir=/opt/sonarqube/temp -XX:-OmitStackTraceInFastThrow --add-opens=java.base/java.util=ALL-UNNAMED -Xmx512m -Xms128m -XX:+HeapDumpOnOutOfMemoryError -Dhttp.nonProxyHosts=localhost|127.*|[::1] -cp ./lib/common/*:/opt/sonarqube/lib/jdbc/h2/h2-1.4.199.jar org.sonar.ce.app.CeServer /opt/sonarqube/temp/sq-process13450214525994035837properties
2020.05.16 14:51:00 INFO  ce[][o.s.p.ProcessEntryPoint] Starting ce
2020.05.16 14:51:00 INFO  ce[][o.s.ce.app.CeServer] Compute Engine starting up...
2020.05.16 14:51:01 INFO  ce[][o.e.p.PluginsService] no modules loaded
2020.05.16 14:51:01 INFO  ce[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.join.ParentJoinPlugin]
2020.05.16 14:51:01 INFO  ce[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.percolator.PercolatorPlugin]
2020.05.16 14:51:01 INFO  ce[][o.e.p.PluginsService] loaded plugin [org.elasticsearch.transport.Netty4Plugin]
2020.05.16 14:51:04 INFO  ce[][o.s.s.e.EsClientProvider] Connected to local Elasticsearch: [127.0.0.1:9001]
2020.05.16 14:51:04 INFO  ce[][o.sonar.db.Database] Create JDBC data source for jdbc:h2:tcp://127.0.0.1:9092/sonar
2020.05.16 14:51:04 WARN  ce[][o.s.db.dialect.H2] H2 database should be used for evaluation purpose only.
2020.05.16 14:51:06 INFO  ce[][o.s.s.p.ServerFileSystemImpl] SonarQube home: /opt/sonarqube
2020.05.16 14:51:06 INFO  ce[][o.s.c.c.CePluginRepository] Load plugins
2020.05.16 14:51:08 INFO  ce[][o.s.c.c.ComputeEngineContainerImpl] Running Community edition
2020.05.16 14:51:08 INFO  ce[][o.s.ce.app.CeServer] Compute Engine is operational
2020.05.16 14:51:08 INFO  app[][o.s.a.SchedulerImpl] Process[ce] is up
2020.05.16 14:51:08 INFO  app[][o.s.a.SchedulerImpl] SonarQube is up
```


- SonarQube Portal
1. Log in to http://localhost:9000 with System Administrator credentials (login=admin, password=admin).
1. Click the Create new project button to analyze your first project.

## Add project to SonarQube

pom.xml add plugin
```
<plugin>
    <groupId>org.sonarsource.scanner.maven</groupId>
    <artifactId>sonar-maven-plugin</artifactId>
</plugin>
```

> mvn clean package

```
[INFO] Scanning for projects...
[WARNING] 
[WARNING] Some problems were encountered while building the effective model for com.foodstuff:demo:jar:0.0.1-SNAPSHOT
[WARNING] 'build.plugins.plugin.version' for org.sonarsource.scanner.maven:sonar-maven-plugin is missing. @ line 46, column 12
[WARNING] 
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING] 
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
[WARNING] 
[INFO] 
[INFO] -------------------------< com.foodstuff:demo >-------------------------
[INFO] Building demo 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The POM for com.jayway.jsonpath:json-path:jar:2.4.0 is invalid, transitive dependencies (if any) will not be available, enable debug logging for more details
[WARNING] The POM for org.skyscreamer:jsonassert:jar:1.5.0 is invalid, transitive dependencies (if any) will not be available, enable debug logging for more details
[INFO] 
[INFO] --- maven-clean-plugin:3.1.0:clean (default-clean) @ demo ---
[INFO] Deleting /var/local/git/foodstuff2/demo/target
[INFO] 
[INFO] --- maven-resources-plugin:3.1.0:resources (default-resources) @ demo ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 1 resource
[INFO] Copying 0 resource
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ demo ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 4 source files to /var/local/git/foodstuff2/demo/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:3.1.0:testResources (default-testResources) @ demo ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /var/local/git/foodstuff2/demo/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ demo ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 2 source files to /var/local/git/foodstuff2/demo/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.22.2:test (default-test) @ demo ---
[WARNING] The POM for junit:junit:jar:4.12 is invalid, transitive dependencies (if any) will not be available, enable debug logging for more details
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.foodstuff.demo.DemoApplicationTests
03:43:46.275 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating CacheAwareContextLoaderDelegate from class [org.springframework.test.context.cache.DefaultCacheAwareContextLoaderDelegate]
03:43:46.292 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating BootstrapContext using constructor [public org.springframework.test.context.support.DefaultBootstrapContext(java.lang.Class,org.springframework.test.context.CacheAwareContextLoaderDelegate)]
03:43:46.341 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating TestContextBootstrapper for test class [com.foodstuff.demo.DemoApplicationTests] from class [org.springframework.boot.test.context.SpringBootTestContextBootstrapper]
03:43:46.367 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Neither @ContextConfiguration nor @ContextHierarchy found for test class [com.foodstuff.demo.DemoApplicationTests], using SpringBootContextLoader
03:43:46.373 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.foodstuff.demo.DemoApplicationTests]: class path resource [com/foodstuff/demo/DemoApplicationTests-context.xml] does not exist
03:43:46.373 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.foodstuff.demo.DemoApplicationTests]: class path resource [com/foodstuff/demo/DemoApplicationTestsContext.groovy] does not exist
03:43:46.374 [main] INFO org.springframework.test.context.support.AbstractContextLoader - Could not detect default resource locations for test class [com.foodstuff.demo.DemoApplicationTests]: no resource found for suffixes {-context.xml, Context.groovy}.
03:43:46.375 [main] INFO org.springframework.test.context.support.AnnotationConfigContextLoaderUtils - Could not detect default configuration classes for test class [com.foodstuff.demo.DemoApplicationTests]: DemoApplicationTests does not declare any static, non-private, non-final, nested classes annotated with @Configuration.
03:43:46.431 [main] DEBUG org.springframework.test.context.support.ActiveProfilesUtils - Could not find an 'annotation declaring class' for annotation type [org.springframework.test.context.ActiveProfiles] and class [com.foodstuff.demo.DemoApplicationTests]
03:43:46.523 [main] DEBUG org.springframework.context.annotation.ClassPathScanningCandidateComponentProvider - Identified candidate component class: file [/var/local/git/foodstuff2/demo/target/classes/com/foodstuff/demo/DemoApplication.class]
03:43:46.524 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Found @SpringBootConfiguration com.foodstuff.demo.DemoApplication for test class com.foodstuff.demo.DemoApplicationTests
03:43:46.655 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - @TestExecutionListeners is not present for class [com.foodstuff.demo.DemoApplicationTests]: using defaults.
03:43:46.656 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Loaded default TestExecutionListener class names from location [META-INF/spring.factories]: [org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener, org.springframework.test.context.web.ServletTestExecutionListener, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener, org.springframework.test.context.support.DependencyInjectionTestExecutionListener, org.springframework.test.context.support.DirtiesContextTestExecutionListener, org.springframework.test.context.transaction.TransactionalTestExecutionListener, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener, org.springframework.test.context.event.EventPublishingTestExecutionListener]
03:43:46.667 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Skipping candidate TestExecutionListener [org.springframework.test.context.web.ServletTestExecutionListener] due to a missing dependency. Specify custom listener classes or make the default listener classes and their required dependencies available. Offending class: [javax/servlet/ServletContext]
03:43:46.669 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Skipping candidate TestExecutionListener [org.springframework.test.context.transaction.TransactionalTestExecutionListener] due to a missing dependency. Specify custom listener classes or make the default listener classes and their required dependencies available. Offending class: [org/springframework/transaction/TransactionDefinition]
03:43:46.670 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Skipping candidate TestExecutionListener [org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener] due to a missing dependency. Specify custom listener classes or make the default listener classes and their required dependencies available. Offending class: [org/springframework/transaction/interceptor/TransactionAttribute]
03:43:46.671 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Using TestExecutionListeners: [org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener@15aab8c6, org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener@33990a0c, org.springframework.boot.test.autoconfigure.SpringBootDependencyInjectionTestExecutionListener@4de4b452, org.springframework.test.context.support.DirtiesContextTestExecutionListener@50b5ac82, org.springframework.test.context.event.EventPublishingTestExecutionListener@101952da, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener@6babf3bf, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener@3059cbc, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener@7ea9e1e2, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener@24fcf36f, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener@10feca44]
03:43:46.676 [main] DEBUG org.springframework.test.context.support.AbstractDirtiesContextTestExecutionListener - Before test class: context [DefaultTestContext@3e84448c testClass = DemoApplicationTests, testInstance = [null], testMethod = [null], testException = [null], mergedContextConfiguration = [MergedContextConfiguration@4a7f959b testClass = DemoApplicationTests, locations = '{}', classes = '{class com.foodstuff.demo.DemoApplication}', contextInitializerClasses = '[]', activeProfiles = '{}', propertySourceLocations = '{}', propertySourceProperties = '{org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true}', contextCustomizers = set[org.springframework.boot.test.context.filter.ExcludeFilterContextCustomizer@147ed70f, org.springframework.boot.test.json.DuplicateJsonObjectContextCustomizerFactory$DuplicateJsonObjectContextCustomizer@15b204a1, org.springframework.boot.test.mock.mockito.MockitoContextCustomizer@0, org.springframework.boot.test.web.client.TestRestTemplateContextCustomizer@12b0404f, org.springframework.boot.test.autoconfigure.properties.PropertyMappingContextCustomizer@0, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverContextCustomizerFactory$Customizer@794cb805, org.springframework.boot.test.context.SpringBootTestArgs@1], contextLoader = 'org.springframework.boot.test.context.SpringBootContextLoader', parent = [null]], attributes = map[[empty]]], class annotated with @DirtiesContext [false] with mode [null].
03:43:46.692 [main] DEBUG org.springframework.test.context.support.DependencyInjectionTestExecutionListener - Performing dependency injection for test context [[DefaultTestContext@3e84448c testClass = DemoApplicationTests, testInstance = com.foodstuff.demo.DemoApplicationTests@1a18644, testMethod = [null], testException = [null], mergedContextConfiguration = [MergedContextConfiguration@4a7f959b testClass = DemoApplicationTests, locations = '{}', classes = '{class com.foodstuff.demo.DemoApplication}', contextInitializerClasses = '[]', activeProfiles = '{}', propertySourceLocations = '{}', propertySourceProperties = '{org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true}', contextCustomizers = set[org.springframework.boot.test.context.filter.ExcludeFilterContextCustomizer@147ed70f, org.springframework.boot.test.json.DuplicateJsonObjectContextCustomizerFactory$DuplicateJsonObjectContextCustomizer@15b204a1, org.springframework.boot.test.mock.mockito.MockitoContextCustomizer@0, org.springframework.boot.test.web.client.TestRestTemplateContextCustomizer@12b0404f, org.springframework.boot.test.autoconfigure.properties.PropertyMappingContextCustomizer@0, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverContextCustomizerFactory$Customizer@794cb805, org.springframework.boot.test.context.SpringBootTestArgs@1], contextLoader = 'org.springframework.boot.test.context.SpringBootContextLoader', parent = [null]], attributes = map[[empty]]]].
03:43:46.719 [main] DEBUG org.springframework.test.context.support.TestPropertySourceUtils - Adding inlined properties to environment: {spring.jmx.enabled=false, org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true, server.port=-1}

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.7.RELEASE)

2020-05-17 03:43:47.036  INFO 19121 --- [           main] com.foodstuff.demo.DemoApplicationTests  : Starting DemoApplicationTests on coding with PID 19121 (started by erictan in /var/local/git/foodstuff2/demo)
2020-05-17 03:43:47.038  INFO 19121 --- [           main] com.foodstuff.demo.DemoApplicationTests  : No active profile set, falling back to default profiles: default
2020-05-17 03:43:47.649  INFO 19121 --- [           main] com.foodstuff.demo.DemoApplicationTests  : Started DemoApplicationTests in 0.927 seconds (JVM running for 2.217)
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.744 s - in com.foodstuff.demo.DemoApplicationTests
[INFO] Running com.foodstuff.demo.repository.TestTimeslotRepository
Timeslot{day=2020-05-18, hour=1, shopper=[User{id=1}, User{id=2}, User{id=3}, User{id=4}, User{id=5}, User{id=6}, User{id=7}, User{id=8}]}
Timeslot{day=2020-05-19, hour=1, shopper=[User{id=1}]}
Timeslot{day=2020-05-20, hour=1, shopper=[User{id=1}]}
Timeslot{day=2020-05-21, hour=1, shopper=[User{id=1}]}
{0=0, 1=1, 2=2, 3=3, 4=2, 5=0, 6=0, 7=0, 8=0, 9=0, 10=0, 11=0, 12=0, 13=0, 14=0, 15=0, 16=0, 17=0, 18=0, 19=0, 20=0, 21=0, 22=0, 23=0}
[INFO] Tests run: 7, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.036 s - in com.foodstuff.demo.repository.TestTimeslotRepository
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 8, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] 
[INFO] --- maven-jar-plugin:3.1.2:jar (default-jar) @ demo ---
[INFO] Building jar: /var/local/git/foodstuff2/demo/target/demo-0.0.1-SNAPSHOT.jar
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.2.7.RELEASE:repackage (repackage) @ demo ---
[INFO] Replacing main artifact with repackaged archive
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  7.684 s
[INFO] Finished at: 2020-05-17T03:43:49+12:00
[INFO] ------------------------------------------------------------------------
```
> mvn sonar:sonar
```
[INFO] Scanning for projects...
[WARNING] 
[WARNING] Some problems were encountered while building the effective model for com.foodstuff:demo:jar:0.0.1-SNAPSHOT
[WARNING] 'build.plugins.plugin.version' for org.sonarsource.scanner.maven:sonar-maven-plugin is missing. @ line 46, column 12
[WARNING] 
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING] 
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
[WARNING] 
[INFO] 
[INFO] -------------------------< com.foodstuff:demo >-------------------------
[INFO] Building demo 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The POM for com.jayway.jsonpath:json-path:jar:2.4.0 is invalid, transitive dependencies (if any) will not be available, enable debug logging for more details
[WARNING] The POM for org.skyscreamer:jsonassert:jar:1.5.0 is invalid, transitive dependencies (if any) will not be available, enable debug logging for more details
[INFO] 
[INFO] --- sonar-maven-plugin:3.7.0.1746:sonar (default-cli) @ demo ---
[INFO] User cache: /home/erictan/.sonar/cache
[INFO] SonarQube version: 8.3.1
[INFO] Default locale: "en_HK", source code encoding: "UTF-8"
[WARNING] SonarScanner will require Java 11 to run starting in SonarQube 8.x
[INFO] Load global settings
[INFO] Load global settings (done) | time=158ms
[INFO] Server id: BF41A1F2-AXId9uFML5Z3utAYfBhM
[INFO] User cache: /home/erictan/.sonar/cache
[INFO] Load/download plugins
[INFO] Load plugins index
[INFO] Load plugins index (done) | time=90ms
[INFO] Load/download plugins (done) | time=144ms
[INFO] Process project properties
[INFO] Process project properties (done) | time=16ms
[INFO] Execute project builders
[INFO] Execute project builders (done) | time=5ms
[INFO] Project key: com.foodstuff:demo
[INFO] Base dir: /var/local/git/foodstuff2/demo
[INFO] Working dir: /var/local/git/foodstuff2/demo/target/sonar
[INFO] Load project settings for component key: 'com.foodstuff:demo'
[INFO] Load project settings for component key: 'com.foodstuff:demo' (done) | time=77ms
[INFO] Load quality profiles
[INFO] Load quality profiles (done) | time=128ms
[INFO] Load active rules
[INFO] Load active rules (done) | time=2797ms
[INFO] Indexing files...
[INFO] Project configuration:
[INFO] 7 files indexed
[INFO] 0 files ignored because of scm ignore settings
[INFO] Quality profile for java: Sonar way
[INFO] Quality profile for xml: Sonar way
[INFO] ------------- Run sensors on module demo
[INFO] Load metrics repository
[INFO] Load metrics repository (done) | time=48ms
[INFO] Sensor JavaSquidSensor [java]
[INFO] Configured Java source version (sonar.java.source): 8
[INFO] JavaClasspath initialization
[INFO] JavaClasspath initialization (done) | time=16ms
[INFO] JavaTestClasspath initialization
[INFO] JavaTestClasspath initialization (done) | time=3ms
[INFO] Java Main Files AST scan
[INFO] 4 source files to be analyzed
[INFO] Load project repositories
[INFO] Load project repositories (done) | time=37ms
[INFO] 4/4 source files have been analyzed
[INFO] Java Main Files AST scan (done) | time=2400ms
[INFO] Java Test Files AST scan
[INFO] 2 source files to be analyzed
[INFO] Java Test Files AST scan (done) | time=266ms
[INFO] 2/2 source files have been analyzed
[INFO] Java Generated Files AST scan
[INFO] 0 source files to be analyzed
[INFO] Java Generated Files AST scan (done) | time=1ms
[INFO] Sensor JavaSquidSensor [java] (done) | time=2951ms
[INFO] 0/0 source files have been analyzed
[INFO] Sensor SonarCSS Rules [cssfamily]
[INFO] No CSS, PHP, HTML or VueJS files are found in the project. CSS analysis is skipped.
[INFO] Sensor SonarCSS Rules [cssfamily] (done) | time=3ms
[INFO] Sensor JaCoCo XML Report Importer [jacoco]
[INFO] 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
[INFO] No report imported, no coverage information will be imported by JaCoCo XML Report Importer
[INFO] Sensor JaCoCo XML Report Importer [jacoco] (done) | time=5ms
[INFO] Sensor SurefireSensor [java]
[INFO] parsing [/var/local/git/foodstuff2/demo/target/surefire-reports]
[INFO] Sensor SurefireSensor [java] (done) | time=55ms
[INFO] Sensor JavaXmlSensor [java]
[INFO] 1 source files to be analyzed
[INFO] Sensor JavaXmlSensor [java] (done) | time=353ms
[INFO] 1/1 source files have been analyzed
[INFO] Sensor HTML [web]
[INFO] Sensor HTML [web] (done) | time=5ms
[INFO] Sensor XML Sensor [xml]
[INFO] 1 source files to be analyzed
[INFO] Sensor XML Sensor [xml] (done) | time=201ms
[INFO] 1/1 source files have been analyzed
[INFO] ------------- Run sensors on project
[INFO] Sensor Zero Coverage Sensor
[INFO] Sensor Zero Coverage Sensor (done) | time=20ms
[INFO] Sensor Java CPD Block Indexer
[INFO] Sensor Java CPD Block Indexer (done) | time=42ms
[INFO] SCM Publisher SCM provider for this project is: git
[INFO] SCM Publisher 1 source file to be analyzed
[INFO] SCM Publisher 0/1 source files have been analyzed (done) | time=166ms
[WARNING] Missing blame information for the following files:
[WARNING]   * pom.xml
[WARNING] This may lead to missing/broken features in SonarQube
[INFO] CPD Executor 1 file had no CPD blocks
[INFO] CPD Executor Calculating CPD for 3 files
[INFO] CPD Executor CPD calculation finished (done) | time=13ms
[INFO] Analysis report generated in 158ms, dir size=106 KB
[INFO] Analysis report compressed in 65ms, zip size=25 KB
[INFO] Analysis report uploaded in 70ms
[INFO] ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard?id=com.foodstuff%3Ademo
[INFO] Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
[INFO] More about the report processing at http://localhost:9000/api/ce/task?id=AXIeKKOsL5Z3utAYfD_E
[INFO] Analysis total time: 12.377 s
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  15.886 s
[INFO] Finished at: 2020-05-17T03:44:39+12:00
[INFO] ------------------------------------------------------------------------
```

## configure

- [SonarScanner for Maven](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-maven)

```
<plugin>
	<groupId>org.sonarsource.scanner.maven</groupId>
	<artifactId>sonar-maven-plugin</artifactId>
</plugin>
```
			
## add Jacoco Test Coverage

```
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <!--<version>0.7.7.201606060606</version>-->
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>CodeOps
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
        <execution>
            <id>jacoco-check</id>
            <goals>
                <goal>check</goal>
            </goals>
            <configuration>
                <rules>
                    <rule>
                        <limits>
                            <limit>
                                <minimum>0.9</minimum>
                            </limit>
                        </limits>
                    </rule>
                </rules>
            </configuration>
        </execution>
    </executions>
</plugin>
```
- as suggested by [Samuel Addico
](https://medium.com/codeops/code-coverage-with-jacoco-sonarqube-and-maven-59fb04a9a383)
> mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install
>
> cd target/
>
> ls -l jacoco.exec

