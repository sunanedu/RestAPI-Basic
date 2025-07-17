# RestAPI-Basic

สวัสดีครับ! ทุกคนผมชื่อครูวิท (sunan.edu@gmail.com) วันนี้ผมจะมาสอนการออกแบบระบบ RestAPI ด้วย PHP PDO รองรับ Endpoint พื้นฐาน GET POST PUT DELETE (CRUD) รองรับ JWT Token แบบง่ายๆ สำหรับมือใหม่

# 🎏 สรุปภาพรวมของเนื้อหานี้

 "เจ้า API ที่เรากำลังจะสร้างกันเนี่ย มันคืออะไร? เรียนแล้วจะเอาไปทำอะไรได้บ้าง? แล้วใครที่ควรจะเรียนรู้เรื่องนี้?"

### 📕 ถ้าเรียนรู้เรื่องนี้ จะมีประโยชน์อย่างไร? เรียนแล้วได้อะไร?

การสร้าง API ได้ ไม่ใช่แค่การเขียนโค้ดเป็นนะครับ แต่มันคือการสร้าง **"สมอง"** ให้กับแอปพลิเคชันสมัยใหม่เลยทีเดียว ลองนึกภาพตามนะครับ

* **สร้าง Back-end ที่รองรับได้ทุกอย่าง:** สมัยก่อนเราอาจจะเขียนเว็บที่โค้ดหน้าบ้าน (HTML) กับหลังบ้าน (PHP) ปนกันไปหมด แต่พอเราสร้าง API เป็น "สมอง" แยกออกมา เราสามารถสร้าง "หน้าตา" (Front-end) กี่แบบก็ได้มาเชื่อมต่อกับสมองอันนี้ ไม่ว่าจะเป็น:

  * เว็บไซต์ (ทำด้วย React, Vue, Angular)

  * แอปพลิเคชันมือถือ (iOS, Android)

  * โปรแกรมบนคอมพิวเตอร์

  * หรือแม้กระทั่งให้ระบบอื่นๆ มาคุยกับเรา

* **เป็นทักษะที่เป็นที่ต้องการสูงมาก:** ในยุคนี้ แทบทุกบริษัทที่พัฒนาซอฟต์แวร์ต้องการคนทำ Back-end และ API ได้ครับ การที่คุณเข้าใจหลักการเหล่านี้ จะทำให้โปรไฟล์ของคุณโดดเด่นและเป็นที่ต้องการของตลาดแรงงานอย่างแน่นอน

* **เข้าใจสถาปัตยกรรมซอฟต์แวร์สมัยใหม่:** คุณจะไม่ได้เรียนแค่การเขียน PHP แต่คุณจะได้เรียนรู้ "หลักการออกแบบ" ที่เป็นหัวใจสำคัญ เช่น:

  * **Router:** การจัดการเส้นทางของแอปพลิเคชัน

  * **Controller:** การแบ่งโค้ดตามหน้าที่ความรับผิดชอบ

  * **Middleware:** การสร้างด่านตรวจเพื่อความปลอดภัย

  * **JWT:** การยืนยันตัวตนแบบไร้สถานะ (Stateless) ซึ่งหลักการเหล่านี้ สามารถนำไปปรับใช้กับภาษาหรือ Framework อื่นๆ ได้ทั้งหมดเลยครับ

* **ทำงานเป็นทีมได้ดีขึ้น:** แม้ว่าคุณจะเป็นสาย Front-end การเข้าใจว่า API ทำงานอย่างไร จะทำให้คุณสื่อสารกับทีม Back-end ได้ง่ายขึ้นมาก คุณจะรู้ว่าต้องขอข้อมูลแบบไหน และจะจัดการกับข้อมูลที่ได้รับมาอย่างไร

### เนื้อหานี้เหมาะกับใคร?

เนื้อหานี้ถูกออกแบบมาให้เป็นมิตรและเห็นภาพชัดเจน เหมาะสำหรับ:

* **นักพัฒนา PHP ที่อยากอัปเกรด:** สำหรับคนที่เคยทำเว็บด้วย PHP แบบเดิมๆ (เช่น ผสมโค้ดในไฟล์เดียว, ทำเว็บด้วย WordPress) และอยากจะก้าวเข้าสู่โลกของการพัฒนาแอปพลิเคชันสมัยใหม่ เนื้อหานี้คือประตูบานแรกที่ดีที่สุดครับ

* **นักศึกษาหรือผู้เริ่มต้น:** สำหรับน้องๆ ที่กำลังเรียนสายคอมพิวเตอร์ หรือเพิ่งเรียนจบ โปรเจคนี้เหมาะมากที่จะเป็นโปรเจคใส่พอร์ตฟอลิโอ เพราะมันแสดงให้เห็นว่าคุณเข้าใจหลักการทำงานของระบบที่ใช้งานจริง

* **นักพัฒนา Front-end ที่อยากรู้เรื่อง Back-end:** สำหรับคนที่ทำหน้าเว็บสวยๆ ด้วย React หรือ Vue แต่อยากเข้าใจว่า "ข้อมูลที่เอามาแสดงผลมันมาจากไหน?" "ระบบ Login ทำงานยังไง?" การเรียนรู้เรื่องนี้จะทำให้คุณเป็นนักพัฒนาที่ครบเครื่องมากขึ้น

* **คนที่อยากเข้าใจ "ภาพใหญ่":** สำหรับใครก็ตามที่อยากเข้าใจว่าเว็บแอปหรือแอปมือถือที่เราใช้กันทุกวันนี้มันมีโครงสร้างเบื้องหลังอย่างไร เนื้อหานี้จะทำให้คุณ "อ๋อ!" ขึ้นมาทันที

### ควรมีความรู้พื้นฐานอะไรมาก่อนบ้าง?

เพื่อให้การเรียนรู้เป็นไปอย่างราบรื่นและสนุกที่สุด ครูแนะนำว่าควรจะมีพื้นฐานเหล่านี้ติดตัวมาบ้างนะครับ

* **ความรู้ที่จำเป็น (ต้องมี):**

  * **PHP พื้นฐาน:** เข้าใจเรื่องตัวแปร, ฟังก์ชัน, `if/else`, การวนลูป (`for`, `foreach`) ไม่จำเป็นต้องเก่งมาก แต่ต้องเขียนเป็นครับ

  * **SQL พื้นฐาน:** สามารถเขียนคำสั่ง `SELECT`, `INSERT`, `UPDATE`, `DELETE` ได้ และเข้าใจแนวคิดของ `Primary Key` กับ `Foreign Key`

  * **ความเข้าใจเรื่องเว็บเบื้องต้น:** รู้ว่า HTML, CSS, JavaScript คืออะไรและทำหน้าที่อะไร

* **ความรู้ที่แนะนำ (ถ้ามีจะดีมาก แต่ไม่มีก็เรียนรู้ไปพร้อมกันได้):**

  * **OOP ใน PHP:** การเข้าใจเรื่อง `class`, `object`, `public`, `private`, `__construct` จะช่วยให้คุณเข้าใจโค้ดในส่วนของ Controller, Router ได้ง่ายขึ้นมาก เพราะมันคือการเขียนโปรแกรมเชิงวัตถุทั้งหมดเลย

  * **Command Line / Terminal:** สามารถใช้คำสั่งพื้นฐานอย่าง `cd` (เปลี่ยนโฟลเดอร์) และ `mkdir` (สร้างโฟลเดอร์) ได้

  * **Composer:** แค่รู้ว่ามันคือ "เครื่องมือช่วยติดตั้ง Library" ให้กับโปรเจค PHP ของเราก็เพียงพอแล้วครับ

ในคู่มือนี้ เราจะมาสร้าง REST API พื้นฐานด้วย PHP กันแบบจับมือทำทีละขั้นตอนเลยนะครับ ผมจะพยายามใช้คำพูดง่ายๆ เป็นกันเอง ให้เหมือนเรานั่งทำโปรเจคอยู่ข้างๆ กันเลย เป้าหมายของเราคือการสร้าง API ที่มีระบบจัดการผู้ใช้ (Users) พร้อมระบบสิทธิ์ (Permissions) ที่แข็งแรงและยืดหยุ่น โดยใช้เครื่องมือพื้นฐานที่นักพัฒนาเว็บคุ้นเคยกันดีครับ

## ขั้นตอนแรก: มาทำความเข้าใจภาพรวมกันก่อน

ก่อนที่เราจะเริ่มเขียนโค้ด เรามาดูกันก่อนว่าระบบที่เรากำลังจะสร้างมีหน้าตาและหลักการทำงานเป็นอย่างไร

### แผนผังความสัมพันธ์ของฐานข้อมูล (ER Diagram)

นี่คือแผนผังที่แสดงว่าข้อมูลแต่ละส่วนในระบบของเราเชื่อมโยงกันอย่างไร

```
[users] ----(1:N)---- [orders] ----(1:N)---- [order_items]
  |                     |                     |
  |                     |                     |
(1:N)                 (1:N)                 (1:N)
  |                     |                     |
[addresses]         [payments]            [reviews] ----(N:1)---- [products] ----(N:1)---- [categories]
```

