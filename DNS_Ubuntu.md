# DNS

◻️ `sudo su -` ;

◻️ `apt install bind9 -y` ;

◻️ `cd /etc/bind/` ;

◻️ `nano named.conf.options` ;
```
forwarders {
        8.8.8.8;
};
```
◻️ `cp db.local db.DOMAIN` ;

Além da opção de copiar o ficheiro "db.local", pode optar por simplesmente criar `nano db.DOMAIN` e copiar o seguinte exemplo:
```
$TTL    86400
@               IN SOA  DOMAIN. root (
                        42              ; serial
                        3H              ; refresh
                        15M             ; retry
                        1W              ; expiry
                        1D )            ; minimum
         IN NS  ns
ns       IN A   192.168.0.100
www      IN A   192.168.1.101
central  IN A   192.168.2.150
```
◻️ `cp db.127 db.IP-Reverse` ;

O mesmo procedimento se repete para o ficheiro "db.IP-Reverse", pode optar por simplesmente criar `nano db.IP-Reverse` e copiar o seguinte exemplo:
```
$TTL    604800
@       IN      SOA     ns.DOMAIN. root.DOMAIN. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@           IN      NS      ns.
100.0     IN      PTR     ns.DOMAIN.
101.1     IN      PTR     www.DOMAIN.
150.2     IN      PTR     central.DOMAIN.
```
Caso não opte pelas duas opções anteriores, configure os ficheiros que foram copiados:

◻️ `nano db.DOMAIN` ;
```
 CTRL + \ (procura e substitui: localhost >> DOMAIN)
 Configura a tua forward zone
```
◻️ `nano db.IP-R` ;
```
CTRL + \ (procura e substitui: localhost >> DOMAIN)
Configura a tua reverse zone
```
◻️ `mv db.DOMAIN /var/lib/bind/` ;

◻️ `mv db.IP-R /var/lib/bind/` ;

◻️ `nano named.conf.default-zones` ;
```
Copiar os exemplos de forward e reverse zone.
```
◻️ `nano named.conf.local` ;
```
Colar os exemplos de forward e reverse zone que foram copiados do outro ficheiro;
Configurar as forward e reverse zones.
```
◻️ `systemctl restart bind9` ;

◻️ `nslookup SITE IP` ;

◻️ `dig SITE @IP` .
