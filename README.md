# BD_LAB6
Задание 1.
Создайте таблицу orders для хранения списка заказов:

id — идентификатор, целое положительное.
user_id — идентификатор пользователя, который оформил заказ. Целое положительное, NULL запрещен.
amount — стоимость заказа. Целое положительное число не более 1 млн. NULL запрещен, по умолчанию 0.
created — дата и время создания заказа. NULL запрещен.
state — статус заказа. Выбор из new, cancelled, in_progress, delivered, completed. Можно выбрать только один вариант. NULL запрещен. По умолчанию должен стоять new.
Добавьте 3 записи так, чтобы получалась таблица ниже


DROP TABLE if EXISTS orders;
CREATE TABLE orders (
id INT UNSIGNED PRIMARY KEY,
user_id INT UNSIGNED NOT NULL,
amount INT UNSIGNED NOT NULL DEFAULT 0 CHECK (amount <= 1000000),
created DATETIME NOT NULL,
state ENUM('new', 'cancelled', 'in_progress', 'delivered', 'completed') NOT NULL DEFAULT 'new');

INSERT INTO orders (id, user_id, amount, created, state) VALUES
(1, 56, 5400, '2018-02-01 17:46:59', 'new'),
(2, 90, 249, '2018-02-01 19:13:04', 'new'),
(3, 78, 2200, '2018-02-01 22:43:09', 'new');



Задание 2.
Создайте таблицу users для хранения списка пользователей сайта:

id — идентификатор, целое положительное.
first_name — имя, строка до 20 символов. NULL запрещен.
last_name — фамилия, строка до 20 символов. NULL запрещен.
patronymic — отчество, строка до 20 символов. NULL запрещен, по умолчанию пустая строка.
is_active — отметка об активности пользователя. Логическое поле, по умолчанию TRUE.
is_superuser — отметка администратора. Логическое поле, по умолчанию FALSE.
Добавьте 3 записи так, чтобы получалась таблица ниже:


DROP TABLE if EXISTS users;
CREATE TABLE users (
id INT UNSIGNED PRIMARY KEY,
first_name VARCHAR(20) NOT NULL,
last_name VARCHAR(20) NOT NULL,
patronymic VARCHAR(20) NOT NULL DEFAULT '',
is_active BOOLEAN NOT NULL DEFAULT TRUE,
is_superuser BOOLEAN NOT NULL DEFAULT FALSE);

INSERT INTO users (id, first_name, last_name, patronymic, is_active, is_superuser) VALUES
(1, 'Дмитрий', 'Иванов', '', TRUE, FALSE),
(2, 'Анатолий', 'Белый', 'Сергеевич', TRUE, TRUE),
(3, 'Андрей', 'Крючков', '', FALSE, FALSE);



Задание 3.
Создайте таблицу products для хранения товаров в интернет магазине:

id — идентификатор, целое положительное.
category_id — категория, целое положительное. Может принимать NULL. По умолчанию NULL.
name — название, строка до 100 символов. NULL запрещен.
count — количество, целое положительное до 255. NULL запрещен, по умолчанию 0.
price — цена типа DECIMAL с 10 знаками, 2 из которых выделены для копеек. NULL запрещен, по умолчанию 0.00.
Добавьте 3 записи так, чтобы получалась таблица ниже:


DROP TABLE if EXISTS products;
CREATE TABLE products (
id INT UNSIGNED PRIMARY KEY,
category_id INT UNSIGNED NULL DEFAULT NULL,
name VARCHAR(100) NOT NULL,
count TINYINT UNSIGNED NOT NULL DEFAULT 0,
price DECIMAL(10, 2) NOT NULL DEFAULT 0.00);

INSERT INTO products (id, category_id, name, count, price) VALUES
(1, 1, 'Кружка', 5, 45.90),
(2, 17, 'Фломастеры', 0, 78.00),
(3, NULL, 'Сникерс', 12, 50.30);