จากแผนผังจะเห็นว่า:

* ผู้ใช้ 1 คน (`users`) สามารถมีได้หลายที่อยู่ (`addresses`) และหลายคำสั่งซื้อ (`orders`)

* คำสั่งซื้อ 1 รายการ (`orders`) สามารถมีได้หลายการจ่ายเงิน (`payments`) และมีสินค้าได้หลายชิ้น (`order_items`)

* สินค้า 1 ชิ้น (`products`) สามารถมีได้หลายรีวิว (`reviews`) และอยู่ใน 1 หมวดหมู่ (`categories`)

### การออกแบบสถาปัตยกรรมเว็บแอปพลิเคชัน (Front Controller) และวงจรชีวิตของคำขอ (Request Lifecycle)

ลองนึกภาพตามนะครับว่าเมื่อมีคนส่งคำขอ (Request) เข้ามาที่ API ของเรา มันเดินทางผ่านระบบของเราอย่างไร

**ตัวอย่าง:** มีคนส่งคำขอ `PUT /api/users/5` เพื่อ "แก้ไขข้อมูลผู้ใช้ที่มี ID เป็น 5"

1. **ประตูหน้า (`/public/.htaccess`):** คำขอทั้งหมดจะถูกส่งมาที่ประตูนี้ก่อนเลย `.htaccess` จะทำหน้าที่เหมือน รปภ. ที่ชี้ทางให้ทุกคำขอวิ่งไปที่ไฟล์ `index.php` เสมอ

2. **ผู้จัดการ (`/public/index.php`):** ไฟล์นี้คือ "ผู้จัดการ" ของระบบเราครับ มันจะเตรียมความพร้อมเบื้องต้น แล้วเรียก "สมองกล" ของเราซึ่งก็คือ **Router** ขึ้นมาทำงาน

3. **สมองกล (`/src/Core/Router.php`):** Router จะรับคำขอมาแล้วเปิด "สารบัญ" (`/src/routes.php`) เพื่อดูว่าเส้นทาง `/api/users/5` และวิธีการ `PUT` นี้ มีใครรับผิดชอบ

4. **ยามรักษาความปลอดภัย (`/src/Middleware/AuthMiddleware.php`):** เมื่อ Router เจอว่าเส้นทางนี้มียามเฝ้าอยู่ (เช่น `isSelfOrManager`) มันจะเรียกยามก่อนเลย ยามจะขอดูบัตร (JWT Token) แล้วเช็คว่า "คุณเป็นเจ้าของข้อมูล ID 5 หรือเปล่า? หรือเป็น Manager ขึ้นไปไหม?" ถ้าใช่ ก็จะปล่อยให้เข้าไป ถ้าไม่ใช่ ก็จะไล่กลับไป (Forbidden!)

5. **ผู้เชี่ยวชาญ (`/src/Controllers/UserController.php`):** เมื่อผ่านด่านยามมาได้ Router จะส่งคำขอต่อไปให้ "ผู้เชี่ยวชาญ" ที่ดูแลเรื่อง User โดยเฉพาะ ซึ่งก็คือ `UserController` ของเรานั่นเอง

6. **ลงมือทำ:** `UserController` จะรับคำขอมาแล้วทำงานตามหน้าที่ของมัน เช่น เชื่อมต่อฐานข้อมูล, สร้างคำสั่ง SQL เพื่อ `UPDATE` ข้อมูล, และสุดท้ายคือส่งคำตอบ (Response) กลับไปในรูปแบบ JSON

จะเห็นว่ามีการแบ่งหน้าที่กันชัดเจน ทำให้โค้ดของเราสะอาดและจัดการง่ายครับ

## ขั้นตอนที่ 1: เตรียมฐานข้อมูลให้พร้อม

มาเริ่มกันที่ฐานข้อมูลก่อนเลยครับ (หวังว่าคุณคงติดตั้งโปรแกรมเหล่านี้แล้ว XAMPP , Composer, VSCode, PostMAN, Firefox Developer Edition, ฯลฯ ที่จำเป็นสำหรับ Devops)

### สร้างฐานข้อมูล จากคำสั่ง SQL ต่อไปนี้

เปิด `phpMyAdmin` ขึ้นมา สร้างฐานข้อมูล `api_db`  เลือก collation `utf8mb4_general_ci` หลังจากสร้างเสร็จแล้ว ให้รันคำสั่ง SQL 

### 
```sql
-- ตาราง categories
CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- ตาราง users
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    role ENUM('customer', 'employee', 'manager', 'director', 'admin') DEFAULT 'customer',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- ตาราง products
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    description TEXT,
    category_id INT,
    stock INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL
);

-- ตาราง orders
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    total_amount DECIMAL(10,2) NOT NULL,
    status ENUM('pending', 'completed', 'cancelled') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- ตาราง order_items
CREATE TABLE order_items (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE
);

-- ตาราง addresses
CREATE TABLE addresses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    address_line VARCHAR(255) NOT NULL,
    city VARCHAR(100) NOT NULL,
    postal_code VARCHAR(20) NOT NULL,
    country VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- ตาราง payments
CREATE TABLE payments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    method ENUM('credit_card', 'bank_transfer', 'cash') NOT NULL,
    status ENUM('pending', 'completed', 'failed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE
);

-- ตาราง reviews
CREATE TABLE reviews (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_id INT NOT NULL,
    user_id INT NOT NULL,
    rating INT NOT NULL CHECK (rating >= 1 AND rating <= 5),
    comment TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);


-- ข้อมูลตัวอย่าง
INSERT INTO categories (name, description) VALUES
('Electronics', 'Electronic devices and gadgets'),
('Clothing', 'Apparel and accessories');

INSERT INTO users (username, email, password, first_name, last_name, role) VALUES
('user1', 'user1@example.com', '$2y$10$hashedpassword', 'John', 'Doe', 'customer'),
('admin1', 'admin@example.com', '$2y$10$hashedpassword', 'Admin', 'User', 'admin');

INSERT INTO products (name, price, description, category_id, stock) VALUES
('Laptop', 25000.00, 'High-performance laptop', 1, 50),
('Smartphone', 15000.00, 'Latest model smartphone', 1, 100),
('T-Shirt', 500.00, 'Cotton T-shirt', 2, 200);

INSERT INTO orders (user_id, total_amount, status) VALUES
(1, 25500.00, 'pending');

INSERT INTO order_items (order_id, product_id, quantity, unit_price) VALUES
(1, 1, 1, 25000.00),
(1, 3, 1, 500.00);

INSERT INTO addresses (user_id, address_line, city, postal_code, country) VALUES
(1, '123 Main St', 'Bangkok', '10110', 'Thailand'),
(2, '456 Admin Rd', 'Chiang Mai', '50200', 'Thailand');

INSERT INTO payments (order_id, amount, method, status) VALUES
(1, 25500.00, 'credit_card', 'completed');

INSERT INTO reviews (product_id, user_id, rating, comment) VALUES
(1, 1, 5, 'Great laptop, very fast!'),
(2, 1, 4, 'Good smartphone, but battery could be better.');
```

## สนับสนุนให้ผมทำเนื้อหาดีๆ ได้ตามความเหมาะสม เพื่อเป็นกำลังใจในการทำเนื้อหาดีๆ ต่อไปครับ

![](qr-code.jpg)
** ถ้าต้องการโค้ดแบบเต็ม สามารถสนับสนุนแล้ว ติดต่อได้ที่ sunan.edu@gmail.com


## ขั้นตอนที่ 2: ตั้งค่าโปรเจคและเว็บเซิร์ฟเวอร์ (XAMPP)

เพื่อให้เราเรียก API ผ่าน URL สวยๆ ได้ (เช่น `http://one.com`) เรามาตั้งค่า XAMPP กันก่อนครับ

### 2.1 แก้ไขไฟล์ `httpd-vhosts.conf`

* **ไปที่:** `C:\xampp\apache\conf\extra\httpd-vhosts.conf`

* **ทำอะไร:** เพิ่มโค้ดนี้เข้าไปท้ายไฟล์ เพื่อสร้าง "บ้าน" ให้กับโปรเจคของเรา

