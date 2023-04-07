………создание и заполнение таблицы продуктов…………………………………………………………………………………………………………………….
CREATE TABLE `products` (
  `id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `price` decimal(5,2) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

INSERT INTO `products` VALUES (1,'мороженка',90.00),(2,'тортик',500.00),(3,'чипсики',120.00),(4,'печеньки',80.00),(5,'булочка',40.00);

………создание и заполнение таблицы заказов…………………………………………………………………………………………………………………….
CREATE TABLE `orders` (
  `id` int NOT NULL AUTO_INCREMENT,
  `FIO` varchar(45) NOT NULL,
  `address` varchar(45) NOT NULL,
  `courier_id` int NOT NULL,
  PRIMARY KEY (`id`),
  KEY `orders_couriers_idx` (`courier_id`),
  CONSTRAINT `orders_couriers` FOREIGN KEY (`courier_id`) REFERENCES `couriers` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

INSERT INTO `orders` VALUES (1,'Илона','Калоева',1),(2,'ВерОника','Киевская',2),(3,'Стас','Ватутина',3),(4,'Роза','Шмулевича',1),(5,'Олина','Калинина',2),(11,'Яна','Гугкаева',3),(12,'Яна','Гугкаева',3),(13,'Яна','Гугкаева',3),(14,'Яна','Гугкаева',3),(15,'Яна','Гугкаева',3),(16,'Яна','Гугкаева',3),(17,'Яна','Гугкаева',3),(18,'Яна','Гугкаева',3),(19,'Яна','Гугкаева',3);

………создание и заполнение таблицы курьеров…………………………………………………………………………………………………………………….
CREATE TABLE `couriers` (
  `id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `phone_num` varchar(20) NOT NULL,
  `car_num` varchar(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

INSERT INTO `couriers` VALUES (1,'Сос','+79708675436','Audi'),(2,'Вова','+79452341563','BMW'),(3,'Эрик','+79605897546','Bentley');

………создание и заполнение таблицы связи…………………………………………………………………………………………………………………….
CREATE TABLE `order_items` (
  `id` int NOT NULL AUTO_INCREMENT,
  `product_id` int NOT NULL,
  `order_id` int NOT NULL,
  `amount` int NOT NULL,
  PRIMARY KEY (`id`),
  KEY `products_order_items_idx` (`product_id`),
  KEY `orders_order_items_idx` (`order_id`),
  CONSTRAINT `orders_order_items` FOREIGN KEY (`order_id`) REFERENCES `orders` (`id`),
  CONSTRAINT `products_order_items` FOREIGN KEY (`product_id`) REFERENCES `products` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=22 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

INSERT INTO `order_items` VALUES (1,1,1,3),(2,2,2,2),(3,3,3,3),(4,4,4,4),(5,5,5,5),(6,2,3,5),(7,3,1,2),(8,2,3,5),(9,3,1,2),(10,2,3,5),(11,3,1,2),(12,2,3,5),(13,3,1,2),(14,2,3,5),(15,3,1,2),(16,2,3,5),(17,3,1,2),(18,2,3,5),(19,3,1,2),(20,2,3,5),(21,3,1,2);

………запрос №1 …………………………………………………………………………………………………………………….
SELECT o.FIO, o.address, p.name, oi.amount, p.price*oi.amount as Sum, c.name 

FROM shop.orders as o

join shop.couriers as c
on o.courier_id = c.id

join shop.order_items as oi
on o.id = oi.order_id

join shop.products as p
on p.id = oi.product_id

where o.id = 5;

………запрос №2 …………………………………………………………………………………………………………………….
INSERT INTO shop.orders (FIO, address, courier_id) VALUES ('Яна', 'Гугкаева', '3');
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('2', '3', '5');
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('3', '1', '2');

………запрос №3 …………………………………………………………………………………………………………………….
SELECT  x.FIO, x.address, p.name, oi.amount, p.price*oi.amount as Sum, c.name 
FROM shop.orders as x

join shop.couriers as c
on x.courier_id = c.id

join shop.order_items as oi
on x.id = oi.order_id

join shop.products as p
on p.id = oi.product_id

where x.courier_id = 1

………запрос №4 …………………………………………………………………………………………………………………….
UPDATE shop.order_items 
SET amount = '3' 
WHERE (id = '1');
