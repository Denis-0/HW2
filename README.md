# HW2
Описание/Пошаговая инструкция выполнения домашнего задания:
• сделать в GCE инстанс с Ubuntu 20.04 или развернуть докер любым удобным способом
--сделал инстанс виртуальной машины на Яндекс облаке
--установил PostgreSQL14
![image](https://user-images.githubusercontent.com/45406197/178510509-aa106968-7e24-4122-b2a0-607fdcf95074.png)
![image](https://user-images.githubusercontent.com/45406197/178511215-1e0f6fef-8cc8-4973-b962-cde37dc8cef8.png)
• поставить на нем Docker Engine
--установил докер 
--curl -fsSL https://get.docker.com -o get-docker.sh
--sudo sh get-docker.sh
![image](https://user-images.githubusercontent.com/45406197/178511057-af27bcb6-ce04-4581-86a7-309a4f375881.png)
• сделать каталог /var/lib/postgres
--mkdir /var/lib/postgres
• развернуть контейнер с PostgreSQL 14 смонтировав в него /var/lib/postgres
--sudo docker run --name pg-docker --network pg-net -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
![image](https://user-images.githubusercontent.com/45406197/178511381-bdcc6ed8-4c08-42ea-af23-07c2a2f5587e.png)
• развернуть контейнер с клиентом postgres

• подключится из контейнера с клиентом к контейнеру с сервером и сделать
таблицу с парой строк
sudo docker ps -a
--подключился
sudo docker run --name pg-server --network pg-net -e POSTGRES_PASSWORD=postgres -d -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
sudo docker run -it --rm --network pg-net --name pg-client postgres:14 psql -h pg-server -U postgres
--CREATE DATABASE test;
--CREATE TABLE test (number int, amount int);
--INSERT INTO test(number) VALUES (100);
--INSERT INTO test(amount) VALUES (300);
![image](https://user-images.githubusercontent.com/45406197/178511524-0435c774-e112-4d4f-a209-e1f542784b4c.png)

• подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов GCP/места установки докера

• удалить контейнер с сервером
--sudo docker stop
![image](https://user-images.githubusercontent.com/45406197/178511817-e31c4c7c-cb86-4e59-ba73-9afe3fce1029.png)

• создать его заново

• подключится снова из контейнера с клиентом к контейнеру с сервером
sudo docker run --name pg-server --network pg-net -e POSTGRES_PASSWORD=postgres -d -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
sudo docker run -it --rm --network pg-net --name pg-client postgres:14 psql -h pg-server -U postgres
• проверить, что данные остались на месте
данные на месте
![image](https://user-images.githubusercontent.com/45406197/178511948-1db96ac0-4dbe-4379-9fb9-27d3ff847863.png)
select * from test;
