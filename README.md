# 6to4-
Learn how to set up and configure 6to4 IPv6 tunneling on Linux with this comprehensive guide and accompanying repository. 


 دستورات تانل سرور ایران

1) nano /etc/rc.local

2) کپی کنید /etc/rc.local این دستورات رو در فایل 
و آیپی خارج و ایران رو در جاهایی که گفته شده جایگزین کنید

#!/bin/bash
ip tunnel add 6to4tun_KH mode sit remote ipIran local ipKharej
ip -6 addr add 2001:470:1f10:e1f::2/64 dev 6to4tun_KH
ip link set 6to4tun_KH mtu 1480
ip link set 6to4tun_KH up

ip -6 tunnel add GRE6Tun_KH mode ip6gre remote 2001:470:1f10:e1f::1 local 2001:470:1f10:e1f::2
ip addr add 172.16.1.2/30 dev GRE6Tun_KH
ip link set GRE6Tun_KH mtu 1436
ip link set GRE6Tun_KH up

iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD  -j ACCEPT
sudo sysctl -w net.ipv4.ip_forward=1
echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf
sysctl -p
service iptables save
service iptables restart
service iptables stop
service iptables start

بعد از سیو کردن و خروج این دستورات رو به ترتیب وارد کنید

4) chmod +x /etc/rc.local

5) echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf sysctl -p

6) /etc/rc.local



دستورات تانل سرور خارج

1) nano /etc/rc.local

2) کپی کنید /etc/rc.local این دستورات رو در فایل 
و آیپی خارج و ایران رو در جاهایی که گفته شده جایگزین کنید

#!/bin/bash
ip tunnel add 6to4tun_KH mode sit remote #ipIran local #ipKharej
ip -6 addr add 2001:470:1f10:e1f::2/64 dev 6to4tun_KH
ip link set 6to4tun_KH mtu 1480
ip link set 6to4tun_KH up

ip -6 tunnel add GRE6Tun_KH mode ip6gre remote 2001:470:1f10:e1f::1 local 2001:470:1f10:e1f::2
ip addr add 172.16.1.2/30 dev GRE6Tun_KH
ip link set GRE6Tun_KH mtu 1436
ip link set GRE6Tun_KH up

iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD  -j ACCEPT
sudo sysctl -w net.ipv4.ip_forward=1
echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf
sysctl -p
service iptables save
service iptables restart
service iptables stop
service iptables start

بعد از سیو کردن و خروج این دستورات رو به ترتیب وارد کنید

4) chmod +x /etc/rc.local

5) echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf sysctl -p

6) /etc/rc.local


الان هردو سرور شما متصل شدن و شما آیپی ورژن 6 لوکال دارید

آیپی خارج : 
2001:470:1f10:e1f::2

آیپی ایران : 
2001:470:1f10:e1f::1

حالا میتونید با هر روشی مثل دکودمودور از این آیپی خارج برای تانل استفاده کنید


https://t.me/nyx_host