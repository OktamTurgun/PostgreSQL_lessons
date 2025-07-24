# 📝 Amaliy mashqlar — View va virtual jadvallar

---

### 1. Oddiy view yaratish
**Vazifa:** students jadvalidan faqat bahosi 'A' bo‘lgan talabalarni ko‘rsatuvchi view yarating.

**Kod:**
```sql
CREATE VIEW excellent_students AS
SELECT id, name
FROM students
WHERE grade = 'A';
```
**Natija:**
| id | name |
|----|------|
| 1  | Ali  |

**Izoh:** excellent_students view’iga SELECT so‘rovi yuborilsa, faqat bahosi A bo‘lgan talabalar chiqadi.

**Tushuntirish:** View yordamida tez-tez kerak bo‘ladigan so‘rovlarni soddalashtirish mumkin.

---

### 2. JOIN bilan view yaratish
**Vazifa:** students va orders jadvallarini birlashtirib, har bir talabaning buyurtmalari ko‘rsatiladigan view yarating.

**Kod:**
```sql
CREATE VIEW student_orders AS
SELECT s.name, o.product, o.amount
FROM students s
JOIN orders o ON s.id = o.student_id;
```
**Natija:**
| name | product | amount |
|------|---------|--------|
| Ali  | Kitob   | 2      |
| Vali | Daftar  | 3      |

**Izoh:** student_orders view’ida har bir talabaning buyurtmalari ko‘rsatiladi.

**Tushuntirish:** JOIN yordamida bir nechta jadvaldan ma’lumotlarni bitta view’da ko‘rish mumkin.

---

### 3. View’ni yangilash
**Vazifa:** excellent_students view’ini yangilab, endi bahosi 'A' yoki 'B' bo‘lgan talabalarni ko‘rsating.

**Kod:**
```sql
CREATE OR REPLACE VIEW excellent_students AS
SELECT id, name, grade
FROM students
WHERE grade IN ('A', 'B');
```
**Natija:**
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | A     |
| 2  | Vali   | B     |

**Izoh:** Endi view’da bahosi A yoki B bo‘lgan talabalar chiqadi.

**Tushuntirish:** CREATE OR REPLACE yordamida view’ni oson yangilash mumkin.

---

### 4. View’ni o‘chirish
**Vazifa:** student_orders view’ini bazadan o‘chirib tashlang.

**Kod:**
```sql
DROP VIEW student_orders;
```
**Natija:**
```
View "student_orders" o‘chirildi.
```
**Izoh:** student_orders view’i bazadan butunlay o‘chiriladi.

**Tushuntirish:** DROP VIEW yordamida keraksiz view’larni oson o‘chirish mumkin.

---

### 5. View’lar bilan bog‘liq muammolar
**Vazifa:** View’lardan noto‘g‘ri foydalanganda qanday muammolar yuzaga kelishi mumkinligini tushuntiring.

**Tafsif va tushuntirish:**
- View’lar real ma’lumot saqlamaydi, har safar so‘rovda asosiy jadvaldan natija olinadi.
- Juda ko‘p va murakkab view’lar samaradorlikni pasaytirishi mumkin.
- View’lar orqali ba’zi ustunlarni yashirish mumkin, lekin bu xavfsizlikni to‘liq ta’minlamaydi.

**Izoh:** View’lardan foydalanishda ehtiyot bo‘lish, faqat zarur joyda ishlatish va natijalarni doim tekshirish kerak.

---

### 6. Viewda WHERE bilan filtrlash
**Vazifa:** orders jadvalidan faqat miqdori 2 dan katta bo‘lgan buyurtmalarni ko‘rsatuvchi view yarating.

**Kod:**
```sql
CREATE VIEW big_orders AS
SELECT id, student_id, product, amount
FROM orders
WHERE amount > 2;
```
**Natija:**
| id | student_id | product | amount |
|----|------------|---------|--------|
| 2  | 2          | Daftar  | 3      |

**Izoh:** big_orders view’ida faqat miqdori 2 dan katta bo‘lgan buyurtmalar chiqadi.

**Tushuntirish:** WHERE yordamida view’da kerakli ma’lumotlarni filtrlash mumkin.

---

### 7. View orqali ma’lumotlarni tartiblash
**Vazifa:** students jadvalidagi talabalarni bahosi bo‘yicha kamayish tartibida ko‘rsatuvchi view yarating.

**Kod:**
```sql
CREATE VIEW students_by_grade AS
SELECT id, name, grade
FROM students
ORDER BY grade DESC;
```
**Natija:**
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | A     |
| 2  | Vali   | B     |
| 3  | Hasan  | C     |

**Izoh:** students_by_grade view’ida talabalar bahosi bo‘yicha tartiblanadi.

**Tushuntirish:** ORDER BY yordamida view natijasini tartiblash mumkin.

---

### 8. Viewda aggregate funksiyadan foydalanish
**Vazifa:** Har bir talaba nechta buyurtma qilganini ko‘rsatuvchi view yarating.

**Kod:**
```sql
CREATE VIEW student_order_count AS
SELECT s.id, s.name, COUNT(o.id) AS order_count
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name;
```
**Natija:**
| id | name   | order_count |
|----|--------|-------------|
| 1  | Ali    | 1           |
| 2  | Vali   | 1           |
| 3  | Hasan  | 0           |

**Izoh:** student_order_count view’ida har bir talaba nechta buyurtma qilgani ko‘rsatiladi.

**Tushuntirish:** COUNT() va GROUP BY yordamida view’da statistik ma’lumotlarni olish mumkin.

---

## Qo‘shimcha savollar
- View va real jadval o‘rtasidagi farq nima?
- View’larni yangilash va o‘chirishda nimalarga e’tibor berish kerak?
- View’lar yordamida xavfsizlikni qanday oshirish mumkin? 