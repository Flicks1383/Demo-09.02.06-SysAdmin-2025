# <div align="center"><strong>⚙️</strong></div> <div align="center"><strong>МОДУЛЬ 1</strong></div>

<br/>

<p align="center">
  <img src="https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/Диаграмма%20без%20названия.jpg?raw=true" alt="Топология" />
</p>

### <p align="center"><strong>Топология</strong></p>

<br/>

## ✔️ Задание 1
### Произведите базовую настройку устройств

> [!NOTE]
> **По ходу выполнения заданий, можно воспользоваться сразу же редактором файла, вместо создания командой TOUCH**

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
<summary><strong>[Решение]</strong></summary>
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

### <p align="center"><strong>Таблицы адрессации </strong></p>

<br/>

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

# <br/>

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


## > Настройка адрессации <

## <p align="center"><strong>ISP - Настройка в сторону `провайдера`</strong></p>

Создать папку по пути `/etc/net/ifaces/enp6s18`

  ```
  mkdir /etc/net/ifaces/enp6s18
  ```

- Далее требуется создать файл: `options`
  
  ```
  vi /etc/net/ifaces/enp6s18/options
  ```

- После чего привести файл `options` к следующему виду:
```
DISABLED=no
TYPE=eth
BOOTPROTO=dhcp
CONFIG_IPV4=yes
```  
</br>



## <p align="center"><strong>Настройка интерфейса `ISP` в сторону `HQ-RTR`</strong></p>
- Создать папку по пути `/etc/net/ifaces/enp6s19`
  ```
  mkdir /etc/net/ifaces/enp6s19
  ```  
- Далее требуется создать файлы: `options`, `ipv4address`
  ```
  vi /etc/net/ifaces/enp6s19/options
    
  vi /etc/net/ifaces/enp6s19/ipv4address
  ```  
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


## <p align="center"><strong>Настройка интерфейса `ISP` в сторону `BR-RTR`</strong></p>

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


## <p align="center"><strong>Настройка адрессации `HQ-RTR` & `BR-RTR`</strong></p>

**Настройка адресации на `HQ-RTR` проиcходит в режиме `configure terminal`** 
```
interface ISP 
  ip address 172.16.4.2/28
!
port te0
  service-instance toISP
  encapsulation untagged
  connect ip interface ISP
wr mem
```
#

**Настройка адресации на `BR-RTR` происходит в режиме `configure terminal`** 
```
interface ISP  
  ip address 172.16.5.2/28  
port te0
  service-instance toISP
  encapsulation untagged
  connect ip interface ISP
wr mem
```

## <p align="center"><strong>Клиентские машины `HQ-SRV`, `HQ-CLI`, `BR-SRV`</strong></p>

### <p align="center"><strong>HQ-SRV</strong></p>

**`/etc/net/ifaces/*имя интерфейса*/options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```
</br>

**`/etc/net/ifaces/*имя интерфейса*/ipv4address`**
```
192.168.100.62/26
```
</br>

**`/etc/net/ifaces/*имя интерфейса*/ipv4route`**
```
default via 192.168.100.1
```

### <p align="center"><strong>HQ-CLI</strong></p>

</details>

<br/>

## ✔️ Задание 2

### Настройка ISP

- Настройте адресацию на интерфейсах:

  - Интерфейс, подключенный к магистральному провайдеру, получает адрес по DHCP **[Выполнено в задании 1]**

  - Настройте маршруты по умолчанию там, где это необходимо 

  - Интерфейс, к которому подключен HQ-RTR, подключен к сети 172.16.4.0/28 **[Выполнено в задании 1]**

  - Интерфейс, к которому подключен BR-RTR, подключен к сети 172.16.5.0/28 **[Выполнено в задании 1]**

  - На ISP настройте динамическую сетевую трансляцию в сторону HQ-RTR и BR-RTR для доступа к сети Интернет

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>



## Настройка маршрута по умолчанию

Прописываем шлюз по умолчанию:
```yml
default via *адрес шлюза*
```

<br/>



## Настройка динамической сетевой трансляции на ISP

