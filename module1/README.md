# ⚙️Модуль 1

<p align="center">
  <img src="https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/Диаграмма%20без%20названия.jpg" alt="Топология" />
</p>
<p align="center"><strong>Топология</strong></p>

## Задание 1
### Произведите базовую настройку устройств

- Настройте имена устройств согласно топологии. Используйте полное доменное имя
- На всех устройствах необходимо сконфигурировать IPv4
- IP-адрес должен быть из приватного диапазона, в случае, если сеть локальная, согласно RFC1918
- Локальная сеть в сторону HQ-SRV(VLAN100) должна вмещать не более 64 адресов
- Локальная сеть в сторону HQ-CLI(VLAN200) должна вмещать не более 16 адресов
- Локальная сеть в сторону BR-SRV должна вмещать не более 32 адресов
- Локальная сеть для управления(VLAN999) должна вмещать не более 8 адресов
- Сведения об адресах занесите в отчёт, в качестве примера используйте Таблицу 3
<br/>
<details>
<summary><strong>---Решение---</strong></summary>
<br/>
  
   ## > Настройка имени устройств <
  - Для **Linux** используется команда `hostnamectl set-hostname (имя устройства.au-team.irpo)`
    
  - Для **EcoRouter** используется команда `hostname (имя устройства)`
    
>ISP: `isp.au-team.irpo`
>
>HQ-RTR: `hq-rtr.au-team.irpo`
>
> BR-RTR: `br-rtr.au-team.irpo`
>
> HQ-SRV: `hq-srv.au-team.irpo`
>
> HQ-CLI: `hq-cli.au-team.irpo`
>
> BR-SRV: `br-srv.au-team.irpo`

#

<table align="center">
  <tr>
    <td align="center"><strong>Сеть</strong></td>
    <td align="center"><strong>Адрес подсети</strong></td>
    <td align="center"><strong>Пул-адресов</strong></td>
  </tr>
  <tr>
    <td align="center">SRV-Net (VLAN 100)</td>
    <td align="center">192.168.100.0/26</td>
    <td align="center">192.168.100.1 - 62</td>
  </tr>
  <tr>
    <td align="center">CLI-Net (VLAN 200)</td>
    <td align="center">192.168.200.0/28</td>
    <td align="center">192.168.200.1 - 14</td>
  </tr>
  <tr>
    <td align="center">BR-Net</td>
    <td align="center">192.168.0.0/27</td>
    <td align="center">192.168.0.1 - 30</td>
  </tr>
  <tr>
    <td align="center">MGMT (VLAN 999)</td>
    <td align="center">192.168.99.0/29</td>
    <td align="center">192.168.99.1 - 6</td>
  </tr>
  <tr>
    <td align="center">ISP-HQ</td>
    <td align="center">172.16.4.0/28</td>
    <td align="center">172.16.4.1 - 14</td>
  </tr>
  <tr>
    <td align="center">ISP-BR</td>
    <td align="center">172.16.5.0/28</td>
    <td align="center">172.16.5.1 - 14</td>
  </tr>
</table>
<p align="center"><strong>Таблица подсетей</strong></p>

<br/>

<table align="center">
  <tr>
    <td align="center"><strong>Устройство</strong></td>
    <td align="center"><strong>Интерфейс</strong></td>
    <td align="center"><strong>IPv4/IPv6</strong></td>
    <td align="center"><strong>Маска/Префикс</strong></td>
    <td align="center"><strong>Шлюз</strong></td>
    <td align="center"><strong>Сеть</strong></td>
  </tr>
  <tr>
    <td align="center" rowspan="3">ISP</td>
    <td align="center">enp6s18</td>
    <td align="center">192.168.###.### (DHCP)</td>
    <td align="center">/##</td>
    <td align="center">192.168.###.###</td>
    <td align="center">INTERNET</td>
  </tr>
  <tr>
    <td align="center">enp6s19</td>
    <td align="center">172.16.4.1</td>
    <td align="center">/28</td>
    <td align="center"></td>
    <td align="center">ISP-HQRTR</td>
  </tr>
  <tr>
    <td align="center">enp6s20</td>
    <td align="center">172.16.5.1</td>
    <td align="center">/28</td>
    <td align="center"></td>
    <td align="center">ISP-BRRTR</td>
  </tr>
  <tr>
    <td align="center" rowspan="3">HQ-RTR</td>
    <td align="center">te0/int0</td>
    <td align="center">172.16.4.2</td>
    <td align="center">/28</td>
    <td align="center">172.16.4.1</td>
    <td align="center">ISP-HQRTR</td>
  </tr>
  <tr>
    <td align="center">vlan100/int1</td>
    <td align="center">192.168.100.1</td>
    <td align="center">/26</td>
    <td align="center"></td>
    <td align="center">HQRTR-CLI</td>
  </tr>
  <tr>
    <td align="center">vlan200/int2</td>
    <td align="center">192.168.200.1</td>
    <td align="center">/28</td>
    <td align="center"></td>
    <td align="center">HQRTR-SRV</td>
  </tr>
  <tr>
    <td align="center" rowspan="2">BR-RTR</td>
    <td align="center">te0/int0</td>
    <td align="center">172.16.5.2</td>
    <td align="center">/28</td>
    <td align="center">172.16.5.1</td>
    <td align="center">ISP-BRRTR</td>
  </tr>
  <tr>
    <td align="center">te1/int1</td>
    <td align="center">192.168.0.1</td>
    <td align="center">/27</td>
    <td align="center"></td>
    <td align="center">BRRTR-SRV</td>
  </tr>
  <tr>
    <td align="center">HQ-SRV</td>
    <td align="center">enp6s##</td>
    <td align="center">192.168.100.62</td>
    <td align="center">/26</td>
    <td align="center">192.168.100.1</td>
    <td align="center">HQRTR-SRV</td>
  </tr>
  <tr>
    <td align="center">BR-SRV</td>
    <td align="center">enp6s##</td>
    <td align="center">192.168.0.30</td>
    <td align="center">/27</td>
    <td align="center">192.168.0.1</td>
    <td align="center">HQRTR-SRV</td>
  </tr>
  <tr>
    <td align="center">HQ-CLI</td>
    <td align="center">enp6s##</td>
    <td align="center">192.168.200.14</td>
    <td align="center">/28</td>
    <td align="center">192.168.200.1</td>
    <td align="center">HQRTR-CLI</td>
  </tr>
