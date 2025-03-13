# Лекция 1: Внутренняя Архитектура PostgreSQL
## Ход выполнения задания
1. Развернуть ВМ (Linux) с PostgreSQL. В моем случае на докере был развернут контейнер с 17 версией PG при помощи docker-compose
Код:
```yaml
services:
  postgres:
    image: postgres:17.4
    environment:
      POSTGRES_DB: "lesson1"
      POSTGRES_USER: "<USER>"
      POSTGRES_PASSWORD: "<PASSWORD>"
      PGDATA: "<PATH>"
    volumes:
      - lesson1-data:<PATH>
    ports:
      - "5432:5432"
    networks:
      - "net"

networks:
  net:
    driver: bridge

volumes:
  lesson1-data:
```
Скриншот
<img width="960" alt="изображение" src="https://github.com/user-attachments/assets/529075ac-2d6b-404c-9609-829f66e8afa9" />

2. Залить Тайские перевозки в минимальном варианте
С помощью `psql` команды была создана база данных и была залита схема с данными
```sh
psql -h localhost -p 5432 -b thai < thai.sql
```
3. Посчитать количество поездок - select count(*) from book.tickets:
Ответ: 5185505 записей
4. После все операций контейнер остановлен