```
echo net.ipv4.ip_forward=1 > /etc/sysctl.conf
apt-get install iptables –y   
iptables –t nat –A POSTROUTING –s 172.16.4.0/28 –o enp6s18 –j MASQUERADE  
iptables –t nat –A POSTROUTING –s 172.16.5.0/28 –o enp6s18 –j MASQUERADE  
iptables-save > /etc/sysconfig/iptables  
systemctl restart iptables  
```

> Для проверки можно использовать команду: **`iptables –L –t nat`** - должны высветится в Chain POSTROUTING две настроенные подсети

#

</details>

<br/>

## ✔️ Задание 3

### Создание локальных учетных записей

- Создайте пользователя sshuser на серверах HQ-SRV и BR-SRV

  - Пароль пользователя sshuser с паролем P@ssw0rd

  - Идентификатор пользователя 1010

  - Пользователь sshuser должен иметь возможность запускать sudo без дополнительной аутентификации.

  - Создайте пользователя net_admin на маршрутизаторах HQ-RTR и BR-RTR

  - Пароль пользователя net_admin с паролем P@$$word

  - При настройке на EcoRouter пользователь net_admin должен обладать максимальными привилегиями

  - При настройке ОС на базе Linux, запускать sudo без дополнительной аутентификации

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>

- ### Создание учёток на Linux `КРОМЕ ISP`:
```
useradd sshuser -u 1010
passwd P@ssw0rd
```

Добавляем в группу **wheel**:
```yml
usermod -aG wheel sshuser
```

<br/>

Добавляем строку в **`/etc/sudoers`**:
```yml
sshuser ALL=(ALL) NOPASSWD:ALL
```
> Позволяет запускать **sudo** без аутентификации 

<br/>

- ## Создание учёток на EcoRouter:
```
username net_admin
password P@ssw0rd
role admin
```

</details>

<br/>

## ❌/✔️ Задание 4

### Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор

- Сервер HQ-SRV должен находиться в ID VLAN 100
- Клиент HQ-CLI в ID VLAN 200
- Создайте подсеть управления с ID VLAN 999
- Основные сведения о настройке коммутатора и выбора реализации разделения на VLAN занесите в отчёт

<br/>

<details>
<summary>[В процессе]</summary>
<br/>

### Конфигурация VLAN на HQ-RTR

Создание интерфейсов и привязка с физ.портом на **`HQ-RTR`**
```
interface CLI
  ip address 192.168.200.1/28
!
port te1
  service-instance toCLI
  encapsulation dot1Q 200
  rewrite pop 1
  connect ip interface CLI
!
interface SRV
  ip address 192.168.100.1/26
!
port te1
  service-instance toSRV
  encapsulation dot1Q 100
  rewrite pop 1
  connect ip interface SRV
wr mem
```
>`wr mem` - сохранение конфигурации роутера после изменения настроек


----------**В процессе**----------

</details>

<br/>

## ✔️ Задание 5

### Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV

- Для подключения используйте порт 2024
- Разрешите подключения только пользователю sshuser
- Ограничьте количество попыток входа до двух
- Настройте баннер «Authorized access only»

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>

# > Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV <

#

## Для настройки SSH необходимо его установить коммандой 
`apt-get install ssh-server`

#

- После чего необходимо добавить строчки в файл `/etc/openssh/sshd_config`
```
Port 2024
MaxAuthTries 2
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
           ^ - это TAB
```
- После чего требуется создать файл `/etc/openssh/bannermotd`
```
----------------------
Authorized access only
----------------------
```
- Далее необходимо перезапустить SSH коммандой
  
`systemctl restart sshd`

#

</details>

<br/>

## ✔️ Задание 6

### Между офисами HQ и BR необходимо сконфигурировать IP-туннель

- Сведения о туннеле занесите в отчёт

- На выбор технологии GRE или IP in IP

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>


# > Конфигурация GRE туннеля <

- Настройка производится на **HQ-RTR** и **BR-RTR**

```
####настройка производится на HQ-RTR####

interface tunnel.0
  ip address 172.16.0.1/30
  ip mtu 1400
  ip tunnel 172.16.4.2 172.16.5.2 mode gre
```
> На `BR-RTR` настройка похожа, но меняется IP адрес туннеля, и меняются IP адреса строкой ниже

#

</details>

<br/>

## ✔️ Задание 7

