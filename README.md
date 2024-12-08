## Введение
Данный проект использует docker compose для развертывания Wireguard с дополнительными компонентами, такими как Nginx, клиент peer, шлюз, а также конфигурацию программного межсетевого экрана iptables. Конфигурация включает в себя блокировку всего входящего трафика на nginx за исключением входящего трафика по 80 порту. Далее будет описаны все составляющие работы и настройка правил в iptables.



## Составляющие работы 
# контейнеры 
**peer** - клиент 
**gateway** - контейнер для сетевой диагностики с утилитой tcpdump 
**wg-easy** - интерфейс для управления wireguard
**nginx** - веб-сервер

# используемые сети
**net_A** - использован для клиента и шлюза
**net_B** - используется для шлюза и wg-easy
**net_C**  - используется для wg-easy и nginx

## IP-адреса каждого контейнера 

**peer** - 10.1.0.70
**gateway** - 10.1.0.2; 10.2.0.2
**wg-easy** - 10.3.0.3; 10.2.0.3
**nginx** - 10.3.0.10

## Сервисы и порты

| Сервис   | Порт (Хост:Контейнер)  | Протокол |
|----------|------------------------|----------|
| wg-easy  | 51820:51820            | udp      |
| wg-easy  | 53000:51821            | tcp      |

## Подготовка к работе 
Для начала работы с этим репозиторием необходимо:
'install docker' - установка Docker 
'docker compose up -d' - запуск Docker Compose 
'docker ps -a' - проверка работоспособности всех контейнеров 



## Дополнительные команды 
'ping xx.xx.xx.xx' - проверка доступности сетевых узлов ( отправка пакетов ICMP данных)
'curl xx.xx.xx.xx' - передача данных с сетевыми протоколами 
'curl xx.xx.xx.xx:port' - передача данных с сетевыми протоколами (учитывается порт)
'docker exec -it name_container /bin/bash' - подключение и работа от контейнера
'apt install iptables' - установка утилиты iptables
'iptables -L -n' - вывод установленных правил iptables  

![iptables nginx](C:\Users\Sofy\Pictures\nginx-iptables)
![iptables wg-easy](C:\Users\Sofy\Pictures\wgeasy-iptables)
![iptables gateway](C:\Users\Sofy\Pictures\gateway-iptables)
![peer result](C:\Users\Sofy\Pictures\peer-result)



#   i p t a b l e s  
 