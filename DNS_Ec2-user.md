# DNS installation and configuration

◻️ `sudo su -` ;

◻️ `yum install bind -y` ;

◻️ `systemctl enable --now named` ;

◻️ `systemctl status named` ;

◻️ `cp /etc/named.conf /etc/named.conf_` in case of security ;

◻️ `nano /etc/named.conf` ;

Modify:
```
listen... any;
listen... any;
dns...enable no;
dns...tion no;
```
Copy and paste the following below `dns...tion no;`:
```
forwarders  {
      8.8.8.8;
};
```
Copy and paste the following above `include "/etc/named.rfc1912.zones";`:
```
zone "enta.pt" {
        type master;
        file "/var/named/db.enta.pt";
};
zone "31.172.in-addr.arpa" {
        type master;
        file "/var/named/db.31.172";
};
```
◻️ `cd /var/named` ;

◻️ `nano db.enta.pt` ;
```
@       IN      SOA     enta.pt. root.enta.pt. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS              enta.pt.
@               IN      A               172.31.0.100
ns              IN      A               172.31.0.100

control         IN      A               172.31.0.100
control         IN      A               172.31.1.100
control         IN      A               172.31.2.100
dmz             IN      A               172.31.1.101
www             IN      CNAME           dmz.enta.pt.
```
◻️ `nano db.31.172` ;
```
$TTL    604800
@       IN      SOA     enta.pt. root.enta.pt. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      enta.pt.
100.0   IN      PTR     control.enta.pt.
100.1   IN      PTR     control.enta.pt.
100.2 IN      PTR     control.enta.pt.

101.1   IN      PTR     dmz.enta.pt.
101.1   IN      PTR     www.enta.pt.
```
◻️ `systemctl restart named` ;

◻️ `systemctl status named` ;

◻️ `nano /etc/sysconfig/network-scripts/ifcfg-eth0` ;

Add:
```
DNS1=172.31.0.100
```
◻️ `systemctl restart network` ;

◻️ `nslookup SITE` ;

◻️ `dig SITE @IP` .
