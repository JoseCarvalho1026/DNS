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

◻️ `cp db.127 db.IP-Reverse` ;

◻️ `mv db.DOMAIN /var/lib/bind/` ;

◻️ `mv db.IP-R /var/lib/bind/` ;

◻️ `cd /var/lib/bind/` ;

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
◻️ `cd /etc/bind/` ;

◻️ `nano named.conf.default-zones` ;
```
Copias os exemplos de forward e reverse zone.
```
◻️ `nano named.conf.local` ;
```
Colar o que copiaste do outro ficheiro;
Configura as tuas forward e reverse zones.
```
◻️ `systemctl restart bind9` ;

◻️ `nslookup SITE IP` ;

◻️ `dig SITE @IP` .
