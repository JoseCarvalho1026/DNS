# DNS

◻️ `sudo su -` ;

◻️ `yum install bind -y` ;

◻️ `systemctl enable --now named` ;

◻️ `systemctl status named` ;

◻️ `cp /etc/named.conf /etc/named.conf_` para caso de segurança ;

◻️ `nano /etc/named.conf` ;
```
listen... any;
listen... any;
dns...enable no;
dns...tion no;
```
```
zone "enta.com" {
   type master;
   file "/var/named/db.enta.pt";
};
zone "31.172.in-addr.arpa" {
   type master;
   file "/var/named/db.31.172";
};
```
◻️ `cd /var/named` ;

◻️ `nano db.DOMAIN` ;
```
$TTL    86400
@               IN SOA  DOMAIN. root (
                        42              ; serial
                        3H              ; refresh
                        15M             ; retry
                        1W              ; expiry
                        1D )            ; minimum
         IN NS  ns
ns       IN A   172.31.0.100
www      IN A   172.31.1.101
```
◻️ `nano db.IP-Reverse` ;
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
```
◻️ `systemctl restart named` ;

◻️ `systemctl status named` ;

◻️ `nano /etc/sysconfig/network-scripts/ifcfg-eth0` ;

Adicionar:
```
DNS1=172.31.162.100
DNS2=8.8.8.8
```
◻️ `systemctl restart network` ;

◻️ `nslookup SITE IP` ;

◻️ `dig SITE @IP` .
