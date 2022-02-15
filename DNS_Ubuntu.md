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
Create `nano db.inova.pt` and copy the following example:
```                            
$TTL    86400
@               IN SOA  inova.pt. root (
                        42              ; serial
                        3H              ; refresh
                        15M             ; retry
                        1W              ; expiry
                        1D )            ; minimum
         IN NS  ns
ns       IN A   192.168.0.100
www      IN A   192.168.1.101
central  IN A   192.168.2.150
wazuh    IN A   192.168.2.151
sales    IN A   192.168.2.152
marketing IN A   192.168.2.153
```
◻️ `cp db.127 db.IP-Reverse` ;

Create `nano db.31.172` and copy the following example:
```
$TTL    604800
@       IN      SOA     ns.inova.pt. root.inova.pt. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@           IN      NS      ns.
100.0     IN      PTR     ns.inova.pt.
101.1     IN      PTR     www.inova.pt.
150.2     IN      PTR     central.inova.pt.
151.2     IN      PTR     wazuh.inova.pt.
152.2     IN      PTR     sales.inova.pt.
153.2     IN      PTR     marketing.inova.pt.
```
◻️ `mv db.inova.pt /var/lib/bind/` ;

◻️ `mv db.31.172 /var/lib/bind/` ;

◻️ `nano named.conf.default-zones` ;
```
Copy the following examples of forward and reverse zone.
```
◻️ `nano named.conf.local` ;
```
Paste the examples of forward and reverse zone that were copied from the other file;
Configurate the forward and reverse zones.
```
◻️ `systemctl restart bind9` ;

◻️ `nslookup SITE` ;

◻️ `dig SITE @IP` .
