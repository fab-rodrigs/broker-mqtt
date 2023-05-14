# broker-mqtt

Este é um projeto voltado para a criação de um broker MQTT virtual.

MQTT (Message Queuing Telemetry Transport) é um protocolo de comunicação simples para dispositivos IoT. Se baseia em uma separação por tópicos, no qual cada dispositivo inscrito em um determinado tópico receberá as mensagens enviadas para aquele tópico. Um broker MQTT seria o caminho entre as mensagens recebidas e os dispositivos inscritos em seus respectivos tópicos.

Podemos testar a comunicação MQTT entre dois terminais. Para realizar essa comunicação no Linux primeiro deve-se instalar o Mosquitto, que é o servidor broker, e o Mosquitto Clients, que são os clientes para realizar a interface com o broker do próprio dispositivo.
```
sudo apt install mosquitto mosquitto-clients
```
Para melhorar a segurança em sistemas maiores, pode-se realizar criação de um usuário e senha para acesso ao broker: 
```
sudo mosquitto_passwd -c /etc/mosquitto/passwd (usuario)
```
Para a utilização desse login, pode-se criar um arquivo de configuração:
```
sudo vim /etc/mosquitto/conf.d/default.conf
```
Esse arquivo deve possuir os seguintes comandos:
```
allow_anonymous false                 // impossibilita o acesso anônimo
password file /etc/mosquitto/passwd   // localiza o arquivo onde a senha foi armazenada
```
Após esse processo, deve-se reiniciar o Mosquitto para aplicar as alterações:
```
sudo service mosquitto restart
```

Agora é possível a visualização e publicação de tópicos entre dispositivos. Pode-se testar utilizando um terminal para visualização e outro para publicação, respectivamente:
```
mosquitto_sub -h localhost -t /sw -u (usuario) -P (senha)
```
```
mosquitto_pub -h localhost -t /sw -u (usuario) -P (senha)
```
