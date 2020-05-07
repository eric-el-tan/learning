# Maven

#problem
Caused by: org.apache.logging.log4j.LoggingException: log4j-slf4j-impl cannot be present with log4j-to-slf4j

[solution](https://www.baeldung.com/slf4j-classpath-multiple-bindings)

> mvn dependency:tree
```
[INFO] com.eric:login-svc:jar:0.1
[INFO] +- org.springframework.boot:spring-boot-starter-log4j2:jar:2.2.6.RELEASE:compile
[INFO] |  +- org.apache.logging.log4j:log4j-slf4j-impl:jar:2.12.1:compile
[INFO] |  |  \- org.apache.logging.log4j:log4j-api:jar:2.12.1:compile
[INFO] |  +- org.apache.logging.log4j:log4j-core:jar:2.12.1:compile
[INFO] |  +- org.apache.logging.log4j:log4j-jul:jar:2.12.1:compile
[INFO] |  \- org.slf4j:jul-to-slf4j:jar:1.7.30:compile
[INFO] +- org.springframework.boot:spring-boot-starter-data-jpa:jar:2.2.6.RELEASE:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter-aop:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- org.springframework:spring-aop:jar:5.2.5.RELEASE:compile
[INFO] |  |  \- org.aspectj:aspectjweaver:jar:1.9.5:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter-jdbc:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- com.zaxxer:HikariCP:jar:3.4.2:compile
[INFO] |  |  \- org.springframework:spring-jdbc:jar:5.2.5.RELEASE:compile
[INFO] |  +- jakarta.activation:jakarta.activation-api:jar:1.2.2:compile
[INFO] |  +- jakarta.persistence:jakarta.persistence-api:jar:2.2.3:compile
[INFO] |  +- jakarta.transaction:jakarta.transaction-api:jar:1.3.3:compile
[INFO] |  +- org.springframework.data:spring-data-jpa:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- org.springframework.data:spring-data-commons:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- org.springframework:spring-orm:jar:5.2.5.RELEASE:compile
[INFO] |  |  +- org.springframework:spring-context:jar:5.2.5.RELEASE:compile
[INFO] |  |  +- org.springframework:spring-tx:jar:5.2.5.RELEASE:compile
[INFO] |  |  \- org.springframework:spring-beans:jar:5.2.5.RELEASE:compile
[INFO] |  \- org.springframework:spring-aspects:jar:5.2.5.RELEASE:compile
[INFO] +- org.springframework.boot:spring-boot-starter-web:jar:2.2.6.RELEASE:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- org.springframework.boot:spring-boot-starter-logging:jar:2.2.6.RELEASE:compile
[INFO] |  |  |  +- ch.qos.logback:logback-classic:jar:1.2.3:compile
[INFO] |  |  |  |  \- ch.qos.logback:logback-core:jar:1.2.3:compile
[INFO] |  |  |  \- org.apache.logging.log4j:log4j-to-slf4j:jar:2.12.1:compile
[INFO] |  |  +- jakarta.annotation:jakarta.annotation-api:jar:1.3.5:compile
[INFO] |  |  \- org.yaml:snakeyaml:jar:1.25:runtime
[INFO] |  +- org.springframework.boot:spring-boot-starter-json:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- com.fasterxml.jackson.datatype:jackson-datatype-jdk8:jar:2.10.3:compile
[INFO] |  |  +- com.fasterxml.jackson.datatype:jackson-datatype-jsr310:jar:2.10.3:compile
[INFO] |  |  \- com.fasterxml.jackson.module:jackson-module-parameter-names:jar:2.10.3:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter-tomcat:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- org.apache.tomcat.embed:tomcat-embed-core:jar:9.0.33:compile
[INFO] |  |  +- org.apache.tomcat.embed:tomcat-embed-el:jar:9.0.33:compile
[INFO] |  |  \- org.apache.tomcat.embed:tomcat-embed-websocket:jar:9.0.33:compile
[INFO] |  +- org.springframework.boot:spring-boot-starter-validation:jar:2.2.6.RELEASE:compile
[INFO] |  |  +- jakarta.validation:jakarta.validation-api:jar:2.0.2:compile
[INFO] |  |  \- org.hibernate.validator:hibernate-validator:jar:6.0.18.Final:compile
[INFO] |  +- org.springframework:spring-web:jar:5.2.5.RELEASE:compile
[INFO] |  \- org.springframework:spring-webmvc:jar:5.2.5.RELEASE:compile
[INFO] |     \- org.springframework:spring-expression:jar:5.2.5.RELEASE:compile
[INFO] +- org.springframework.boot:spring-boot-devtools:jar:2.2.6.RELEASE:runtime (optional) 
[INFO] |  +- org.springframework.boot:spring-boot:jar:2.2.6.RELEASE:compile
[INFO] |  \- org.springframework.boot:spring-boot-autoconfigure:jar:2.2.6.RELEASE:compile
[INFO] +- com.h2database:h2:jar:1.4.200:runtime
[INFO] +- org.springframework.boot:spring-boot-starter-test:jar:2.2.6.RELEASE:test
[INFO] |  +- org.springframework.boot:spring-boot-test:jar:2.2.6.RELEASE:test
[INFO] |  +- org.springframework.boot:spring-boot-test-autoconfigure:jar:2.2.6.RELEASE:test
[INFO] |  +- com.jayway.jsonpath:json-path:jar:2.4.0:test
[INFO] |  +- jakarta.xml.bind:jakarta.xml.bind-api:jar:2.3.3:test
[INFO] |  +- org.junit.jupiter:junit-jupiter:jar:5.5.2:test
[INFO] |  |  +- org.junit.jupiter:junit-jupiter-api:jar:5.5.2:test
[INFO] |  |  |  +- org.apiguardian:apiguardian-api:jar:1.1.0:test
[INFO] |  |  |  +- org.opentest4j:opentest4j:jar:1.2.0:test
[INFO] |  |  |  \- org.junit.platform:junit-platform-commons:jar:1.5.2:test
[INFO] |  |  +- org.junit.jupiter:junit-jupiter-params:jar:5.5.2:test
[INFO] |  |  \- org.junit.jupiter:junit-jupiter-engine:jar:5.5.2:test
[INFO] |  |     \- org.junit.platform:junit-platform-engine:jar:1.5.2:test
[INFO] |  +- org.mockito:mockito-junit-jupiter:jar:3.1.0:test
[INFO] |  +- org.assertj:assertj-core:jar:3.13.2:test
[INFO] |  +- org.hamcrest:hamcrest:jar:2.1:test
[INFO] |  +- org.mockito:mockito-core:jar:3.1.0:test
[INFO] |  |  +- net.bytebuddy:byte-buddy:jar:1.10.8:compile
[INFO] |  |  +- net.bytebuddy:byte-buddy-agent:jar:1.10.8:test
[INFO] |  |  \- org.objenesis:objenesis:jar:2.6:test
[INFO] |  +- org.skyscreamer:jsonassert:jar:1.5.0:test
[INFO] |  +- org.springframework:spring-core:jar:5.2.5.RELEASE:compile
[INFO] |  |  \- org.springframework:spring-jcl:jar:5.2.5.RELEASE:compile
[INFO] |  +- org.springframework:spring-test:jar:5.2.5.RELEASE:test
[INFO] |  \- org.xmlunit:xmlunit-core:jar:2.6.4:test
[INFO] +- io.jsonwebtoken:jjwt-api:jar:0.10.5:compile
[INFO] +- io.jsonwebtoken:jjwt-impl:jar:0.10.5:runtime
[INFO] +- io.jsonwebtoken:jjwt-jackson:jar:0.10.5:runtime
[INFO] |  \- com.fasterxml.jackson.core:jackson-databind:jar:2.10.3:compile
[INFO] |     +- com.fasterxml.jackson.core:jackson-annotations:jar:2.10.3:compile
[INFO] |     \- com.fasterxml.jackson.core:jackson-core:jar:2.10.3:compile
[INFO] +- io.springfox:springfox-swagger2:jar:2.8.0:compile
[INFO] |  +- io.swagger:swagger-annotations:jar:1.5.14:compile
[INFO] |  +- io.swagger:swagger-models:jar:1.5.14:compile
[INFO] |  +- io.springfox:springfox-spi:jar:2.8.0:compile
[INFO] |  |  \- io.springfox:springfox-core:jar:2.8.0:compile
[INFO] |  +- io.springfox:springfox-schema:jar:2.8.0:compile
[INFO] |  +- io.springfox:springfox-swagger-common:jar:2.8.0:compile
[INFO] |  +- io.springfox:springfox-spring-web:jar:2.8.0:compile
[INFO] |  |  \- org.reflections:reflections:jar:0.9.11:compile
[INFO] |  +- com.google.guava:guava:jar:20.0:compile
[INFO] |  +- com.fasterxml:classmate:jar:1.5.1:compile
[INFO] |  +- org.slf4j:slf4j-api:jar:1.7.30:compile
[INFO] |  +- org.springframework.plugin:spring-plugin-core:jar:1.2.0.RELEASE:compile
[INFO] |  +- org.springframework.plugin:spring-plugin-metadata:jar:1.2.0.RELEASE:compile
[INFO] |  \- org.mapstruct:mapstruct:jar:1.2.0.Final:compile
[INFO] +- io.springfox:springfox-swagger-ui:jar:2.8.0:compile
[INFO] +- javax.validation:validation-api:jar:2.0.1.Final:compile
[INFO] +- javax.persistence:javax.persistence-api:jar:2.2:compile
[INFO] \- org.hibernate:hibernate-core:jar:5.2.3.Final:compile
[INFO]    +- org.jboss.logging:jboss-logging:jar:3.4.1.Final:compile
[INFO]    +- org.hibernate.javax.persistence:hibernate-jpa-2.1-api:jar:1.0.0.Final:compile
[INFO]    +- org.javassist:javassist:jar:3.20.0-GA:compile
[INFO]    +- antlr:antlr:jar:2.7.7:compile
[INFO]    +- org.apache.geronimo.specs:geronimo-jta_1.1_spec:jar:1.1.1:compile
[INFO]    +- org.jboss:jandex:jar:2.0.0.Final:compile
[INFO]    +- dom4j:dom4j:jar:1.6.1:compile
[INFO]    +- org.hibernate.common:hibernate-commons-annotations:jar:5.0.1.Final:compile
[INFO]    \- javax.enterprise:cdi-api:jar:1.1:compile
[INFO]       +- javax.el:el-api:jar:2.2:compile
[INFO]       +- org.jboss.spec.javax.interceptor:jboss-interceptors-api_1.1_spec:jar:1.0.0.Beta1:compile
[INFO]       +- javax.annotation:jsr250-api:jar:1.0:compile
[INFO]       \- javax.inject:javax.inject:jar:1:compile

```