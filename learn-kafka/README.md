## Kafka

### install binary
 - download [binary v2.12](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.5.0/kafka_2.12-2.5.0.tgz)
> tar xvf kafka_2.12-2.5.0.tgz

> vim ~/.bashrc
- append to the bottom
```bash
export PATH="$PATH:/var/local/software/kafka/kafka_2.12-2.5.0/bin"
```
[Official documentation](https://kafka.apache.org/quickstart)

### Test if Kafka works 
> kafka-topics.sh

### Start server
```bash
cd /var/local/software/kafka/kafka_2.12-2.5.0
```
> kafka-server-start.sh config/server.properties
>
