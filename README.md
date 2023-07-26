# Домашнее задание к занятию "`SQL. Часть 1`"
# `Островский Евгений`


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

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```SQL
SELECT DISTINCT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```

![1](https://github.com/joos-net/SQL_1/blob/main/img/1.png)

---

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```SQL
SELECT amount, payment_date FROM payment WHERE amount > 10 AND payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59';
```

![2](https://github.com/joos-net/SQL_1/blob/main/img/2.png)

---

### Задание 3

Получите последние пять аренд фильмов.

```SQL
SELECT rental_id, rental_date, last_update  FROM rental ORDER BY rental_date DESC, rental_id DESC LIMIT 5;
```

![3](https://github.com/joos-net/SQL_1/blob/main/img/3.png)

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

```SQL
SELECT LOWER(first_name), LOWER(last_name), REPLACE(LOWER(first_name), 'll', 'pp')as ll_TO_pp FROM customer WHERE first_name LIKE 'Kelly' OR  first_name  LIKE 'Willie';
```

![4](https://github.com/joos-net/SQL_1/blob/main/img/4.png)

---
## Дополнительные задания (со звездочкой*)

Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

### Задание 5

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

```SQL
SELECT email, SUBSTRING_INDEX(email,'@',1) AS BEFORE_AT_SIGN, SUBSTR(email, INSTR(email, '@') + 1) AS AFTER_AT_SIGN FROM customer;
```

![5](https://github.com/joos-net/SQL_1/blob/main/img/5.png)

### Задание 6

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

```SQL
SELECT email, CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email,'@',1),1)), LCASE(SUBSTRING(SUBSTRING_INDEX(email,'@',1), 2))) AS BEFORE_AT_SIGN, CONCAT(UPPER(LEFT(SUBSTR(email, INSTR(email, '@') + 1),1)), LCASE(SUBSTRING(SUBSTR(email, INSTR(email, '@') + 1), 2))) AS AFTER_AT_SIGN FROM customer;
```

![6](https://github.com/joos-net/SQL_1/blob/main/img/6.png)
