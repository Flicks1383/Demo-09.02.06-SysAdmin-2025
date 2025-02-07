# <div align="center"><strong>Демонстрационный экзамен (AltLinux+EcoRouter)</strong></div>

### <div align="center"><strong>Описание</strong> </div>
<div align="center">Инструкция для написания демонстрационного экзамена 2025 года для специальности</div> <div align="center"><strong>СЕТЕВОЕ И СИСТЕМНОЕ АДМИНИСТРИРОВАНИЕ 09.02.06</strong></div>
</br>

>[!WARNING]
>Убедительная просьба, перед тем как начинать настраивать машины, **ДЕЛАЙТЕ СНАПШОТИКИ**, для отката после каждого выполненного задания !!!

>[!WARNING]
>Так же не забывайте про **`wr mem`** !!!

#


### Модули и их решения: 

+ **[⚙️МОДУЛЬ 1]()** 
<details>
  <summary><ins>Содержание</ins></summary> 
  
  1. **[Произведите _базовую настройку_ устройств](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-1)**
  
  2. **[Настройка _ISP_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-2)**
  
  3. **[Создание _ЛОКАЛЬНЫХ_ учетных записей](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-3)**
  
  4. **[Настройте на интерфейсе _HQ-RTR_ в сторону офиса _HQ_ виртуальный коммутатор](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#-задание-4)**
   
  5. **[Настройка безопасного удаленного доступа на серверах _HQ-SRV_ и _BR-SRV_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-5)**
  
  6. **[Между офисами _HQ_ и _BR_ необходимо сконфигурировать _IP-туннель_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-6)**

  7. **[Обеспечьте _ДИНАМИЧЕСКУЮ МАРШРУТИЗАЦИЮ_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-7)**

  8. **[Настройка _ДИНАМИЧЕСКОЙ ТРАНСЛЯЦИИ АДРЕСОВ_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module1/README.md#%EF%B8%8F-задание-8)**

  9. **[Настройка _ПРОТОКОЛА ДИНАМИЧЕСКОЙ КОНФИГУРАЦИИ ХОСТОВ_]()**

  10. **[Настройка _DNS для офисов HQ и BR_]()**

  11. **[Настройте _ЧАСОВОЙ ПОЯС_ на всех устройствах, согласно месту проведения экзамена]()**
    
  </details>

</br>

+ **[⚙️МОДУЛЬ 2](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2)**
<details>
  <summary><ins>Содержание</ins></summary>

1. **[Настройте доменный контроллер _SAMBA_ на машине _BR-SRV_](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2#настройте-доменный-контроллер-samba-на-машине-br-srv)**
    
2. **[Сконфигурируйте _ФАЙЛОВОЕ ХРАНИЛИЩЕ_](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2#сконфигурируйте-файловое-хранилище)**

3. **[Настройте службу сетевого времени на базе сервиса _CHRONY_](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2#настройте-службу-сетевого-времени-на-базе-сервиса-chrony)**

4. **[Сконфигурируйте _ANSIBLE_ на сервере BR-SRV](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2#сконфигурируйте-ansible-на-сервере-br-srv)**
    
5. **[Развертывание приложений в _DOCKER_ на сервере BR-SRV](https://github.com/Flicks1383/Demo09.02.06_2025/tree/main/module2#развертывание-приложений-в-docker-на-сервере-br-srv)**
    
6. **[На маршрутизаторах сконфигурируйте _СТАТИЧЕСКУЮ ТРАНСЛЯЦИЮ ПОРТОВ_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module2/README.md#на-маршрутизаторах-сконфигурируйте-статическую-трансляцию-портов)**

7. **[Запустите сервис _MOODLE_ на сервере _HQ-SRV_:](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module2/README.md#запустите-сервис-moodle-на-сервере-hq-srv)**

8. **[Настройте веб-сервер _NGINX_ как обратный _ПРОКСИ-СЕРВЕР_ на _HQ-RTR_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module2/README.md#настройте-веб-сервер-nginx-как-обратный-прокси-сервер-на-hq-rtr)**

9. **[Удобным способом установите приложение _Яндекс Браузере_ для организаций на _HQ-CLI_](https://github.com/Flicks1383/Demo09.02.06_2025/blob/main/module2/README.md#удобным-способом-установите-приложение-яндекс-браузере-для-организаций-на-hq-cli)**
  </details>

#



### Репозитории добряков откуда взят материал:
+ **>[damh66](https://github.com/damh66/demo2025)**
+ **>[ItsLiventsev](https://github.com/ItsLiventsev/NetSys_Demo_2025?tab=readme-ov-file)**
+ **>[abdurrah1m](https://github.com/abdurrah1m/DEMO2025/blob/main/README.md)**
+ **>[doughboyjaba](https://github.com/doughboyjaba/demo25)**
+ **>[каб-220](http://каб-220.рф/ru/demo-2025/modul-1/modul-1-1)**

#



### Решения проблем
