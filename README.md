# RestAPI-Basic

ออกแบบระบบ RestAPI ด้วย PHP PDO รองรับ Endpoint พื้นฐาน GET POST PUT DELETE (CRUD) รองรับ JWT Token แบบง่ายๆ สำหรับมือใหม่

สวัสดีครับ! ในคู่มือนี้ เราจะมาสร้าง REST API พื้นฐานด้วย PHP กันแบบจับมือทำทีละขั้นตอนเลยนะครับ ผมจะพยายามใช้คำพูดง่ายๆ เป็นกันเอง ให้เหมือนเรานั่งทำโปรเจคอยู่ข้างๆ กันเลย เป้าหมายของเราคือการสร้าง API ที่มีระบบจัดการผู้ใช้ (Users) พร้อมระบบสิทธิ์ (Permissions) ที่แข็งแรงและยืดหยุ่น โดยใช้เครื่องมือพื้นฐานที่นักพัฒนาเว็บคุ้นเคยกันดีครับ

## ขั้นตอนที่ แรก: มาทำความเข้าใจภาพรวมกันก่อน

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

### หลักการทำงานของ API และการไหลของข้อมูล

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

มาเริ่มกันที่ฐานข้อมูลก่อนเลยครับ

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

ถึงเวลาสนุกแล้วครับ! ให้สร้างไฟล์ตามโครงสร้างด้านบน แล้วคัดลอกโค้ดเหล่านี้ไปวางได้เลย

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

```
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

```
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

```
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

### ไฟล์: `/config/Database.php`

```
<?php
class Database {
    private $host = DB_HOST;
    private $db_name = DB_NAME;
    private $username = DB_USER;
    private $password = DB_PASS;
    public $conn;

    public function getConnection() {
        $this->conn = null;
        try {
            $this->conn = new PDO('mysql:host=' . $this->host . ';dbname=' . $this->db_name . ';charset=utf8', $this->username, $this->password);
            $this->conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        } catch(PDOException $exception) {
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

```
<?php
class Router {
    protected $routes = [];

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

    public function get($uri, $action, $middleware = null) { $this->addRoute('GET', $uri, $action, $middleware); }
    public function post($uri, $action, $middleware = null) { $this->addRoute('POST', $uri, $action, $middleware); }
    public function put($uri, $action, $middleware = null) { $this->addRoute('PUT', $uri, $action, $middleware); }
    public function delete($uri, $action, $middleware = null) { $this->addRoute('DELETE', $uri, $action, $middleware); }

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

```
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
    ];

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

    public function isAuthenticated() { $this->getDecodedToken(); }

    private function hasMinimumRole(string $requiredRole) {
        $decoded = $this->getDecodedToken();
        $userRole = $decoded->data->role;

        if (!isset(self::ROLE_HIERARCHY[$userRole]) || self::ROLE_HIERARCHY[$userRole] < self::ROLE_HIERARCHY[$requiredRole]) {
            http_response_code(403);
            echo json_encode(['message' => 'Forbidden. You do not have sufficient permissions. Required role: ' . $requiredRole . ' or higher.']);
            exit();
        }
    }
    
    public function isEmployee() { $this->hasMinimumRole('employee'); }
    public function isManager() { $this->hasMinimumRole('manager'); }
    public function isAdmin() { $this->hasMinimumRole('admin'); }

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

    public function isSelfOrManager($id) { $this->isSelfOrHasRole($id, 'manager'); }
    public function isSelfOrAdmin($id) { $this->isSelfOrHasRole($id, 'admin'); }
}
?>
```

### ไฟล์: `/src/routes.php`

```
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

```
<?php
namespace App\Controllers;

use Firebase\JWT\JWT;

class AuthController {
    private $db;

    public function __construct() {
        $database = new \Database();
        $this->db = $database->getConnection();
    }

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

```
<?php
namespace App\Controllers;

class UserController {
    private $db;

    public function __construct() {
        $database = new \Database();
        $this->db = $database->getConnection();
    }

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

