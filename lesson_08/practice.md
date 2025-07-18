# 📐 Amaliy mashqlar — Lesson 08

## 🎯 Maqsad:
PostgreSQLʼda NULL va DEFAULT qiymatlar bilan ishlashni amalda oʼrganish.

---

## 🔷 Vazifalar:
1⃣ Jadval yarating va ustunlarga DEFAULT va NOT NULL cheklovlari qoʼshing  
2⃣ NULL va DEFAULT qiymatlar bilan yozuvlar kiriting  
3⃣ NULL va DEFAULT qiymatlarni SELECT bilan koʼring  
4⃣ COALESCE va IS NULL operatorlarini amalda sinab koʼring  
5⃣ DEFAULT qiymatni oʼzgartiring va natijani tekshiring

---

## 💻 Buyruqlar:

### 1. Jadval yaratish:
```sql
CREATE TABLE contacts (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    email VARCHAR(100) DEFAULT 'noemail@example.com',
    is_active BOOLEAN DEFAULT TRUE
);
```

### 2. NULL va DEFAULT qiymatlar bilan yozuv kiritish:
```sql
-- Faqat majburiy ustunlar bilan (DEFAULT va NULL ishlatiladi)
INSERT INTO contacts (name) VALUES ('Ali Valiyev');

-- NULL qiymat kiritish
INSERT INTO contacts (name, phone) VALUES ('Gulbahor Karimova', NULL);

-- DEFAULT kalit soʼzi bilan
INSERT INTO contacts (name, email) VALUES ('Aziz Toshmatov', DEFAULT);

-- Barcha ustunlar bilan
INSERT INTO contacts (name, phone, email, is_active) VALUES ('Malika Yusupova', '998901234567', 'malika@example.com', FALSE);
```

### 3. NULL va DEFAULT qiymatlarni SELECT bilan koʼrish:
```sql
-- Barcha kontaktlarni koʼrish
SELECT * FROM contacts;

-- Faqat NULL qiymatli telefon raqamlari
SELECT * FROM contacts WHERE phone IS NULL;

-- Faqat DEFAULT qiymatli email
SELECT * FROM contacts WHERE email = 'noemail@example.com';
```

### 4. COALESCE va IS NULL operatorlari:
```sql
-- Telefon raqami yoʼq boʼlsa, 'yoʼq' deb chiqarsin
SELECT name, COALESCE(phone, 'yoʼq') AS telefon FROM contacts;

-- Emaili mavjud boʼlmaganlar
SELECT name FROM contacts WHERE email IS NULL;
```

### 5. DEFAULT qiymatni oʼzgartirish va natijani tekshirish:
```sql
ALTER TABLE contacts ALTER COLUMN email SET DEFAULT 'user@example.com';
INSERT INTO contacts (name) VALUES ('Rustam Jalilov');
SELECT * FROM contacts WHERE name = 'Rustam Jalilov';
```

---

## 📋 Kutilgan natija:

| id | name               | phone         | email                | is_active |
|----|--------------------|--------------|----------------------|-----------|
| 1  | Ali Valiyev        | NULL         | noemail@example.com  | t         |
| 2  | Gulbahor Karimova  | NULL         | noemail@example.com  | t         |
| 3  | Aziz Toshmatov     | NULL         | noemail@example.com  | t         |
| 4  | Malika Yusupova    | 998901234567 | malika@example.com   | f         |
| 5  | Rustam Jalilov     | NULL         | user@example.com     | t         |

---

## 🔍 Qoʼshimcha topshiriqlar:
- NOT NULL cheklovi bilan xatolik keltirib chiqarib koʼring
- COALESCE yordamida barcha NULL qiymatlarni oʼzgartirib chiqaring
- DEFAULT qiymatni yana oʼzgartirib, yangi yozuv kiriting
- IS NOT NULL operatori bilan faqat qiymati bor ustunlarni koʼring 