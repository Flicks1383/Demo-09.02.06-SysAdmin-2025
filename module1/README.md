# >Настройка имени устройств<
- Для Linux используется команда `hostnamectl set-hostname (имя устройства.au-team.irpo)`  
- Для EcoRouter используется команда `hostname (имя устройства)`
# >Настройка адресации на устройствах<
## Для корректной работы интернета на ISP требуется:
- Создать папку по пути `/etc/net/ifaces/enp6s18`  
- Далее требуется создать файлы: `options`, `ipv4address`  
- После чего привести файл `options` к следующему виду:
```
DISABLED=no
TYPE=eth
BOOTPROTO=dhcp
CONFIG_IPV4=yes
```  
После чего идет настройка адресации в сторону HQ-RTR:
- Создать папку по пути `/etc/net/ifaces/enp6s19`  
- Далее требуется создать файлы: `options`, `ipv4address`  
- После чего привести файл `options` к следующему виду:
```
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```
- После чего привести файл `ipv4address` к следующему виду:
```
172.16.4.1/28
```
После чего идет настройка адресации в сторону BR-RTR:
- Создать папку по пути `/etc/net/ifaces/enp6s20`  
- Далее требуется создать файлы: `options`, `ipv4address`  
- После чего привести файл `options` к следующему виду:
```
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```
- После чего привести файл `ipv4address` к следующему виду:
```
172.16.5.1/28
```
## Настрйока адресации на HQ-RTR проиcходит в режиме `configure terminal`:  
```
interface ISP  
  ip address 172.16.4.2/28  
port te0
  service-instance toISP
  encapsulation untagged
  connect ip interface ISP
wr mem
```
## Настрйока адресации на BR-RTR происходит в режиме `configure terminal`:  
```
interface ISP  
  ip address 172.16.5.2/28  
port te0
  service-instance toISP
  encapsulation untagged
  connect ip interface ISP
wr mem
```
## Настройка динамической сетевой трансляции на ISP:
```
echo net.ipv4.ip_forward=1 > /etc/sysctl.conf
apt-get install iptables –y   
iptables –t nat –A POSTROUTING –s 172.16.4.0/28 –o enp6s18 –j MASQUERADE  
iptables –t nat –A POSTROUTING –s 172.16.5.0/28 –o enp6s18 –j MASQUERADE  
iptables-save > /etc/sysconfig/iptables  
systemctl restart iptables  
```
Для проверки можно использовать команду `iptables –L –t nat`