```
# VirtualHost สำหรับ localhost (เพื่อให้ phpMyAdmin ใช้งานได้)
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs"
    ServerName localhost
</VirtualHost>

# VirtualHost สำหรับโปรเจค API ของเรา
# *** สำคัญ: DocumentRoot ต้องชี้ไปที่โฟลเดอร์ /public นะครับ ***
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/api1/public"
    ServerName one.com
    <Directory "C:/xampp/htdocs/api1/public">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### 2.2 แก้ไขไฟล์ `hosts` ของ Windows

* **ไปที่:** `C:\Windows\System32\drivers\etc\hosts` (อาจจะต้องเปิดด้วยสิทธิ์ Administrator)

* **ทำอะไร:** เพิ่มบรรทัดนี้เข้าไป เพื่อบอกคอมพิวเตอร์ของเราว่า "ถ้าเจอ `one.com` ให้วิ่งไปที่เครื่องตัวเองนะ"

```
127.0.0.1   localhost
127.0.0.1   one.com
```

### 2.3 Restart Apache

ขั้นตอนสุดท้ายของการตั้งค่า คือเปิด XAMPP Control Panel แล้วกด **Stop** และ **Start** ที่โมดูล Apache หนึ่งครั้งครับ

## ขั้นตอนที่ 3: โครงสร้างไฟล์ของโปรเจค

นี่คือโครงสร้างไฟล์ทั้งหมดที่เราจะสร้างกันครับ การวางไฟล์แบบนี้จะช่วยให้โปรเจคของเราเป็นระเบียบและง่ายต่อการจัดการในระยะยาว

```
C:\xampp\htdocs\api1\
│
├── public/                 <-- โฟลเดอร์สำหรับไฟล์สาธารณะ
│   ├── .htaccess
│   └── index.php           <-- Front Controller
│
├── src/                    <-- โฟลเดอร์สำหรับโค้ดหลัก
│   ├── Controllers/
│   │   ├── AuthController.php
│   │   └── UserController.php
│   ├── Core/
│   │   └── Router.php
│   ├── Middleware/
│   │   └── AuthMiddleware.php
│   └── routes.php          <-- ไฟล์นิยามเส้นทางทั้งหมด
│
├── config/
│   ├── Database.php
│   └── config.php
│
├── core/
│   └── initialize.php
│
├── vendor/                 <-- โฟลเดอร์ของ Composer
│
└── composer.json
```

## ขั้นตอนที่ 4: ลงมือเขียนโค้ดกันเลย!

ถึงเวลาสนุกแล้วครับ! ให้สร้างไฟล์ตามโครงสร้างด้านบน 


### คำสั่งสร้างไฟล์และโฟลเดอร์ ใน C:\xampp\htdocs (คำสั่งนี้เฉพาะ windows 10 → Command Prompt)
```bash
cd /d C:\xampp\htdocs
mkdir api1
cd api1
mkdir public src config core vendor
mkdir src\Controllers src\Core src\Middleware
type nul > public\.htaccess
type nul > public\index.php
type nul > src\Controllers\AuthController.php
type nul > src\Controllers\UserController.php
type nul > src\Core\Router.php
type nul > src\Middleware\AuthMiddleware.php
type nul > src\routes.php
type nul > config\Database.php
type nul > config\config.php
type nul > core\initialize.php
type nul > composer.json
tree /F
```

แล้วคัดลอกโค้ดเหล่านี้ไปวางได้เลย

### ไฟล์: `/composer.json`

```
{
    "require": {
        "firebase/php-jwt": "^6.10"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

**คำแนะนำ:** หลังจากสร้างไฟล์นี้แล้ว ให้เปิด Terminal ในโฟลเดอร์โปรเจค แล้วรัน 2 คำสั่งนี้ครับ: `composer install` และ `composer dump-autoload`

### ไฟล์: `/public/.htaccess`

```
RewriteEngine On

# อนุญาตให้เว็บอื่นเรียกใช้ API ของเราได้ (CORS)
Header set Access-Control-Allow-Origin "*"
Header set Access-Control-Allow-Methods "GET, POST, PUT, DELETE, OPTIONS"
Header set Access-Control-Allow-Headers "Content-Type, Authorization"

# จัดการกับ OPTIONS request ที่เบราว์เซอร์ส่งมาถามก่อน
RewriteCond %{REQUEST_METHOD} OPTIONS
RewriteRule ^(.*)$ $1 [R=200,L]

# ส่งทุก request ที่หาไฟล์ไม่เจอไปที่ index.php
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

### ไฟล์: `/public/index.php`

```php
<?php
// เปิด Error Reporting ไว้สำหรับตอนพัฒนาโปรแกรม
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// เรียกใช้ไฟล์ตั้งค่าเริ่มต้น และ Autoloader ของ Composer
require_once __DIR__ . '/../core/initialize.php';
require_once __DIR__ . '/../src/Core/Router.php';

// สร้าง Router ขึ้นมา
$router = new Router();

// โหลด "สารบัญ" ของเว็บเรา
require_once __DIR__ . '/../src/routes.php';

// สั่งให้ Router เริ่มทำงาน
$router->dispatch();
?>
```

### ไฟล์: `/core/initialize.php`

```php
<?php
// ตั้งค่า Timezone ให้เป็นเวลาประเทศไทย
date_default_timezone_set('Asia/Bangkok');
    
// ตั้งค่า Header พื้นฐานสำหรับทุกๆ Response
header("Content-Type: application/json; charset=UTF-8");
header("Access-Control-Allow-Origin: *");
header("Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS");
header("Access-Control-Max-Age: 3600");
header("Access-Control-Allow-Headers: Content-Type, Access-Control-Allow-Headers, Authorization, X-Requested-With");

// จัดการกับ pre-flight request (OPTIONS)
if ($_SERVER['REQUEST_METHOD'] === 'OPTIONS') {
    http_response_code(200);
    exit();
}

// เรียกใช้ไฟล์ตั้งค่าและ Library ที่จำเป็น
require_once __DIR__ . '/../config/config.php';
require_once __DIR__ . '/../config/Database.php';
require_once __DIR__ . '/../vendor/autoload.php';
?>
```

### ไฟล์: `/config/config.php`

```php
<?php
// ไฟล์สำหรับเก็บค่าตั้งค่าต่างๆ ของโปรเจค

// ตั้งค่าฐานข้อมูล
define('DB_HOST', '127.0.0.1');
define('DB_USER', 'root'); // หรือ username ของคุณ
define('DB_PASS', '');     // หรือ password ของคุณ
define('DB_NAME', 'api_db');

// ตั้งค่า JWT
define('JWT_SECRET', 'YOUR_SUPER_SECRET_KEY_CHANGE_ME'); // **สำคัญมาก: เปลี่ยนเป็น Key ลับของคุณเอง**
define('JWT_ISSUER', 'one.com');
define('JWT_AUDIENCE', 'one.com');
?>
```
🔗 [สร้างรหัสผ่านแบบง่ายๆ](https://passwd.kroovit.com) (กด Ctrl+Click เพื่อเปิดแท็บใหม่)

### ไฟล์: `/config/Database.php`

```php
<?php
class Database {
    // กำหนดตัวแปรสำหรับเก็บข้อมูลการเชื่อมต่อฐานข้อมูล
    private $host = DB_HOST;     // ที่อยู่ของเซิร์ฟเวอร์ฐานข้อมูล
    private $db_name = DB_NAME;  // ชื่อฐานข้อมูล
    private $username = DB_USER; // ชื่อผู้ใช้สำหรับเข้าถึงฐานข้อมูล
    private $password = DB_PASS; // รหัสผ่านสำหรับเข้าถึงฐานข้อมูล
    public $conn;                // ตัวแปรสำหรับเก็บการเชื่อมต่อ PDO

    /**
     * getConnection
     * ฟังก์ชันสำหรับสร้างและคืนค่าการเชื่อมต่อฐานข้อมูลด้วย PDO
     * การเรียกใช้งาน: สร้างอ็อบเจกต์ของคลาส Database แล้วเรียก $database->getConnection()
     * คืนค่า: อ็อบเจกต์ PDO ที่ใช้สำหรับการทำงานกับฐานข้อมูล
     * หากเกิดข้อผิดพลาด: ส่ง HTTP status code 500 และข้อความข้อผิดพลาดในรูปแบบ JSON
     */
    public function getConnection() {
        $this->conn = null;
        try {
            // สร้างการเชื่อมต่อ PDO ด้วย MySQL, host, ชื่อฐานข้อมูล, และกำหนด charset เป็น utf8
            $this->conn = new PDO('mysql:host=' . $this->host . ';dbname=' . $this->db_name . ';charset=utf8', $this->username, $this->password);
            // ตั้งค่า PDO ให้ throw exception เมื่อเกิดข้อผิดพลาด
            $this->conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        } catch(PDOException $exception) {
            // ส่ง HTTP status code 500 และข้อความข้อผิดพลาดในรูปแบบ JSON
            http_response_code(500);
            echo json_encode(['message' => 'Database connection error: ' . $exception->getMessage()]);
            exit();
        }
        return $this->conn;
    }
}
?>
```

### ไฟล์: `/src/Core/Router.php`

```php
<?php
class Router {
    protected $routes = []; // อาร์เรย์สำหรับเก็บข้อมูลเส้นทางทั้งหมด

    /**
     * addRoute
     * ฟังก์ชันสำหรับเพิ่มเส้นทางใหม่ลงในอาร์เรย์ $routes
     * การเรียกใช้งาน: เรียกภายในคลาสผ่านเมธอด get, post, put, delete
     * พารามิเตอร์:
     *   - $method: HTTP method (GET, POST, PUT, DELETE)
     *   - $uri: เส้นทาง URI (อาจมีพารามิเตอร์ เช่น /user/{id})
     *   - $action: อาร์เรย์ที่ระบุ controller และ method ([ControllerClass, methodName])
     *   - $middleware: อาร์เรย์ที่ระบุ middleware และ method ([MiddlewareClass, methodName])
     * ฟังก์ชันนี้แปลง URI ที่มีพารามิเตอร์เป็น regex pattern
     */
    private function addRoute($method, $uri, $action, $middleware = null) {
        $uri = preg_replace('/\{([a-z]+)\}/', '(?P<$1>[^/]+)', $uri);
        $uri = '#^' . $uri . '$#';
        $this->routes[] = [
            'method' => $method,
            'uri' => $uri,
            'action' => $action,
            'middleware' => $middleware
        ];
    }

    /**
     * get, post, put, delete
     * ฟังก์ชันสำหรับกำหนดเส้นทางสำหรับ HTTP method แต่ละประเภท
     * การเรียกใช้งาน: $router->get('/path', [ControllerClass::class, 'methodName'], [MiddlewareClass::class, 'methodName']);
     * พารามิเตอร์:
     *   - $uri: เส้นทาง URI
     *   - $action: อาร์เรย์ที่ระบุ controller และ method
     *   - $middleware: อาร์เรย์ที่ระบุ middleware และ method (ถ้ามี)
     */
    public function get($uri, $action, $middleware = null) { $this->addRoute('GET', $uri, $action, $middleware); }
    public function post($uri, $action, $middleware = null) { $this->addRoute('POST', $uri, $action, $middleware); }
    public function put($uri, $action, $middleware = null) { $this->addRoute('PUT', $uri, $action, $middleware); }
    public function delete($uri, $action, $middleware = null) { $this->addRoute('DELETE', $uri, $action, $middleware); }

    /**
     * dispatch
     * ฟังก์ชันสำหรับจับคู่ URI และ HTTP method กับเส้นทางที่กำหนดไว้
     * การเรียกใช้งาน: $router->dispatch();
     * ตรวจสอบ URI และ method จาก request, หากตรงกับเส้นทางที่กำหนด:
     *   - เรียก middleware (ถ้ามี)
     *   - เรียก controller และ method ที่ระบุใน action พร้อมส่งพารามิเตอร์
     * หากไม่พบเส้นทาง: ส่ง HTTP status code 404 และข้อความ JSON
     */
    public function dispatch() {
        $uri = parse_url($_SERVER['REQUEST_URI'])['path'];
        $method = $_SERVER['REQUEST_METHOD'];

        foreach ($this->routes as $route) {
            if ($route['method'] === $method && preg_match($route['uri'], $uri, $matches)) {
                $params = array_filter($matches, 'is_string', ARRAY_FILTER_USE_KEY);

                if ($route['middleware']) {
                    list($middlewareClass, $middlewareMethod) = $route['middleware'];
                    call_user_func_array([new $middlewareClass, $middlewareMethod], $params);
                }

                list($controllerClass, $controllerMethod) = $route['action'];
                
                $controllerInstance = new $controllerClass();
                call_user_func_array([$controllerInstance, $controllerMethod], $params);
                return;
            }
        }

        http_response_code(404);
        echo json_encode(['message' => 'Endpoint Not Found']);
    }
}
?>
```

### ไฟล์: `/src/Middleware/AuthMiddleware.php`

```php
<?php
namespace App\Middleware;

use Firebase\JWT\JWT;
use Firebase\JWT\Key;

class AuthMiddleware {
    private const ROLE_HIERARCHY = [
        'customer' => 1,
        'employee' => 2,
        'manager' => 3,
        'director' => 4,
        'admin' => 5,
    ]; // กำหนดลำดับชั้นของบทบาทผู้ใช้

    /**
     * getDecodedToken
     * ฟังก์ชันสำหรับตรวจสอบและถอดรหัส JWT token จาก Authorization header
     * การเรียกใช้งาน: เรียกภายในคลาสเมื่อต้องการข้อมูลจาก token
     * คืนค่า: อ็อบเจกต์ที่ถอดรหัสจาก JWT
     * หากเกิดข้อผิดพลาด: ส่ง HTTP status code 401 และข้อความ JSON
     */
    private function getDecodedToken() {
        $authHeader = $_SERVER['HTTP_AUTHORIZATION'] ?? null;
        if (!$authHeader) {
            http_response_code(401);
            echo json_encode(['message' => 'Authentication token not provided.']);
            exit();
        }
        list($jwt) = sscanf($authHeader, 'Bearer %s');
        if (!$jwt) {
            http_response_code(401);
            echo json_encode(['message' => 'Invalid token format.']);
            exit();
        }
        try {
            if (!isset($GLOBALS['decoded_token'])) {
                $GLOBALS['decoded_token'] = JWT::decode($jwt, new Key(JWT_SECRET, 'HS256'));
            }
            return $GLOBALS['decoded_token'];
        } catch (\Exception $e) {
            http_response_code(401);
            echo json_encode(['message' => 'Access denied. ' . $e->getMessage()]);
            exit();
        }
    }

    /**
     * isAuthenticated
     * ฟังก์ชันสำหรับตรวจสอบว่า request มี token ที่ถูกต้องหรือไม่
     * การเรียกใช้งาน: $middleware->isAuthenticated();
     * เรียก getDecodedToken เพื่อตรวจสอบ token
     */
    public function isAuthenticated() { $this->getDecodedToken(); }

    /**
     * hasMinimumRole
     * ฟังก์ชันสำหรับตรวจสอบว่าผู้ใช้มีบทบาทเพียงพอตามที่กำหนดหรือไม่
     * การเรียกใช้งาน: เรียกภายในคลาสผ่าน isEmployee, isManager, isAdmin
     * พารามิเตอร์:
     *   - $requiredRole: บทบาทขั้นต่ำที่ต้องการ
     * หากไม่ผ่าน: ส่ง HTTP status code 403 และข้อความ JSON
     */
    private function hasMinimumRole(string $requiredRole) {
        $decoded = $this->getDecodedToken();
        $userRole = $decoded->data->role;

        if (!isset(self::ROLE_HIERARCHY[$userRole]) || self::ROLE_HIERARCHY[$userRole] < self::ROLE_HIERARCHY[$requiredRole]) {
            http_response_code(403);
            echo json_encode(['message' => 'Forbidden. You do not have sufficient permissions. Required role: ' . $requiredRole . ' or higher.']);
            exit();
        }
    }
    
    /**
     * isEmployee, isManager, isAdmin
     * ฟังก์ชันสำหรับตรวจสอบบทบาทขั้นต่ำของผู้ใช้
     * การเรียกใช้งาน: $middleware->isEmployee();, $middleware->isManager();, $middleware->isAdmin();
     * เรียก hasMinimumRole ด้วยบทบาทที่ระบุ
     */
    public function isEmployee() { $this->hasMinimumRole('employee'); }
    public function isManager() { $this->hasMinimumRole('manager'); }
    public function isAdmin() { $this->hasMinimumRole('admin'); }

    /**
     * isSelfOrHasRole
     * ฟังก์ชันสำหรับตรวจสอบว่าผู้ใช้เป็นเจ้าของทรัพยากรหรือมีบทบาทเพียงพอ
     * การเรียกใช้งาน: เรียกภายในคลาสผ่าน isSelfOrManager, isSelfOrAdmin
     * พารามิเตอร์:
     *   - $id: ID ของทรัพยากร
     *   - $roleOverride: บทบาทขั้นต่ำที่ต้องการหากไม่ใช่เจ้าของ
     * หากไม่ผ่าน: ส่ง HTTP status code 403 และข้อความ JSON
     */
    public function isSelfOrHasRole(string $id, string $roleOverride) {
        $decoded = $this->getDecodedToken();
        $userRole = $decoded->data->role;
        $userId = $decoded->data->id;

        if ($userId == $id) { return; }

        if (!isset(self::ROLE_HIERARCHY[$userRole]) || self::ROLE_HIERARCHY[$userRole] < self::ROLE_HIERARCHY[$roleOverride]) {
            http_response_code(403);
            echo json_encode(['message' => 'Forbidden. You can only access your own resource or must have a role of ' . $roleOverride . ' or higher.']);
            exit();
        }
    }

    /**
     * isSelfOrManager, isSelfOrAdmin
     * ฟังก์ชันสำหรับตรวจสอบว่าเป็นเจ้าของทรัพยากรหรือมีบทบาท manager/admin
     * การเรียกใช้งาน: $middleware->isSelfOrManager($id);, $middleware->isSelfOrAdmin($id);
     * พารามิเตอร์:
     *   - $id: ID ของทรัพยากร
     * เรียก isSelfOrHasRole ด้วยบทบาทที่ระบุ
     */
    public function isSelfOrManager($id) { $this->isSelfOrHasRole($id, 'manager'); }
    public function isSelfOrAdmin($id) { $this->isSelfOrHasRole($id, 'admin'); }
}
?>
```

### ไฟล์: `/src/routes.php`

```php
<?php
use App\Controllers\UserController;
use App\Controllers\AuthController;
use App\Middleware\AuthMiddleware;

// Endpoint สำหรับ Login
$router->post('/auth/login', [AuthController::class, 'login']);

// การสร้าง User และตรวจสอบข้อมูลซ้ำ ไม่ต้อง Login
$router->post('/api/users', [UserController::class, 'create']);
$router->post('/api/users/check-existence', [UserController::class, 'checkExistence']);

// พนักงานขึ้นไป (Employee, Manager, Director, Admin) สามารถดูรายชื่อผู้ใช้ทั้งหมดได้
$router->get('/api/users', [UserController::class, 'index'], [AuthMiddleware::class, 'isEmployee']);

// ลูกค้า (Customer) สามารถดูได้เฉพาะข้อมูลตัวเอง
// แต่ Manager ขึ้นไป สามารถดูข้อมูลของใครก็ได้
$router->get('/api/users/{id}', [UserController::class, 'show'], [AuthMiddleware::class, 'isSelfOrManager']);

// ลูกค้า (Customer) สามารถแก้ไขได้เฉพาะข้อมูลตัวเอง
// แต่ Manager ขึ้นไป สามารถแก้ไขข้อมูลของใครก็ได้
$router->put('/api/users/{id}', [UserController::class, 'update'], [AuthMiddleware::class, 'isSelfOrManager']);

// ลูกค้า (Customer) สามารถเปลี่ยนรหัสผ่านของตัวเองได้เท่านั้น
// แต่ Admin สามารถเปลี่ยนรหัสผ่านของใครก็ได้
$router->post('/api/users/{id}/change-password', [UserController::class, 'changePassword'], [AuthMiddleware::class, 'isSelfOrAdmin']);

// การลบข้อมูล ต้องเป็น Admin เท่านั้น!
$router->delete('/api/users/{id}', [UserController::class, 'delete'], [AuthMiddleware::class, 'isAdmin']);
?>
```

### ไฟล์: `/src/Controllers/AuthController.php`

```php
<?php
namespace App\Controllers;

use Firebase\JWT\JWT;

class AuthController {
    private $db; // ตัวแปรสำหรับเก็บการเชื่อมต่อฐานข้อมูล

    /**
     * __construct
     * ฟังก์ชันเริ่มต้นสำหรับสร้างอ็อบเจกต์ AuthController
     * การเรียกใช้งาน: สร้างอ็อบเจกต์ AuthController อัตโนมัติเมื่อมีการ new
     * สร้างการเชื่อมต่อฐานข้อมูลผ่านคลาส Database
     */
    public function __construct() {
        $database = new \Database();
        $this->db = $database->getConnection();
    }

    /**
     * login
     * ฟังก์ชันสำหรับจัดการการล็อกอินผู้ใช้และสร้าง JWT token
     * การเรียกใช้งาน: $controller->login();
     * อ่านข้อมูล email และ password จาก JSON input
     * ตรวจสอบข้อมูลในฐานข้อมูลและสร้าง JWT หากถูกต้อง
     * คืนค่า: JSON พร้อม token หากสำเร็จ หรือข้อความข้อผิดพลาด
     * หากเกิดข้อผิดพลาด: ส่ง HTTP status code 400 หรือ 401 และข้อความ JSON
     */
    public function login() {
        $data = json_decode(file_get_contents("php://input"));

        if (!isset($data->email) || !isset($data->password)) {
            http_response_code(400);
            echo json_encode(['message' => 'Email and password are required.']);
            exit();
        }

        $email = $data->email;
        $password = $data->password;

        $query = "SELECT id, username, password, role FROM users WHERE email = :email LIMIT 1";
        $stmt = $this->db->prepare($query);
        $stmt->bindParam(':email', $email);
        $stmt->execute();

        if ($stmt->rowCount() > 0) {
            $row = $stmt->fetch(\PDO::FETCH_ASSOC);
            
            if (password_verify($password, $row['password'])) {
                $issuedAt = time();
                $expirationTime = $issuedAt + 3600; // 1 ชั่วโมง
                $payload = [
                    'iss' => JWT_ISSUER,
                    'aud' => JWT_AUDIENCE,
                    'iat' => $issuedAt,
                    'exp' => $expirationTime,
                    'data' => [
                        'id' => $row['id'],
                        'username' => $row['username'],
                        'role' => $row['role']
                    ]
                ];

                $jwt = JWT::encode($payload, JWT_SECRET, 'HS256');

                http_response_code(200);
                echo json_encode([
                    'message' => 'Login successful.',
                    'token' => $jwt
                ]);
            } else {
                http_response_code(401);
                echo json_encode(['message' => 'Login failed. Invalid credentials.']);
            }
        } else {
            http_response_code(401);
            echo json_encode(['message' => 'Login failed. User not found.']);
        }
    }
}
?>
```

### ไฟล์: `/src/Controllers/UserController.php`

```php
<?php
namespace App\Controllers;

class UserController {
    private $db; // ตัวแปรสำหรับเก็บการเชื่อมต่อฐานข้อมูล

    /**
     * __construct
     * ฟังก์ชันเริ่มต้นสำหรับสร้างอ็อบเจกต์ UserController
     * การเรียกใช้งาน: เรียกอัตโนมัติเมื่อสร้างอ็อบเจกต์ด้วย new UserController()
     * หน้าที่: สร้างการเชื่อมต่อฐานข้อมูลผ่านคลาส Database และเก็บไว้ในตัวแปร $db
     */
    public function __construct() {
        $database = new \Database();
        $this->db = $database->getConnection();
    }

    /**
     * index
     * ฟังก์ชันสำหรับดึงรายการผู้ใช้ทั้งหมดจากฐานข้อมูล
     * การเรียกใช้งาน: $controller->index();
     * หน้าที่: 
     *   - ดึงข้อมูลผู้ใช้ทั้งหมด (id, username, email, first_name, last_name, role, created_at)
     *   - รองรับการค้นหาด้วย query string (?q=) สำหรับ username, email, first_name, last_name
     *   - รองรับการกรองตาม role (?role=) โดยจำกัดเฉพาะ role ที่กำหนดใน whitelist
     *   - รองรับการเรียงลำดับด้วย sort_by และ order (asc/desc) โดยจำกัดเฉพาะฟิลด์ใน whitelist
     * คืนค่า: JSON array ของข้อมูลผู้ใช้
     * สถานะ HTTP: 200 (OK)
     */
    public function index() {
        $query = "SELECT id, username, email, first_name, last_name, role, created_at FROM users";
        $conditions = [];
        $params = [];

        if (!empty($_GET['q'])) {
            $conditions[] = "(username LIKE :q OR email LIKE :q OR first_name LIKE :q OR last_name LIKE :q)";
            $params[':q'] = '%' . $_GET['q'] . '%';
        }
        
        $role_whitelist = ['customer', 'employee', 'manager', 'director', 'admin'];
        if (!empty($_GET['role']) && in_array($_GET['role'], $role_whitelist)) {
            $conditions[] = "role = :role";
            $params[':role'] = $_GET['role'];
        }

        if (count($conditions) > 0) {
            $query .= " WHERE " . implode(' AND ', $conditions);
        }

        $sort_by_whitelist = ['id', 'username', 'email', 'first_name', 'last_name', 'created_at'];
        $sort_by = in_array($_GET['sort_by'] ?? '', $sort_by_whitelist) ? $_GET['sort_by'] : 'id';
        $order = in_array(strtolower($_GET['order'] ?? ''), ['asc', 'desc']) ? strtoupper($_GET['order']) : 'ASC';
        $query .= " ORDER BY " . $sort_by . " " . $order;

        $stmt = $this->db->prepare($query);
        $stmt->execute($params);
        $users = $stmt->fetchAll(\PDO::FETCH_ASSOC);
        http_response_code(200);
        echo json_encode($users);
    }

    /**
     * show
     * ฟังก์ชันสำหรับดึงข้อมูลผู้ใช้ตาม ID
     * การเรียกใช้งาน: $controller->show($id);
     * พารามิเตอร์:
     *   - $id: ID ของผู้ใช้
     * หน้าที่: ดึงข้อมูลผู้ใช้ (id, username, email, first_name, last_name, role, created_at) ตาม ID
     * คืนค่า: JSON ของข้อมูลผู้ใช้หากพบ
     * สถานะ HTTP:
     *   - 200 (OK): หากพบผู้ใช้
     *   - 404 (Not Found): หากไม่พบผู้ใช้
     */
    public function show($id) {
        $query = "SELECT id, username, email, first_name, last_name, role, created_at FROM users WHERE id = :id";
        $stmt = $this->db->prepare($query);
        $stmt->bindParam(':id', $id);
        $stmt->execute();
        $user = $stmt->fetch(\PDO::FETCH_ASSOC);
        if ($user) {
            http_response_code(200);
            echo json_encode($user);
        } else {
            http_response_code(404);
            echo json_encode(['message' => 'User not found.']);
        }
    }

    /**
     * create
     * ฟังก์ชันสำหรับสร้างผู้ใช้ใหม่ในฐานข้อมูล
     * การเรียกใช้งาน: $controller->create();
     * หน้าที่:
     *   - อ่านข้อมูลจาก JSON input (username, email, password, first_name, last_name, role)
     *   - ทำความสะอาดข้อมูลด้วย htmlspecialchars และ strip_tags
     *   - hash รหัสผ่านด้วย password_hash
     *   - บันทึกข้อมูลลงตาราง users
     * คืนค่า: JSON พร้อมข้อความสถานะ
     * สถานะ HTTP:
     *   - 201 (Created): หากสร้างสำเร็จ
     *   - 400 (Bad Request): หากข้อมูลไม่ครบ
     *   - 409 (Conflict): หากเกิดข้อผิดพลาดจากฐานข้อมูล (เช่น username หรือ email ซ้ำ)
     *   - 503 (Service Unavailable): หากบันทึกไม่สำเร็จ
     */
    public function create() {
        $data = json_decode(file_get_contents("php://input"));
        if (!empty($data->username) && !empty($data->email) && !empty($data->password)) {
            $query = "INSERT INTO users SET username=:username, email=:email, password=:password, first_name=:first_name, last_name=:last_name, role=:role";
            $stmt = $this->db->prepare($query);

            $username = htmlspecialchars(strip_tags($data->username));
            $email = htmlspecialchars(strip_tags($data->email));
            $first_name = htmlspecialchars(strip_tags($data->first_name ?? ''));
            $last_name = htmlspecialchars(strip_tags($data->last_name ?? ''));
            $role = htmlspecialchars(strip_tags($data->role ?? 'customer'));
            $hashed_password = password_hash($data->password, PASSWORD_DEFAULT);

            $stmt->bindParam(':username', $username);
            $stmt->bindParam(':email', $email);
            $stmt->bindParam(':password', $hashed_password);
            $stmt->bindParam(':first_name', $first_name);
            $stmt->bindParam(':last_name', $last_name);
            $stmt->bindParam(':role', $role);

            try {
                if ($stmt->execute()) {
                    http_response_code(201);
                    echo json_encode(['message' => 'User was created.']);
                } else {
                    http_response_code(503);
                    echo json_encode(['message' => 'Unable to create user.']);
                }
            } catch (\PDOException $e) {
                http_response_code(409);
                echo json_encode(['message' => 'Unable to create user. ' . $e->getMessage()]);
            }
        } else {
            http_response_code(400);
            echo json_encode(['message' => 'Unable to create user. Data is incomplete.']);
        }
    }

    /**
     * update
     * ฟังก์ชันสำหรับอัปเดตข้อมูลผู้ใช้ตาม ID
     * การเรียกใช้งาน: $controller->update($id);
     * พารามิเตอร์:
     *   - $id: ID ของผู้ใช้
     * หน้าที่:
     *   - อ่านข้อมูลจาก JSON input (username, email, first_name, last_name, role)
     *   - ทำความสะอาดข้อมูลด้วย htmlspecialchars และ strip_tags
     *   - อัปเดตข้อมูลในตาราง users ตาม ID
     * คืนค่า: JSON พร้อมข้อความสถานะ
     * สถานะ HTTP:
     *   - 200 (OK): หากอัปเดตสำเร็จ
     *   - 400 (Bad Request): หากข้อมูลไม่ครบ
     *   - 404 (Not Found): หากไม่พบผู้ใช้หรือข้อมูลไม่มีการเปลี่ยนแปลง
     *   - 503 (Service Unavailable): หากอัปเดตไม่สำเร็จ
     */
    public function update($id) {
        $data = json_decode(file_get_contents("php://input"));
        if (!empty($data->username) && !empty($data->email) && !empty($data->role)) {
            $query = "UPDATE users SET username = :username, email = :email, first_name = :first_name, last_name = :last_name, role = :role WHERE id = :id";
            $stmt = $this->db->prepare($query);

            $stmt->bindParam(':username', htmlspecialchars(strip_tags($data->username)));
            $stmt->bindParam(':email', htmlspecialchars(strip_tags($data->email)));
            $stmt->bindParam(':first_name', htmlspecialchars(strip_tags($data->first_name ?? '')));
            $stmt->bindParam(':last_name', htmlspecialchars(strip_tags($data->last_name ?? '')));
            $stmt->bindParam(':role', htmlspecialchars(strip_tags($data->role)));
            $stmt->bindParam(':id', $id);

            if ($stmt->execute()) {
                if ($stmt->rowCount()) {
                    http_response_code(200);
                    echo json_encode(['message' => 'User was updated.']);
                } else {
                    http_response_code(404);
                    echo json_encode(['message' => 'User not found or data is the same.']);
                }
            } else {
                http_response_code(503);
                echo json_encode(['message' => 'Unable to update user.']);
            }
        } else {
            http_response_code(400);
            echo json_encode(['message' => 'Unable to update user. Data is incomplete.']);
        }
    }

    /**
     * delete
     * ฟังก์ชันสำหรับลบผู้ใช้ตาม ID
     * การเรียกใช้งาน: $controller->delete($id);
     * พารามิเตอร์:
     *   - $id: ID ของผู้ใช้
     * หน้าที่: ลบผู้ใช้จากตาราง users ตาม ID
     * คืนค่า: JSON พร้อมข้อความสถานะ
     * สถานะ HTTP:
     *   - 200 (OK): หากลบสำเร็จ
     *   - 404 (Not Found): หากไม่พบผู้ใช้
     *   - 503 (Service Unavailable): หากลบไม่สำเร็จ
     */
    public function delete($id) {
        $query = "DELETE FROM users WHERE id = :id";
        $stmt = $this->db->prepare($query);
        $stmt->bindParam(':id', $id);

        if ($stmt->execute()) {
            if ($stmt->rowCount()) {
                http_response_code(200);
                echo json_encode(['message' => 'User was deleted.']);
            } else {
                http_response_code(404);
                echo json_encode(['message' => 'User not found.']);
            }
        } else {
            http_response_code(503);
            echo json_encode(['message' => 'Unable to delete user.']);
        }
    }

    /**
     * checkExistence
     * ฟังก์ชันสำหรับตรวจสอบว่า username หรือ email มีอยู่ในฐานข้อมูลหรือไม่
     * การเรียกใช้งาน: $controller->checkExistence();
     * หน้าที่:
     *   - อ่านข้อมูลจาก JSON input (username หรือ email)
     *   - ตรวจสอบในตาราง users ว่ามี username หรือ email นี้หรือไม่
     * คืนค่า: JSON พร้อมสถานะ exists (true/false) และข้อความ
     * สถานะ HTTP:
     *   - 200 (OK): หากตรวจสอบสำเร็จ
     *   - 400 (Bad Request): หากไม่มี username หรือ email ใน input
     */
    public function checkExistence() {
        $data = json_decode(file_get_contents("php://input"));
        $field = !empty($data->username) ? 'username' : (!empty($data->email) ? 'email' : null);

        if (!$field) {
            http_response_code(400);
            echo json_encode(['message' => 'Username or email field is required.']);
            return;
        }

        $value = $data->{$field};
        $query = "SELECT id FROM users WHERE " . $field . " = :value LIMIT 1";
        $stmt = $this->db->prepare($query);
        $stmt->bindParam(':value', $value);
        $stmt->execute();

        if ($stmt->rowCount() > 0) {
            echo json_encode(['exists' => true, 'message' => ucfirst($field) . ' already taken.']);
        } else {
            echo json_encode(['exists' => false]);
        }
    }

    /**
     * changePassword
     * ฟังก์ชันสำหรับเปลี่ยนรหัสผ่านของผู้ใช้ตาม ID
     * การเรียกใช้งาน: $controller->changePassword($id);
     * พารามิเตอร์:
     *   - $id: ID ของผู้ใช้
     * หน้าที่:
     *   - อ่านข้อมูล old_password และ new_password จาก JSON input
     *   - ตรวจสอบว่ารหัสผ่านเก่าถูกต้องหรือไม่
     *   - hash รหัสผ่านใหม่และอัปเดตในตาราง users
     * คืนค่า: JSON พร้อมข้อความสถานะ
     * สถานะ HTTP:
     *   - 200 (OK): หากเปลี่ยนรหัสผ่านสำเร็จ
     *   - 400 (Bad Request): หากข้อมูลไม่ครบ
     *   - 401 (Unauthorized): หากรหัสผ่านเก่าไม่ถูกต้อง
     *   - 404 (Not Found): หากไม่พบผู้ใช้
     *   - 503 (Service Unavailable): หากอัปเดตไม่สำเร็จ
     */
    public function changePassword($id) {
        $data = json_decode(file_get_contents("php://input"));

        if (empty($data->old_password) || empty($data->new_password)) {
            http_response_code(400);
            echo json_encode(['message' => 'Old password and new password are required.']);
            return;
        }

        $query = "SELECT password FROM users WHERE id = :id";
        $stmt = $this->db->prepare($query);
        $stmt->bindParam(':id', $id);
        $stmt->execute();
        $row = $stmt->fetch(\PDO::FETCH_ASSOC);

        if (!$row) {
            http_response_code(404);
            echo json_encode(['message' => 'User not found.']);
            return;
        }

        if (password_verify($data->old_password, $row['password'])) {
            $new_hashed_password = password_hash($data->new_password, PASSWORD_DEFAULT);
            $update_query = "UPDATE users SET password = :password WHERE id = :id";
            $update_stmt = $this->db->prepare($update_query);
            $update_stmt->bindParam(':password', $new_hashed_password);
            $update_stmt->bindParam(':id', $id);

            if ($update_stmt->execute()) {
                http_response_code(200);
                echo json_encode(['message' => 'Password updated successfully.']);
            } else {
                http_response_code(503);
                echo json_encode(['message' => 'Unable to update password.']);
            }
        } else {
            http_response_code(401);
            echo json_encode(['message' => 'Incorrect old password.']);
        }
    }
}
?>
```

# 5.การใช้งาน API และตัวอย่างการเรียก Endpoint

จะอธิบายวิธีการเรียกใช้งานแต่ละ Endpoint ของ API ที่เราได้สร้างขึ้น พร้อมตัวอย่าง Request, Response, และสิทธิ์ที่จำเป็นในการเข้าถึง

## 5.1 การเตรียมตัวเบื้องต้น

* **โปรแกรม:** ต้องมีโปรแกรมสำหรับทดสอบ API เช่น 🔗 [Postman](https://www.postman.com/downloads/) (กด Ctrl+Click เพื่อเปิดแท็บใหม่)

* **Token:** การเรียกใช้งาน Endpoint ส่วนใหญ่จำเป็นต้องมีการยืนยันตัวตนด้วย JWT Token ซึ่งจะได้รับมาจากการ Login

## 5.2 การยืนยันตัวตน (Authentication)

### Login เพื่อรับ Token

นี่คือขั้นตอนแรกและสำคัญที่สุดเพื่อเข้าใช้งานระบบ

* **Endpoint:** `POST /auth/login`

* **สิทธิ์:** ไม่ต้อง Login (แขก)

* **คำอธิบาย:** ส่ง `email` และ `password` เพื่อขอรับ JWT Token สำหรับการยืนยันตัวตนใน Request ต่อๆ ไป

**ตัวอย่าง Request Body:**

```
{
    "email": "admin@example.com",
    "password": "your_password"
}
```

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "message": "Login successful.",
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3Mi..."
}
```

**คำแนะนำ:** ให้คัดลอกค่า `token` ที่ได้ทั้งหมดเก็บไว้เพื่อใช้ใน Header ของ Request อื่นๆ

## 5.3 การจัดการผู้ใช้ (User Management)

**Header ที่ต้องใช้ (สำหรับทุก Endpoint ที่ต้อง Login):**

* **Key:** `Authorization`

* **Value:** `Bearer <TOKEN_ที่ได้จากการ_LOGIN>`

### 1) สร้างผู้ใช้ใหม่ (Create User)

* **Endpoint:** `POST /api/users`

* **สิทธิ์:** ไม่ต้อง Login (แขก)

* **คำอธิบาย:** สร้างผู้ใช้ใหม่ในระบบ

**ตัวอย่าง Request Body:**

```
{
    "username": "new_employee",
    "email": "employee1@example.com",
    "password": "password123",
    "first_name": "Test",
    "last_name": "Employee",
    "role": "employee"
}
```

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "message": "User was created."
}
```

### 2) ตรวจสอบ Username/Email ซ้ำ

* **Endpoint:** `POST /api/users/check-existence`

* **สิทธิ์:** ไม่ต้อง Login (แขก)

* **คำอธิบาย:** ใช้สำหรับตรวจสอบว่า `username` หรือ `email` ที่ต้องการใช้นั้นมีอยู่ในระบบแล้วหรือยัง

**ตัวอย่าง Request Body:**

```
{
    "email": "employee1@example.com"
}
```

**ตัวอย่าง Response (ถ้ามีอยู่แล้ว):**

```
{
    "exists": true,
    "message": "Email already taken."
}
```

### 3) ดูข้อมูลผู้ใช้ทั้งหมด (Get All Users)

* **Endpoint:** `GET /api/users`

* **สิทธิ์:** พนักงาน (employee) ขึ้นไป

* **คำอธิบาย:** ดึงรายชื่อผู้ใช้ทั้งหมด สามารถใช้ Query Parameters เพื่อค้นหา, กรอง และเรียงลำดับได้

**ตัวอย่างการเรียกใช้งาน:**

* **ดูทั้งหมด:** `GET /api/users`

* **ค้นหา:** `GET /api/users?q=John`

* **กรองตาม Role:** `GET /api/users?role=manager`

* **เรียงลำดับ:** `GET /api/users?sort_by=email&order=desc`

* **ใช้ร่วมกัน:** `GET /api/users?role=customer&sort_by=created_at&order=desc`

**ตัวอย่าง Response (สำเร็จ):**

```
[
    {
        "id": 1,
        "username": "admin1",
        "email": "admin@example.com",
        "first_name": "Admin",
        "last_name": "User",
        "role": "admin",
        "created_at": "2025-07-16 03:45:00"
    },
    {
        "id": 2,
        "username": "new_employee",
        "email": "employee1@example.com",
        "first_name": "Test",
        "last_name": "Employee",
        "role": "employee",
        "created_at": "2025-07-16 03:50:15"
    }
]
```

### 4) ดูข้อมูลผู้ใช้คนเดียว (Get Single User)

* **Endpoint:** `GET /api/users/{id}`

* **สิทธิ์:**

  * **ลูกค้า (customer):** ดูได้เฉพาะข้อมูลตัวเอง

  * **หัวหน้า (manager) ขึ้นไป:** ดูข้อมูลของใครก็ได้

* **คำอธิบาย:** ดึงข้อมูลผู้ใช้ตาม ID ที่ระบุ

**ตัวอย่างการเรียกใช้งาน:** `GET /api/users/2`

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "id": 2,
    "username": "new_employee",
    "email": "employee1@example.com",
    "first_name": "Test",
    "last_name": "Employee",
    "role": "employee",
    "created_at": "2025-07-16 03:50:15"
}
```

### 5) แก้ไขข้อมูลผู้ใช้ (Update User)

* **Endpoint:** `PUT /api/users/{id}`

* **สิทธิ์:**

  * **ลูกค้า (customer):** แก้ไขได้เฉพาะข้อมูลตัวเอง

  * **หัวหน้า (manager) ขึ้นไป:** แก้ไขข้อมูลของใครก็ได้

* **คำอธิบาย:** อัปเดตข้อมูลทั่วไปของผู้ใช้

**ตัวอย่างการเรียกใช้งาน:** `PUT /api/users/2`

**ตัวอย่าง Request Body:**

```
{
    "username": "new_employee_updated",
    "email": "employee1.new@example.com",
    "first_name": "Test",
    "last_name": "EmployeeUpdated",
    "role": "employee"
}
```

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "message": "User was updated."
}
```

### 6) เปลี่ยนรหัสผ่าน (Change Password)

* **Endpoint:** `POST /api/users/{id}/change-password`

* **สิทธิ์:**

  * **ลูกค้า (customer):** เปลี่ยนได้เฉพาะรหัสผ่านตัวเอง

  * **ผู้ดูแลระบบ (admin):** เปลี่ยนรหัสผ่านของใครก็ได้

* **คำอธิบาย:** เปลี่ยนรหัสผ่านของผู้ใช้

**ตัวอย่างการเรียกใช้งาน:** `POST /api/users/2/change-password`

**ตัวอย่าง Request Body:**

```
{
    "old_password": "password123",
    "new_password": "newStrongerPassword456"
}
```

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "message": "Password updated successfully."
}
```

