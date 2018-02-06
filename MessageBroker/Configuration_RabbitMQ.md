
# Configuration RabbitMQ 
> A curated list of awesome READMEs

Rabbit MQ Setting

```
echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list
wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install rabbitmq-server
rabbitmq-plugins enable rabbitmq_management
rabbitmq-plugins enable rabbitmq_mqtt
rabbitmqctl add_user svmchub 1qaz2wsx
rabbitmqctl set_user_tags svmchub administrator
rabbitmqctl set_permissions -p / svmchub ".*" ".*" ".*"
```
