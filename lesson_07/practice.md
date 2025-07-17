# 📐 Amaliy mashqlar — Lesson 07

## 🎯 Maqsad:
PostgreSQLʼda INSERT buyrugʼini turli usullar bilan amalda qoʼllash va maʼlumotlarni samarali kiritishni oʼrganish.

---

## 🔷 Vazifalar:
1⃣ `employees` jadvalini yarating va turli usullar bilan maʼlumotlar kiritish  
2⃣ SERIAL, NULL va DEFAULT qiymatlar bilan ishlash  
3⃣ Bir nechta yozuvni bir vaqtda kiritish  
4⃣ Boshqa jadvaldan maʼlumot kiritish  
5⃣ RETURNING kalit soʼzi bilan natijani koʼrish  
6⃣ Xatolarni oldini olish va tekshirish

---

## 💻 Buyruqlar:

### 1. Jadval yaratish:
```sql
-- Employees jadvalini yarating
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INTEGER,
    salary NUMERIC(10,2) DEFAULT 0,
    email VARCHAR(255),
    department VARCHAR(50) DEFAULT 'IT',
    hire_date DATE DEFAULT CURRENT_DATE
);

-- Departments jadvalini yarating
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    location VARCHAR(100)
);
```

### 2. Bitta yozuv kiritish:
```sql
-- Barcha ustunlar bilan
INSERT INTO employees (id, name, age, salary, email, department, hire_date) 
VALUES (1, 'Ali Valiyev', 25, 2500.00, 'ali@company.com', 'IT', '2024-01-15');

-- Faqat kerakli ustunlar bilan
INSERT INTO employees (name, age, salary) 
VALUES ('Vali Karimov', 30, 3000.00);

-- SERIAL ustun avtomatik to'ldiriladi
INSERT INTO employees (name, age, email) 
VALUES ('Gulbahor Toshmatova', 28, 'gulbahor@company.com');
```

### 3. Bir nechta yozuv kiritish:
```sql
-- Bir qator ichida
INSERT INTO employees (name, age, salary, email, department) VALUES 
('Aziz Yusupov', 32, 3500.00, 'aziz@company.com', 'HR'),
('Malika Karimova', 26, 2800.00, 'malika@company.com', 'Marketing'),
('Jasur Turgunov', 29, 3200.00, 'jasur@company.com', 'IT');

-- Alohida qatorlarda
INSERT INTO employees (name, age, salary, email, department) VALUES 
('Dilfuza Rahimova', 27, 2700.00, 'dilfuza@company.com', 'Finance'),
('Bekzod Alimov', 31, 3800.00, 'bekzod@company.com', 'IT');
```

### 4. NULL va DEFAULT qiymatlar bilan:
```sql
-- NULL qiymat kiritish
INSERT INTO employees (name, age, email) 
VALUES ('Zarina Nurmatova', 24, NULL);

-- DEFAULT qiymatdan foydalanish
INSERT INTO employees (name, age) 
VALUES ('Rustam Jalilov', 33);

-- DEFAULT kalit so'zi bilan
INSERT INTO employees (name, age, salary, department) 
VALUES ('Nodira Azimova', 29, DEFAULT, DEFAULT);
```

### 5. Departments jadvaliga maʼlumot kiritish:
```sql
INSERT INTO departments (name, location) VALUES 
('IT', 'Toshkent'),
('HR', 'Toshkent'),
('Marketing', 'Samarqand'),
('Finance', 'Toshkent'),
('Sales', 'Buxoro');
```

### 6. Boshqa jadvaldan maʼlumot kiritish:
```sql
-- Yangi jadval yaratish
CREATE TABLE it_employees AS 
SELECT * FROM employees WHERE department = 'IT';

-- Maʼlumotlarni boshqa jadvalga kiritish
INSERT INTO it_employees (name, age, salary, email)
SELECT name, age, salary, email FROM employees WHERE department = 'IT';
```

### 7. RETURNING kalit soʼzi bilan:
```sql
-- Kiritilgan yozuvni qaytarish
INSERT INTO employees (name, age, salary, email) 
VALUES ('Laziz Toshmatov', 35, 4500.00, 'laziz@company.com')
RETURNING id, name, salary;

-- Bir nechta yozuv kiritish natijasi
INSERT INTO employees (name, age, salary, email) VALUES 
('Shahnoza Karimova', 26, 2900.00, 'shahnoza@company.com'),
('Farrux Alimov', 34, 4200.00, 'farrux@company.com')
RETURNING id, name, department;
```

### 8. Maʼlumotlarni koʼrish:
```sql
-- Barcha xodimlarni koʼrish
SELECT * FROM employees;

-- Faqat IT boʼlimi xodimlarini koʼrish
SELECT name, age, salary FROM employees WHERE department = 'IT';

-- Boʼlimlar roʼyxatini koʼrish
SELECT * FROM departments;
```

---

## 📋 Kutilgan natija:

### Employees jadvali:
| id | name | age | salary | email | department | hire_date |
|----|------|-----|--------|-------|------------|-----------|
| 1  | Ali Valiyev | 25 | 2500.00 | ali@company.com | IT | 2024-01-15 |
| 2  | Vali Karimov | 30 | 3000.00 | NULL | IT | 2024-07-17 |
| 3  | Gulbahor Toshmatova | 28 | 0.00 | gulbahor@company.com | IT | 2024-07-17 |
| 4  | Aziz Yusupov | 32 | 3500.00 | aziz@company.com | HR | 2024-07-17 |
| 5  | Malika Karimova | 26 | 2800.00 | malika@company.com | Marketing | 2024-07-17 |

### Departments jadvali:
| id | name | location |
|----|------|----------|
| 1  | IT | Toshkent |
| 2  | HR | Toshkent |
| 3  | Marketing | Samarqand |
| 4  | Finance | Toshkent |
| 5  | Sales | Buxoro |

---

## 🔍 Qoʼshimcha topshiriqlar:
- Yangi jadval yarating va INSERT ... SELECT bilan maʼlumot kiritish
- UNIQUE cheklovlari bilan jadval yarating va xatolarni sinab koʼring
- NOT NULL cheklovlari bilan ishlang
- Tranzaksiyalar (BEGIN, COMMIT, ROLLBACK) bilan INSERT qiling
- Katta hajmdagi maʼlumotlarni kiritish uchun BATCH INSERT ishlatish
- Maʼlumotlarni fayldan yuklash (COPY buyrugʼi) ni oʼrganing 