</table>
<p align="center"><strong>Таблица адресации</strong></p>
      
</details>


#


# > Настройка адресации на устройствах <
## Для корректной работы интернета на ISP требуется:
- Создать папку по пути `/etc/net/ifaces/enp6s18`  
- Далее требуется создать файлы: `options`  
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
           ^ - это TAB
```
После чего требуется создать файл /etc/openssh/bannermotd
```
Authorized access only
```
Далее необходимо перезапустить SSH коммандой `systemctl restart sshd`
# > Конфигурация GRE туннеля <
## Настройка производится на HQ-RTR и BR-RTR
```
interface tunnel.0
  ip address 172.16.0.1/30
  ip tunnel 172.16.4.2 172.16.5.2 mode gre
```
- На BR-RTR настройка похожа, но меняется IP адрес туннеля, и меняются IP адреса строкой ниже
# > Настройка динамической маршрутизации <
## Настройка для HQ-RTR:
```
router ospf 1
  router-id 1.1.1.1
  network 172.16.0.0/30 area 0
  network 172.16.4.0/28 area 0
  network 192.168.100.0/26 area 1
  network 192.168.200.0/28 area 2
  passive-interface default
  no passive-interface tunnel.0
```
Настройка для BR-RTR идентичная, изеняется только `router-id`, `area 3`
# > Настройка динамичесткой трансляции адресов <
## На ISP эта настройка была проведена ранее.  
Настройка на роутерах выглядит следующим образом:
```
int te1
  ip nat inside
int te2
  ip nat inside
int te0
  ip nat outside
ip nat pool NAT_POOL 192.168.100.1-192.168.100.62,192.168.200.1-192.168.200.14
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface te0
```
Настройка для BR-RTR идентична, описанной выше, за исключением пула и портов  
# > Настройка динамической конфигурации хостов <
## В качестве DHCP сервера выступает HQ-RTR. 
### Настройка для него выглядит следующим образом
```
apt-get install dhcp-server
ip pool cli_pool 192.168.200.14-192.168.200.14
dhcp-server 1
  pool pool1
  mask 255.255.255.240
  gateway 172.16.4.2
  dns 192.168.100.62
  domain-name au-team.irpo
interface te2 (возможно)
  dhcp-server 1
```
# > Настройка DNS <
## Основной DNS-сервер реализован на HQ-SRV
### Для работы с DNS требуется установить "bind" командой `apt-get install bind9`  
Далее необходимо сконфигурировать файл `/etc/bind/options.conf` таким образом:
```
listen-on { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
forwarders { 77.88.8.8; };
recursion yes;
allow-query { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
allow-query-cache { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
allow-recursion { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
```  
Конфигурация ключей rndc: `rndc-confgen > /etc/rndckey`  
После чего требуется привести файл `/etc/bind/rndc.key` к следующему виду:
```
//key "rndc-key" {
//  secret "@RNDC_KEY@";
//};
key "rndc-key" {
  algorithm hmac-sha256;
  secret "VTmhjyXFDo0QpaBl3UQWx1e0g9HElS2MiFDtNQzDylo=";
};
```
После чего, для проверки, можно использовать комманду `named-checkconf`
Далее необходимо запустить утилиту коммандой `systemctl enable --now bind`
Далее требуется изменить конфигурацию файла `resolv.conf`
```
search au-team.irpo
nameserver 127.0.0.1
nameserver 192.168.100.62
nameserver 77.88.8.8
search yandex.ru
```
После чего требуется прописать в `/etc/bind/local/conf`:
```
zone "au-team.irpo" {
  type master;
  file "au-team.irpo.db";
};
```
Командой `cp /etc/bind/zone/localdomain /etc/bind/zone/au-team.irpo.db` создается копия файла  
Которому присваиваются права: 
```
chown named. /etc/bind/zone/au-team.irpo.db
chmod 600 /etc/bind/zone/au-team.irpo.db
```
