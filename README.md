# kafka
Kafka cheatsheets

```
wget https://archive.apache.org/dist/kafka/2.7.0/kafka_2.13-2.7.0.tgz
tar -xzf kafka_2.13-2.7.0.tgz
cd kafka_2.13-2.7.0

./bin/zookeeper-server-start.sh -daemon config/zookeeper.properties

./bin/kafka-server-start.sh -daemon config/server.properties

# Создание топика
./bin/kafka-topics.sh --create --topic registrations --bootstrap-server localhost:9092

# Информация о топике
./bin/kafka-topics.sh --describe --topic registrations --bootstrap-server localhost:9092

# Запись в топик из консоли
./bin/kafka-console-producer.sh --topic registrations --bootstrap-server localhost:9092

# Чтение
./bin/kafka-console-consumer.sh --topic registrations --bootstrap-server localhost:9092
# Чтение с самого начала, до того как запустили консольный консьюмер
./bin/kafka-console-consumer.sh --topic registrations --bootstrap-server localhost:9092 --consumer-property auto.offset.reset=earliest
# Чтение с определением группа
./bin/kafka-console-consumer.sh --topic registrations --bootstrap-server localhost:9092 --consumer-property auto.offset.reset=earliest --group bgelov
# Описание группы
./bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group bgelov --describe
# Сброс на начало
./bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group bgelov --to-earliest --reset-offsets --execute --topic registrations
# Чтение с отключением автокоммита
./bin/kafka-console-consumer.sh --topic registrations --bootstrap-server localhost:9092 --group bgelov --consumer-property auto.offset.reset=earliest --consumer-property enable.auto.commit=false


# Проверка retentions
./bin/kafka-topics.sh --describe --topic registrations --bootstrap-server localhost:9092

```


# Конфигурация
https://kafka.apache.org/documentation/#configuration
```
vi config/server.properties

log.retention.check.interval.ms=1000

# Удаление сообщений через минуту
# retention.ms=60000
./bin/kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name registrations --alter --add-config retention.ms=60000
```

segment.ms=10000


# Zookeeper
```
./bin/zookeeper-shell.sh localhost:2181

ls /
get /controller
get /brokers/topics/registrations/partitions/0/state
stat /brokers/ids/0
```
