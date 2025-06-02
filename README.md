# Лабораторная работа 4.

## Шаги работы:

1. Устанавливаем ubuntu live server.
![](screenshots/1.png)
![](screenshots/2.png)
![](screenshots/3.png)
![](screenshots/4.png)
![](screenshots/5.png)
2. Создаем Dockerfile.
```
FROM ubuntu:latest
RUN apt-get update && apt-get install -y libaa-bin
CMD ["aafire"]
```
3. Собираем образ.
```
docker build -t aafire .
```
4. Запускаем контейнер.
```
docker run -it aafire
```
![](screenshots/6.png)
5. Добавляем в Dockerfile установку ping.
```
FROM ubuntu:latest
RUN apt-get update && apt-get install -y libaa-bin iputils-ping
CMD ["aafire"]
```
6. Пересобираем образ.
```
docker build -t aafire .
```
7. Запускаем контейнеры.
```
docker run -dit --name con1 aafire
docker run -dit --name con2 aafire
```
8. Проверяем работают ли контейнеры.
![](screenshots/7.png)
9. Создаем сеть.
```
docker network create myNetwork
```
10. Подключаем контейнеры к сети.
```
docker network connect myNetwork con1
docker network connect myNetwork con2
```
11. Смотрим настройки созданной сети.
```
docker network inspect myNetwork
```
![](screenshots/8.png)
12. Подключаемся к контейнерам и проверяем соединение между ними.
```
docker exec -it con1 /bin/bash
ping con2
```
```
docker exec -it con2 /bin/bash
ping con1
```
![](screenshots/9.png)
![](screenshots/10.png)
