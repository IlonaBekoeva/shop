………создание и заполнение таблицы продуктов…………………………………………………………………………………………………………………….</br>
CREATE TABLE `products` (</br>
  `id` int NOT NULL AUTO_INCREMENT,</br>
  `name` varchar(45) NOT NULL,</br>
  `price` decimal(5,2) NOT NULL,</br>
  PRIMARY KEY (`id`)</br>
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;</br>

INSERT INTO `products` VALUES (1,'мороженка',90.00),(2,'тортик',500.00),(3,'чипсики',120.00),(4,'печеньки',80.00),(5,'булочка',40.00);</br>

………создание и заполнение таблицы заказов…………………………………………………………………………………………………………………….</br>
CREATE TABLE `orders` (</br>
  `id` int NOT NULL AUTO_INCREMENT,</br>
  `FIO` varchar(45) NOT NULL,</br>
  `address` varchar(45) NOT NULL,</br>
  `courier_id` int NOT NULL,</br>
  PRIMARY KEY (`id`),</br>
  KEY `orders_couriers_idx` (`courier_id`),</br>
  CONSTRAINT `orders_couriers` FOREIGN KEY (`courier_id`) REFERENCES `couriers` (`id`)</br>
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;</br>
</br>
INSERT INTO `orders` VALUES (1,'Илона','Калоева',1),(2,'ВерОника','Киевская',2),(3,'Стас','Ватутина',3),(4,'Роза','Шмулевича',1),(5,'Олина','Калинина',2),(11,'Яна','Гугкаева',3),(12,'Яна','Гугкаева',3),(13,'Яна','Гугкаева',3),(14,'Яна','Гугкаева',3),(15,'Яна','Гугкаева',3),(16,'Яна','Гугкаева',3),(17,'Яна','Гугкаева',3),(18,'Яна','Гугкаева',3),(19,'Яна','Гугкаева',3);</br>
</br>
………создание и заполнение таблицы курьеров…………………………………………………………………………………………………………………….</br>
CREATE TABLE `couriers` (</br>
  `id` int NOT NULL AUTO_INCREMENT,</br>
  `name` varchar(45) NOT NULL,</br>
  `phone_num` varchar(20) NOT NULL,</br>
  `car_num` varchar(20) NOT NULL,</br>
  PRIMARY KEY (`id`)</br>
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;</br>
</br>
INSERT INTO `couriers` VALUES (1,'Сос','+79708675436','Audi'),(2,'Вова','+79452341563','BMW'),(3,'Эрик','+79605897546','Bentley');</br>
</br>
………создание и заполнение таблицы связи…………………………………………………………………………………………………………………….</br>
CREATE TABLE `order_items` (</br>
  `id` int NOT NULL AUTO_INCREMENT,</br>
  `product_id` int NOT NULL,</br>
  `order_id` int NOT NULL,</br>
  `amount` int NOT NULL,</br>
  PRIMARY KEY (`id`),</br>
  KEY `products_order_items_idx` (`product_id`),</br>
  KEY `orders_order_items_idx` (`order_id`),</br>
  CONSTRAINT `orders_order_items` FOREIGN KEY (`order_id`) REFERENCES `orders` (`id`),</br>
  CONSTRAINT `products_order_items` FOREIGN KEY (`product_id`) REFERENCES `products` (`id`)</br>
) ENGINE=InnoDB AUTO_INCREMENT=22 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;</br>
</br>
INSERT INTO `order_items` VALUES (1,1,1,3),(2,2,2,2),(3,3,3,3),(4,4,4,4),(5,5,5,5),(6,2,3,5),(7,3,1,2),(8,2,3,5),(9,3,1,2),(10,2,3,5),(11,3,1,2),(12,2,3,5),(13,3,1,2),(14,2,3,5),(15,3,1,2),(16,2,3,5),(17,3,1,2),(18,2,3,5),(19,3,1,2),(20,2,3,5),(21,3,1,2);</br>
</br>
………запрос №1 …………………………………………………………………………………………………………………….</br>
SELECT o.FIO, o.address, p.name, oi.amount, p.price*oi.amount as Sum, c.name </br>
</br>
FROM shop.orders as o</br>
</br>
join shop.couriers as c</br>
on o.courier_id = c.id</br>
</br>
join shop.order_items as oi</br>
on o.id = oi.order_id</br>
</br>
join shop.products as p</br>
on p.id = oi.product_id</br>
</br>
where o.id = 5;</br>
</br>
………запрос №2 …………………………………………………………………………………………………………………….</br>
INSERT INTO shop.orders (FIO, address, courier_id) VALUES ('Яна', 'Гугкаева', '3');</br>
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('2', '3', '5');</br>
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('3', '1', '2');</br>
</br>
………запрос №3 …………………………………………………………………………………………………………………….</br>
SELECT  x.FIO, x.address, p.name, oi.amount, p.price*oi.amount as Sum, c.name </br>
FROM shop.orders as x</br>
</br>
join shop.couriers as c</br>
on x.courier_id = c.id</br>
</br>
join shop.order_items as oi</br>
on x.id = oi.order_id</br>
</br>
join shop.products as p</br>
on p.id = oi.product_id</br>
</br>
where x.courier_id = 1</br>
</br>
………запрос №4 …………………………………………………………………………………………………………………….</br>
UPDATE shop.order_items </br>
SET amount = '3' </br>
WHERE (id = '1');</br>
