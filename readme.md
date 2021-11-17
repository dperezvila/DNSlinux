## Readme Docker-Compose 

### cliente + servidor dns

#### Docker-Compose
- version: "3.3" : Indica la version
- services: Aquí vamos a definir los servicios
- asir_bind9: Creas el servicio asir_bind9
- container_name: asir_bind9 : Le asignas el nombre al contenedor
- image: internetsystemsconsortium/bind9:9.11 : Asignas la imagen del bind 9
- networks: Defines la redes
- br02: Asignas una red (Previamente creada)
- ipv4_address: 10.0.2.250 : Asignas una ip a la red
- volumes: Defines los volúmenes
- conf:/etc/bind : Asignas el volumen conf
- asir_cliente: Creas el servicio asir_cliente
- container_name: asir_cliente : Le asignas el nombre al contenedor
- image: ubuntu  : Asignas la imagen de ubuntu
- networks: Defines las redes
- br02 : Asignas la red
- stdin_open: true y tty: true : Crea el terminal        
- dns: Configuras el DNS
- -10.0.2.250 : Configuras la IP del DNS
- volumes: Configuras los volúmenes
- conf: Defines el volumen conf
- external: true : Dices que el volumen ya está creado
- networks: Defines la red
- br02: Asignas la red 
- external: true : Le dices que la red ya está creada

#### Creación de servicios

crear red
docker network create --subnet 10.0.2.0/24 --gateway 10.0.2.1 br02

crear volumen
docker volume create conf

crear contenedores
docker-compose up -d


#### Forwarders
Editas /etc/bind/named.conf.options y añades esto:

forwarders {
    8.8.8.8;
    8.8.4.4;
};