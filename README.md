# Домашнее задание к занятию "`12.4 SQL.Часть 2`" - `Овчинников Дмитрий`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

    фамилия и имя сотрудника из этого магазина;
    город нахождения магазина;
    количество пользователей, закреплённых в этом магазине.

select

s.store_id, count(c.customer_id ) as "Количество пользователей", s2.first_name, s2.last_name, c2.city

from

store s

join customer c on c.store_id = s.store_id

join staff s2 on s2.store_id = s.store_id

join address a on a.address_id =s.address_id

join city c2 on c2.city_id =a.city_id

group by s.store_id, s2.first_name, s2.last_name, c2.city

having

count(c.customer_id) > 300

![sakila1](https://github.com/dmitri13/12.4/blob/main/img/sakila1.png)

---

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

select count(`length`) film_id 

from film f 

where `length` > (select AVG(`length`) from film)

![sakila2](https://github.com/dmitri13/12.4/blob/main/img/sakila2.png)
---

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

SELECT SUM(p.amount) AS 'highest payment',

DATE_FORMAT(p.payment_date, '%Y-%M') AS 'date',

COUNT(r.rental_id) AS 'number of leases'

FROM payment p

LEFT JOIN rental r ON r.rental_id = p.rental_id

GROUP BY DATE_FORMAT(p.payment_date, '%Y-%M')

ORDER BY 1 DESC

LIMIT 1;

![1234](https://github.com/dmitri13/12.4/blob/main/img/1234.png)

---
