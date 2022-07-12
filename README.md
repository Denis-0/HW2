# HW2
Описание/Пошаговая инструкция выполнения домашнего задания:
• сделать в GCE инстанс с Ubuntu 20.04 или развернуть докер любым удобным способом
--сделал инстанс виртуальной машины на Яндекс облаке
--установил PostgreSQL14
• поставить на нем Docker Engine
--установил докер 
--curl -fsSL https://get.docker.com -o get-docker.sh
--sudo sh get-docker.sh
• сделать каталог /var/lib/postgres
--mkdir /var/lib/postgres
• развернуть контейнер с PostgreSQL 14 смонтировав в него /var/lib/postgres
--sudo docker run --name pg-docker --network pg-net -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
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
• подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов GCP/места установки докера

• удалить контейнер с сервером
sudo docker stop
• создать его заново

• подключится снова из контейнера с клиентом к контейнеру с сервером
sudo docker run --name pg-server --network pg-net -e POSTGRES_PASSWORD=postgres -d -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
sudo docker run -it --rm --network pg-net --name pg-client postgres:14 psql -h pg-server -U postgres
• проверить, что данные остались на месте