### 7) ลบผู้ใช้ (Delete User)

* **Endpoint:** `DELETE /api/users/{id}`

* **สิทธิ์:** ผู้ดูแลระบบ (admin) เท่านั้น

* **คำอธิบาย:** ลบผู้ใช้ออกจากระบบ (เป็นการกระทำที่ควรระวัง)

**ตัวอย่างการเรียกใช้งาน:** `DELETE /api/users/2`

**ตัวอย่าง Response (สำเร็จ):**

```
{
    "message": "User was deleted."
}
```

### 6.วิธีใช้งานไฟล์ Postman Collection

6.1. **คัดลอกโค้ด:** คัดลอกเนื้อหาทั้งหมดในกล่องโค้ด "Postman Collection สำหรับทดสอบ API" ด้านล่างสุด

6.2. **สร้างไฟล์ใหม่:** สร้างไฟล์ใหม่บนคอมพิวเตอร์ของคุณ ตั้งชื่ออะไรก็ได้ แต่ให้ลงท้ายด้วย `.json` เช่น `RestAPI-Basic.postman_collection.json`

6.3. **วางโค้ด:** วางโค้ดที่คัดลอกมาลงในไฟล์แล้วบันทึก

6.4. **Import ใน Postman:**

   * เปิดโปรแกรม Postman

   * ไปที่เมนู `File` > `Import...` หรือกดปุ่ม `Import`

   * เลือกไฟล์ `.json` ที่คุณเพิ่งสร้างไว้

