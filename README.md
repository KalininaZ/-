20.02.25

Удалите из таблицы cars все корейские (country = "KR") автомобили, а также все автомобили мощностью (power) меньше 80 лс.

delete from cars where country = 'KR' or power<80

Удалите из таблицы cars все японские автомобили мощностью менее 80 и более 130 лс. (включая крайние значения.

delete from cars where country = "JP" and (power <= 80 or power >= 130)


5.04.25

Создайте таблицу articles для хранения данных о статьях. В таблице должны быть следующие поля:
id — идентификатор, целое положительное, NULL запрещен
name — название статьи, строка до 80 символов.text — текст статьи.
state — статус статьи. Поле из 3 вариантов: draft (черновик), correction (корректура), public (опубликована).Добавьте 3 записи так, чтобы получалась таблица ниже:

![image](https://github.com/user-attachments/assets/20d1fff3-065e-4cc8-9fed-4c44d1df7dd0)

Create table articles (
id int unsigned not null,
name varchar (80),
text text,
state enum('draft', 'correction', 'public')
);
insert into articles (id, name, text, state)
VALUES
(1, 'Новое в Python 3.6', '', 'draft'),
(2, 'Оптимизация SQL запросов', 'При больших объемах данных ...', 'correction'),
(3, 'Транзакции в MySQL', 'По долгу службы мне приходится ...', 'public')

Когда можно выбрать 1 вариант - используем ENUM

когда можно выбрать несколько вариантов - используем SET

-----

Создайте таблицу rooms для хранения номеров в отеле:

id — идентификатор, целое положительное.
number — номер комнаты, целое положительное. Всего в отеле 107 комнат. NULL запрещен.
beds — количество спальных мест. Выбор из 1+1, 2+1, 2+2. Можно выбрать только один вариант. NULL запрещен.
additional — дополнительные удобства в номере. Можно выбрать несколько вариантов из списка: conditioner, bar, fridge и wifi.
Добавьте 3 записи так, чтобы получалась таблица ниже:

![image](https://github.com/user-attachments/assets/f6e1410f-a45f-4774-a6b8-2d5530bdf5ba)

create table rooms (
id int unsigned not null,
number tinyint unsigned not null,
beds enum('1+1','2+1','2+2') not null,
additional set('conditioner','bar','fridge','wifi')
);
insert into rooms (id,number,beds,additional)
values
(1,10,'1+1','conditioner,bar,wifi'),
(2,12,'2+1',''),
(3,24,'2+2','fridge,bar,wifi')

---

Выберите из таблицы products название, цену и страны всех товаров из России и Белоруссии (в поле country обязательно должна присутствовать или Россия, или Белоруссия).
Выбирайте только товары, у которых задана категория.
Данные отсортируйте по цене в обратном порядке.

Поле country относится к типу SET('RU', 'UA', 'BY', 'KZ') NOT NULL.

![image](https://github.com/user-attachments/assets/a282278b-eed1-48d7-99de-08c5d3f41d33)

22.05.25

Создайте таблицу users с со следующими полями:

id — идентификатор, целое положительное, первичный ключ без автоинкремента, NULL запрещен.
first_name — имя пользователя, строка до 50 символов.
last_name — фамилия пользователя, строка до 50 символов.
birthday — дата рождения. Пользователь может не указать день рождения и тогда в поле нужно хранить NULL.
Добавьте 3 записи так, чтобы получалась таблица ниже:

![image](https://github.com/user-attachments/assets/f9cbc536-dde2-4f76-a9a8-1a988c585472)

CREATE TABLE users (
id INT(10)UNSIGNED NOT NULL PRIMARY KEY,
first_name VARCHAR (50) NULL,
last_name VARCHAR (50) NULL,
birthday DATE NULL );
INSERT INTO users (id, first_name, last_name, birthday)
VALUES (1,'Дмитрий','Иванов',NULL),
(2,'Анатолий','Белый',NULL),
(3,'Денис','Давыдов','1995-09-08');

---

Создайте таблицу orders с автоинкрементальным первичным ключом id, полем state для хранения статуса заказа и полем amount для хранения суммы заказа. Статус заказа умещается в строку длиной 8 символов, а сумма заказа является денежным типом до 1 млн. с двумя знаками после десятичной точки.

Добавьте 3 записи так, чтобы получалась таблица ниже:

![image](https://github.com/user-attachments/assets/1bfb8144-9ea4-49ec-ac68-11c4513a2d27)

create table orders (
id int unsigned not null primary key auto_increment,
state varchar (8),
amount decimal (8,2)
);
insert into orders (state, amount)
values ('new', 1000.50),
('new', 3400.10),
('delivery', 7300.00)







