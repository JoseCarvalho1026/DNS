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

Besides de option of copying the file "db.local", you can choose to simply create `nano db.DOMAIN` and copy the following example:
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

The same procedure repeats itself for the file "db.IP-Reverse", you can choose to simply create `nano db.IP-Reverse` and copy the following example:
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
In case you don't follow any of the previous options, Caso não opte pelas duas opções anteriores, configure the files that were copied:

◻️ `nano db.DOMAIN` ;
```
 CTRL + \ (search and procura e substitui: localhost >> DOMAIN)
 Configura a tua forward zone
```
◻️ `nano db.IP-R` ;
```
CTRL + \ (procura ans replace: localhost >> DOMAIN)
Configure your reverse zone
```
◻️ `mv db.DOMAIN /var/lib/bind/` ;

◻️ `mv db.IP-R /var/lib/bind/` ;

◻️ `nano named.conf.default-zones` ;
```
Copy the following examples of forward and reverse zone.
```
◻️ `nano named.conf.local` ;
```
Paste the examples of forward and reverse zone that were copied from the other file;
Configurar as forward e reverse zones.
```
◻️ `systemctl restart bind9` ;

◻️ `nslookup SITE IP` ;

◻️ `dig SITE @IP` .
