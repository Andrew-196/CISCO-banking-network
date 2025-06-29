# Топология cisco банковской сферы
![Топология cisco банк_сферы (1)](https://github.com/user-attachments/assets/6ec3f428-c5d4-4041-b591-a05d3ba4d6bd)




```Сеть банковской сферы на CISCO```

# Количество оборудования
    Switch – 7	Switch в сети NAT |PAT – 1
    Router – 10 	Router в сети NAT | PAT - 2 
    Server – 3	Server в сети NAT | PAT - 1

# IP-адресация
# 192.168.0.0 255.255.255.0 - Front-Office
    Обслуживания клиентов
    Эти ПК используются кассирами и консультантами в отделениях банка 
    + VoIP IP-адресация   
# 5.5.5.0   255.255.255.224 - Tech-Support
    Решение проблем с интернет-банком, доступом к счетам, транзакциями и другими банковскими услугами
    + VoIP IP-адресация               
# 192.168.122.0 255.255.255.0 - Market
     ---      
# 192.168.123.0 255.255.255.0 - Application processing
		Обработка онлайн заявок
		Static IP             
# 192.168.130.0 255.255.255.0 - Security operator
    Видеонаблюдение            
# 192.168.125.0 255.255.255.0 - Currency 
    Выдача валюты клиентам 
    Access-list связь только с Back-Office
# 192.168.10.0 255.255.255.0 - Back Office
    Обработка данных, учет, финансы
    Сотрудники, занимающиеся бухгалтерией и внутренними операциями, используют эти ПК
# 192.168.10.0 255.255.255.0 - IT
    Поддержка инфраструктуры, управление сетями, безопасность данных
    Системные администраторы и ИТ-специалисты работают на этих ПК
# 200.10.123.0 255.255.255.0 - NAT | PAT network
		Хранение резервных копий данных на сервере

# Router IP-адресация (сеть)
    OSPF Network. mask 255.255.255.252
        AREA 0 
            10.10.10.0 | 10.10.10.4 |10.10.10.8 | 
            10.10.10.12 | 10.10.10.20 | 10.10.10.24 | 25.25.25.4 | 50.50.50.0 | 50.50.50.4 | 
            50.50.50.8 | 50.50.50.12
        
        AREA 1
            10.10.10.28
    NAT|PAT Network. mask 255.255.255.0
          177.77.77.0 
    EIGRP Network. mask 255.255.255.252
          25.25.25.0
# Количество оборудования для настроек cisco
    Laptop – 3 
    (+ 3 console)

# Общее описание сети
  ```Создание с нуля сетевой инфраструктуры для работоспособности банка с использованием оборудования cisco.```

    Было создано 6 сетей с использованием OSPF - Это Front-Office, Back-Office ( + IT ), Security-Operator, Currency, Market, Tech-Support. 

    1 сеть на EIGRP - Это Application processing

    В сети Front-Office имеется VoIP и в сети Tech-Support. Они могут общаться по айпи телефонии

    Использован Router (R-NEW-DHCP) как DHCP-server, он выдаёт всем IP кроме сети в EIGRP, т.к там Static IP

    Используется SSH подключение ко всем Switch, на Router SSH только у R-NEW-DHCP. Так же для доступа по SSH создан User: admin, с паролем admin

    Один ABR-Router для связи с другой AREA OSPF

    Один ASBR-Router для связи EIGRP, и так же настроен Redistribution

    Добавлен Failover Router, для отказоустойчивости

    Есть Сервер который находится за NAT|PAT, хранящий резервные копии данных

    Добавлено 3 Сервера: 1 – Клиент Сервер (Внутренний интерфейс банка, управление клиентами), 2 – Фин Сервер (Бухгалтерия и Финансовые Операции), 3 – Запись Сервер (Сервер Видеонаблюдения)
