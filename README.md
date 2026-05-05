2.1. Tạo database
CREATE DATABASE ecommerce_exam_db
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
USE ecommerce_exam_db;

2.2. Bảng roles
CREATE TABLE roles (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(50) NOT NULL UNIQUE
);

2.3. Bảng users
CREATE TABLE users (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(100) NOT NULL UNIQUE,
password VARCHAR(255) NOT NULL,
full_name VARCHAR(150),
enabled BOOLEAN DEFAULT TRUE
);

2.4. Bảng user_roles
CREATE TABLE user_roles (
user_id BIGINT NOT NULL,
role_id BIGINT NOT NULL,
PRIMARY KEY (user_id, role_id),
CONSTRAINT fk_user_role_user
FOREIGN KEY (user_id) REFERENCES users(id),
CONSTRAINT fk_user_role_role
FOREIGN KEY (role_id) REFERENCES roles(id)
);

2.5. Bảng categories
CREATE TABLE categories (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(100) NOT NULL
);

2.6. Bảng products
CREATE TABLE products (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(150) NOT NULL,
price DOUBLE NOT NULL,
quantity INT NOT NULL,
description VARCHAR(500),
image_url VARCHAR(255),

category_id BIGINT,
CONSTRAINT fk_product_category
FOREIGN KEY (category_id) REFERENCES categories(id)
);

3. Dữ liệu mẫu
INSERT INTO roles(name) VALUES
('ROLE_ADMIN'),
('ROLE_USER');
INSERT INTO users(username, password, full_name, enabled) VALUES
('admin', '$2a$10$eC5cloLkWLlqlw5WWxZb..AXPIBheQWaIE2YgMyuU7zUKzrfbzYie',
'System Administrator', true),
('user', '$2a$10$eC5cloLkWLlqlw5WWxZb..AXPIBheQWaIE2YgMyuU7zUKzrfbzYie', 'Normal
User', true);
INSERT INTO user_roles(user_id, role_id) VALUES
(1, 1),
(2, 2);
INSERT INTO categories(name) VALUES
('Laptop'),
('Smartphone'),
('Accessories');
INSERT INTO products(name, price, quantity, description, image_url, category_id) VALUES
('Dell Inspiron 15', 15500000, 10, 'Laptop học tập và văn phòng',
'https://via.placeholder.com/150', 1),
('MacBook Air M2', 24500000, 5, 'Laptop mỏng nhẹ cho lập trình viên',
'https://via.placeholder.com/150', 1),
('iPhone 15', 21000000, 8, 'Điện thoại Apple iPhone 15', 'https://via.placeholder.com/150', 2),
('Samsung Galaxy S24', 19900000, 12, 'Điện thoại Samsung cao cấp',
'https://via.placeholder.com/150', 2),
('Logitech Mouse M331', 350000, 30, 'Chuột không dây Logitech',
'https://via.placeholder.com/150', 3);