### Обеспечьте динамическую маршрутизацию: ресурсы одного офиса должны быть доступны из другого офиса. Для обеспечения динамической маршрутизации используйте `link state` протокол на ваше усмотрение

- Разрешите выбранный протокол только на интерфейсах в ip туннеле

- Маршрутизаторы должны делиться маршрутами только друг с другом

- Обеспечьте защиту выбранного протокола посредством парольной защиты

- Сведения о настройке и защите протокола занесите в отчёт

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>

# > Настройка динамической маршрутизации <

<br/>

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
- Настройка для **BR-RTR** идентичная, изеняется только **`router-id`**, **`area 3`**

</details>

<br/>

## ✔️ Задание 8

### Настройка динамической трансляции адресов

> [!NOTE]
> Пул адрессов можно посмотреть в таблице <strong>[Задания 1](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module1#задание-1)</strong> или же отталкиваться от вашей адрессации.

- Настройте динамическую трансляцию адресов для обоих офисов.

- Все устройства в офисах должны иметь доступ к сети Интернет

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>

# > Настройка динамичесткой трансляции адресов <

<br/>

> ### Настройка на `ISP выполнена` в [Задании 2](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module1#%EF%B8%8F-задание-2)

<br/>

- Настройка на **`HQ-RTR`** выглядит следующим образом:

```
int te1
  ip nat inside
!
int te2
  ip nat inside
!
int ISP
  ip nat outside
!
ip nat pool NAT_POOL 192.168.100.1-192.168.100.62,192.168.200.1-192.168.200.14
!
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface te0
```
> `int te0`  - Порт от которого приходит инет
> 
> `int te1` - Порт которому идёт инет
>
> **`int te2`**


</br>

- Настройка на **`BR-RTR`** выглядит следующим образом:

```
 int te1
  ip nat inside
!
int te0
  ip nat outside
!
ip nat pool NAT_POOL 192.168.0.1-192.168.0.30
!
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
```  
> **`ОБЯЗАТЕЛЬНО`** смотрите на адреса пула и вашей сети, если пул адресов методички отличается от вашей, то делайте на основе вашей адресации сети!!!
</br>

</details>

</br>

## ✔️ Задание 9

### Настройка протокола динамической конфигурации хостов

- Настройте нужную подсеть

- Для офиса HQ в качестве сервера DHCP выступает маршрутизатор HQ-RTR.

- Клиентом является машина HQ-CLI.

- Исключите из выдачи адрес маршрутизатора

- Адрес шлюза по умолчанию – адрес маршрутизатора HQ-RTR.

- Адрес DNS-сервера для машины HQ-CLI – адрес сервера HQ-SRV.

- DNS-суффикс для офисов HQ – au-team.irpo

- Сведения о настройке протокола занесите в отчёт

<br/>

<details>
<summary><strong>[Решение]</strong></summary>
<br/>

# > Настройка динамической конфигурации хостов <

<br/>

Создаем **пул** для **DHCP-сервера** на **`HQ-RTR`**:
```yml
ip pool cli_pool 192.168.200.14-192.168.200.14
```

<br/>

Настраиваем сам **DHCP-сервер**:
```yml
dhcp-server 1
  pool cli-pool 1
  mask 255.255.255.240
  gateway 192.168.200.1
  dns 192.168.100.62
  domain-name au-team.irpo
```

> `pool` - Привязка **пула**

> `mask` - Указание **маски** для выдаваемых адресов из пула

> `gateway` - Указание **шлюза по умолчанию** для клиентов

> `dns` - Указание **DNS-сервера** для клиентов

> `domain-name` - Указание **DNS-суффикса** для офиса **HQ**

<br/>

Привязываем **DHCP-сервер** к интерфейсу (смотрящий в сторону **CLI**):
```yml
interface CLI
  dhcp-server 1
```

</details>


# > Настройка DNS <
## Основной DNS-сервер реализован на HQ-SRV
### Для работы с DNS требуется установить "bind" командой `apt-get install bind9`  
- Далее необходимо сконфигурировать файл `/etc/bind/options.conf` таким образом:
```
listen-on { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
forwarders { 77.88.8.8; };
recursion yes;
allow-query { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
allow-query-cache { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
allow-recursion { 127.0.0.1; 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };
```  
- Конфигурация ключей rndc: `rndc-confgen > /etc/rndckey`  
- После чего требуется привести файл `/etc/bind/rndc.key` к следующему виду:
```
//key "rndc-key" {
//  secret "@RNDC_KEY@";
//};
key "rndc-key" {
  algorithm hmac-sha256;
  secret "VTmhjyXFDo0QpaBl3UQWx1e0g9HElS2MiFDtNQzDylo=";
};
```
- После чего, для проверки, можно использовать комманду `named-checkconf`
- Далее необходимо запустить утилиту коммандой `systemctl enable --now bind`
- Далее требуется изменить конфигурацию файла `resolv.conf`
```
search au-team.irpo
nameserver 127.0.0.1
nameserver 192.168.100.62
nameserver 77.88.8.8
search yandex.ru
```
- После чего требуется прописать в `/etc/bind/local/conf`:
```
zone "au-team.irpo" {
  type master;
  file "au-team.irpo.db";
};
```
- Командой `cp /etc/bind/zone/localdomain /etc/bind/zone/au-team.irpo.db` создается копия файла  
Которому присваиваются права: 
```
chown named. /etc/bind/zone/au-team.irpo.db
chmod 600 /etc/bind/zone/au-team.irpo.db
```
- После чего приводим файл к следующему виду:
```
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
        IN      A       192.168.100.62
hq-rtr  IN      A       192.168.100.1
br-rtr  IN      A       192.168.0.1
hq-srv  IN      A       192.168.100.62
hq-cli  IN      A       192.168.200.14
br-srv  IN      A       192.168.0.30
moodle  IN      CNAME   hq-rtr
wiki    IN      CNAME   hq-rtr
```
- Далее файл `/etc/bind/local.conf` приводим к следующему виду:
```
zone "100.168.192.in-addr.arpa" {
  type master;
  file "100.168.192.in-addr.arpa";
};

zone "200.168.192.in-addr.arpa" {
  type master;
  file "200.168.192.in-addr.arpa";
};

zone "0.168.192.in-addr.arpa" {
  type master;
  file "0.168.192.in-addr.arpa";
};
```
- После чего создаем файлы командами
```
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/100.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/200.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/0.168.192.in-addr.arpa
```
- После этого задаем права файлам командами:
```
chown named. /etc/bind/zone/100.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/100.168.192.in-addr.arpa
chown named. /etc/bind/zone/200.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/200.168.192.in-addr.arpa
chown named. /etc/bind/zone/0.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/0.168.192.in-addr.arpa
```
- После изменений файл `100.168.192.in-addr.arpa` выглядит так:
```
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; Serial
                                12H             ; Refresh
                                1H              ; Retry
                                1W              ; Expire
                                1H              ; Ncache
                        )
        IN      NS      localhost.
1       IN      PTR     hq-rtr.au-team.irpo.
62      IN      PTR     hq-srv.au-team.irpo.
```
- После изменений файл `200.168.192.in-addr.arpa` выглядит так:
```
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; Serial
                                12H             ; Refresh
                                1H              ; Retry
                                1W              ; Expire
                                1H              ; Ncache
                        )
        IN      NS      localhost.
14      IN      PTR     hq-cli.au-team.irpo.
```
- После изменений файл `0.168.192.in-addr.arpa` выглядит так:
```
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; Serial
                                12H             ; Refresh
                                1H              ; Retry
                                1W              ; Expire
                                1H              ; Ncache
                        )
        IN      NS      localhost.
1       IN      PTR     br-rtr.au-team.irpo.
30      IN      PTR     br-srv.au-team.irpo.
```
Все пробелы выше ^ ставятся TAB'ом
- После чего можно проверить ошибки командой
```
named-checkconf -z
```
- А также перезапускаем `bind` командой
```
systemctl restart bind
```
- Проверить работоспособность можно командой
```
nslookup **IP-адрес/DNS-имя**
```
# > Настройте часовой пояс на всех устройствах <
- На Linux настраивается часовой пояс командой
```
timedatectl set-timezone Asia/Tomsk
```  
- На EcoRouter настраивается часовой пояс командой
```
ntp timezone utc+7
```
