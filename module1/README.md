# > Настройка имени устройств <
- Для Linux используется команда `hostnamectl set-hostname (имя устройства.au-team.irpo)`  
- Для EcoRouter используется команда `hostname (имя устройства)`
# > Настройка адресации на устройствах <
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
## После чего идет настройка адресации в сторону HQ-RTR:
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
## После чего идет настройка адресации в сторону BR-RTR:
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
# > Создание локальных учетных записей <
## Создание учёток на Linux ___кроме ISP___:
```
useradd sshuser -u 1010
passwd P@ssw0rd
usermod -aG wheel sshuser
sshuser ALL=(ALL) NOPASSWD:ALL
```
## Создание учёток на EcoRouter:
```
username net_admin
password P@ssw0rd
role admin
```
# > Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV <
## Для настройки SSH необходимо его установить коммандой `apt-get install ssh-server`
После чего необходимо добавить строчки в файл `/etc/openssh/sshd_config`
```
Port 2024
MaxAuthTries 2
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
```
После чего требуется создать файл /etc/openssh/bannermotd
```
Authorized access only
```
Далее необходимо перезапустить SSH коммандой `systemctl restart sshd`