6.5. **ทดสอบ:**

   * คุณจะเห็น Collection ใหม่ชื่อ "RestAPI-Basic"

   * เปิด Collection แล้วไปที่ `Authentication` > `Login`

   * แก้ไข `email` และ `password` ใน Body ให้ถูกต้องแล้วกด `Send`

   * หลังจาก Login สำเร็จ Token จะถูกบันทึกอัตโนมัติ

   * ตอนนี้คุณสามารถเรียกใช้งาน Request อื่นๆ ในโฟลเดอร์ `User Management` ได้เลย

```json
{
	"info": {
		"_postman_id": "a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d",
		"name": "RestAPI-Basic",
		"description": "Collection for testing the PHP REST API with JWT and Role-Based Access Control.",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
	},
	"item": [
		{
			"name": "Authentication",
			"item": [
				{
					"name": "Login",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"// ทดสอบว่า request สำเร็จหรือไม่",
									"pm.test(\"Status code is 200\", function () {",
									"    pm.response.to.have.status(200);",
									"});",
									"",
									"// ดึง token จาก response แล้วเก็บไว้ใน collection variable",
									"var jsonData = pm.response.json();",
									"if (jsonData.token) {",
									"    pm.collectionVariables.set(\"jwt_token\", jsonData.token);",
									"    console.log(\"JWT Token saved.\");",
									"}"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"email\": \"admin@example.com\",\n    \"password\": \"admin_password\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{baseUrl}}/auth/login",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"auth",
								"login"
							]
						},
						"description": "ส่ง Email และ Password เพื่อรับ JWT Token. \nToken จะถูกบันทึกใน Collection Variable `jwt_token` อัตโนมัติ"
					},
					"response": []
				}
			],
			"description": "Endpoints สำหรับการยืนยันตัวตน"
		},
		{
			"name": "User Management",
			"item": [
				{
					"name": "Create User",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"username\": \"new_manager\",\n    \"email\": \"manager@example.com\",\n    \"password\": \"manager_pass\",\n    \"first_name\": \"The\",\n    \"last_name\": \"Manager\",\n    \"role\": \"manager\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{baseUrl}}/api/users",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users"
							]
						},
						"description": "สร้างผู้ใช้ใหม่ ไม่ต้อง Login"
					},
					"response": []
				},
				{
					"name": "Check Existence",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"email\": \"manager@example.com\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{baseUrl}}/api/users/check-existence",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users",
								"check-existence"
							]
						},
						"description": "ตรวจสอบว่า username หรือ email มีอยู่แล้วหรือไม่"
					},
					"response": []
				},
				{
					"name": "Get All Users",
					"protocolProfileBehavior": {
						"disableBodyPruning": true
					},
					"request": {
						"method": "GET",
						"header": [],
						"body": {},
						"url": {
							"raw": "{{baseUrl}}/api/users?role=manager&sort_by=email",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users"
							],
							"query": [
								{
									"key": "role",
									"value": "manager",
									"description": "กรองตาม role (customer, employee, manager, director, admin)"
								},
								{
									"key": "sort_by",
									"value": "email",
									"description": "เรียงตาม (id, username, email, first_name, last_name, created_at)"
								},
								{
									"key": "order",
									"value": "asc",
									"description": "(asc, desc)",
									"disabled": true
								},
								{
									"key": "q",
									"value": "test",
									"description": "ค้นหาด้วย keyword",
									"disabled": true
								}
							]
						},
						"description": "ดูผู้ใช้ทั้งหมด (ต้องมีสิทธิ์ Employee ขึ้นไป)"
					},
					"response": []
				},
				{
					"name": "Get Single User",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{baseUrl}}/api/users/2",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users",
								"2"
							]
						},
						"description": "ดูข้อมูลผู้ใช้คนเดียว (ต้องเป็นเจ้าของ หรือ Manager ขึ้นไป)"
					},
					"response": []
				},
				{
					"name": "Update User",
					"request": {
						"method": "PUT",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"username\": \"the_manager\",\n    \"email\": \"manager.new@example.com\",\n    \"first_name\": \"The\",\n    \"last_name\": \"Big Boss\",\n    \"role\": \"director\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{baseUrl}}/api/users/3",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users",
								"3"
							]
						},
						"description": "แก้ไขข้อมูลผู้ใช้ (ต้องเป็นเจ้าของ หรือ Manager ขึ้นไป)"
					},
					"response": []
				},
				{
					"name": "Change Password",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"old_password\": \"manager_pass\",\n    \"new_password\": \"new_manager_password\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{baseUrl}}/api/users/3/change-password",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users",
								"3",
								"change-password"
							]
						},
						"description": "เปลี่ยนรหัสผ่าน (ต้องเป็นเจ้าของ หรือ Admin)"
					},
					"response": []
				},
				{
					"name": "Delete User",
					"request": {
						"method": "DELETE",
						"header": [],
						"url": {
							"raw": "{{baseUrl}}/api/users/4",
							"host": [
								"{{baseUrl}}"
							],
							"path": [
								"api",
								"users",
								"4"
							]
						},
						"description": "ลบผู้ใช้ (ต้องเป็น Admin เท่านั้น)"
					},
					"response": []
				}
			],
			"auth": {
				"type": "bearer",
				"bearer": [
					{
						"key": "token",
						"value": "{{jwt_token}}",
						"type": "string"
					}
				]
			},
			"event": [
				{
					"listen": "prerequest",
					"script": {
						"type": "text/javascript",
						"exec": [
							"// --- สคริปต์ตรวจสอบ JWT Token ก่อนใช้งาน ---",
							"",
							"// 1. ดึง Token จากตัวแปรของ Collection",
							"const token = pm.collectionVariables.get(\"jwt_token\");",
							"",
							"// 2. ตรวจสอบว่ามี Token เก็บอยู่หรือไม่",
							"if (!token) {",
							"    console.warn(\"ยังไม่มี JWT Token! กรุณา Login ก่อน\");",
							"} else {",
							"    console.log(\"Current JWT Token:\", token);",
							"",
							"    try {",
							"        // 3. ถอดรหัสส่วน Payload (ส่วนกลางของ Token)",
							"        const payloadBase64 = token.split('.')[1];",
							"        const payloadJson = atob(payloadBase64); // atob คือฟังก์ชันถอดรหัส Base64",
							"        const payload = JSON.parse(payloadJson);",
							"",
							"        console.log(\"ข้อมูลใน Token (Payload):\", payload);",
							"",
							"        // 4. ตรวจสอบวันหมดอายุ (exp)",
							"        const expirationTime = payload.exp; // เวลาหมดอายุ (เป็น Unix Timestamp หน่วยวินาที)",
							"        const currentTime = Math.floor(Date.now() / 1000); // เวลาปัจจุบัน (หน่วยวินาที)",
							"",
							"        // แปลงเป็นเวลาที่อ่านง่ายเพื่อแสดงผล",
							"        const expirationDate = new Date(expirationTime * 1000);",
							"        const currentDate = new Date(currentTime * 1000);",
							"",
							"        console.log(\"Token หมดอายุเวลา:\", expirationDate.toLocaleString('th-TH'));",
							"        console.log(\"เวลาปัจจุบันคือ:\", currentDate.toLocaleString('th-TH'));",
							"        ",
							"        if (currentTime >= expirationTime) {",
							"            console.error(\"!!! TOKEN หมดอายุแล้ว !!! กรุณา Login ใหม่อีกครั้ง\");",
							"        } else {",
							"            const timeLeft = expirationTime - currentTime;",
							"            console.log(`Token ยังใช้งานได้ เหลือเวลาอีก: ${timeLeft} วินาที`);",
							"        }",
							"",
							"    } catch (e) {",
							"        console.error(\"ไม่สามารถถอดรหัส JWT Token ได้ อาจจะมีรูปแบบไม่ถูกต้อง\", e);",
							"    }",
							"}"
						]
					}
				},
				{
					"listen": "test",
					"script": {
						"type": "text/javascript",
						"exec": [
							""
						]
					}
				}
			]
		}
	],
	"variable": [
		{
			"key": "baseUrl",
			"value": "http://one.com",
			"type": "default"
		},
		{
			"key": "jwt_token",
			"value": "",
			"type": "default",
			"description": "จะถูกเติมค่าอัตโนมัติหลังจาก Login"
		}
	]
}
```

🎯 ในขั้นตอนต่อไปจะเป็นการจัดการกับ products, orders, order_items, categories, reviews, payments, addresses และ การสร้าง Front-End หรือเว็บแอพเพื่อใช้งาน API โปรแกรมติดตามต่อไปกันครับ 🎯

