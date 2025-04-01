# Лекция 7:
## Ответы на вопросы:
1. Развернуть ВМ (Linux) с PostgreSQL
2. Залить Тайские перевозки
<img width="539" alt="изображение" src="https://github.com/user-attachments/assets/c0f87487-0fd8-4860-9a7b-7b9c1880a84d" />

3. Проверить скорость выполнения сложного запроса
Данный запрос был выполнен за 20 секунд
Запрос:
```sql
WITH all_place AS (
    SELECT count(s.id) as all_place, s.fkbus as fkbus
    FROM book.seat s
    group by s.fkbus
),
order_place AS (
    SELECT count(t.id) as order_place, t.fkride
    FROM book.tickets t
    group by t.fkride
)
SELECT r.id, r.startdate as depart_date, bs.city || ', ' || bs.name as busstation,  
      t.order_place, st.all_place
FROM book.ride r
JOIN book.schedule as s
      on r.fkschedule = s.id
JOIN book.busroute br
      on s.fkroute = br.id
JOIN book.busstation bs
      on br.fkbusstationfrom = bs.id
JOIN order_place t
      on t.fkride = r.id
JOIN all_place st
      on r.fkbus = st.fkbus
GROUP BY r.id, r.startdate, bs.city || ', ' || bs.name, t.order_place,st.all_place
ORDER BY r.startdate
limit 10;
```
Результат

<img width="781" alt="изображение" src="https://github.com/user-attachments/assets/bebe3ac1-7ed0-498d-88f7-8542aa143a98" />

EXPLAIN запроса

<img width="731" alt="изображение" src="https://github.com/user-attachments/assets/4794f2b5-76ee-4ffe-ac82-990786124801" />

4. Навесить индекс на внешние ключи
5. Проверить, помогли ли индексы на внешние ключи ускориться
Было навешены индексы 3 внешних ключа. В итоге выполнение запроса стало составлять 8 секунд. Однако explain никак не изменился

<img width="652" alt="изображение" src="https://github.com/user-attachments/assets/cbe85e7a-347e-4194-a5f5-1ea6e2091252" />

![Uploading изображение.png…]()


