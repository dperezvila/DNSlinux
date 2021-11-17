## Readme Repositorio Configuración

### cliente + servidor dns

#### Agregar una zona

En /etc/bind/named.conf.local añades

zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};

Pones el comando "cp /etc/bind/db.local /etc/bind/db.example.com"

haces "nano /etc/bind/db.example.com"

;
; BIND data file for example.com
;
$TTL    604800
@       IN      SOA     example.com. root.example.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL

@       IN      NS      ns.example.com.
@       IN      A       10.0.2.250
@       IN      AAAA    ::1
ns      IN      A       10.0.2.250


#### Reverse Zone File

En /etc/bind/named.conf.local añades:
zone "2.0.10.in-addr.arpa" {
    type master;
    file "/etc/bind/db.10";
};

Pones el comando "sudo cp /etc/bind/db.127 /etc/bind/db.10"
Haces "nano /etc/bind/db.10"

;
; BIND reverse data file for local 10.0.2.XXX net
;
$TTL    604800
@       IN      SOA     ns.example.com. root.example.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      ns.
10      IN      PTR     ns.example.com.

#### Probando funcionalidad

Reinicias los contenedores y haces un ping a example.com