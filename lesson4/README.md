# Лекция 4: Блокировки
## Результат задания
Я создал таблицы `accounts(id integer, amount numeric)`, и заполнил ее следующими данными: `(1, 1000.00), (2, 2000.00)`
Далее в 2 терминалах я открыл соединения к БД.
В 1 терминале начал писать следующий запрос:
```sql
begin;
update accounts set amount = amount + 1 where id = 1;
```
Во 2 терминале не коммитя изменения 1 также начал делать запрос:
```sql
begin;
update accounts set amount = amount + 1 where id = 2;
```
Потом в 1 и 2 терминале я запустил следующие запросы:
Терминал 1
```sql
update accounts set amount = amount + 1 where id = 2;
```
Терминал 2
```sql
update accounts set amount = amount + 1 where id = 1;
```
В итоге я словил deadlock
<img width="624" alt="изображение" src="https://github.com/user-attachments/assets/710c2943-5ac8-4ad0-9f62-17a0ac36bad8" />

Скриншот логов самого докер-контейнера
<img width="1113" alt="изображение" src="https://github.com/user-attachments/assets/eda5693a-7572-4a42-895a-976ad12dd2c5" />

