# 📖 Lesson 21 — View va virtual jadvallar

## 🎯 Maqsad
PostgreSQL’da view (virtual jadval) tushunchasi, ularni yaratish, ishlatish va amaliyotda qo‘llashni o‘rganish.

---

## 1. View nazariyasi

### Nazariya
- **View** — bu SQL so‘rovi natijasiga asoslangan virtual jadval.
- View’lar ma’lumotlarni ko‘rish, murakkab so‘rovlarni soddalashtirish va xavfsizlikni oshirish uchun ishlatiladi.
- View’lar real ma’lumot saqlamaydi, har safar chaqirilganda asosiy jadvaldan natija olinadi.

---

## 2. View yaratish va asosiy sintaksis

### Nazariya
- View’lar yordamida murakkab so‘rovlarni bir nom ostida saqlash mumkin.
- View’lar SELECT so‘rovi asosida yaratiladi.

### Sintaksis
```sql
CREATE VIEW view_nomi AS
SELECT ...
FROM ...
WHERE ...;
```

### Misol: Oddiy view yaratish
#### Avvalgi holat
**students** jadvali:
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | A     |
| 2  | Vali   | B     |
| 3  | Hasan  | C     |

#### Kod
```sql
CREATE VIEW excellent_students AS
SELECT id, name
FROM students
WHERE grade = 'A';
```
#### Natija
**excellent_students** view’idan so‘rov natijasi:
| id | name |
|----|------|
| 1  | Ali  |

**Izoh:** excellent_students view’iga SELECT so‘rovi yuborilsa, faqat bahosi A bo‘lgan talabalar chiqadi.

---

## 3. Murakkab view va JOIN bilan view yaratish

### Nazariya
- View’lar bir nechta jadvalni birlashtirish (JOIN) uchun ham ishlatiladi.

### Misol: JOIN bilan view
#### Avvalgi holat
**students** jadvali:
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | A     |
| 2  | Vali   | B     |

**orders** jadvali:
| id | student_id | product | amount |
|----|------------|---------|--------|
| 1  | 1          | Kitob   | 2      |
| 2  | 2          | Daftar  | 3      |

#### Kod
```sql
CREATE VIEW student_orders AS
SELECT s.name, o.product, o.amount
FROM students s
JOIN orders o ON s.id = o.student_id;
```
#### Natija
**student_orders** view’idan so‘rov natijasi:
| name | product | amount |
|------|---------|--------|
| Ali  | Kitob   | 2      |
| Vali | Daftar  | 3      |

**Izoh:** student_orders view’ida har bir talabaning buyurtmalari ko‘rsatiladi.

---

## 4. View’ni yangilash va o‘chirish

### Nazariya
- View’ni yangilash uchun `CREATE OR REPLACE VIEW` ishlatiladi.
- View’ni o‘chirish uchun `DROP VIEW` ishlatiladi.

### Misol: View’ni yangilash
```sql
CREATE OR REPLACE VIEW excellent_students AS
SELECT id, name, grade
FROM students
WHERE grade IN ('A', 'B');
```
#### Natija
**excellent_students** view’idan so‘rov natijasi:
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | A     |
| 2  | Vali   | B     |

**Izoh:** Endi view’da bahosi A yoki B bo‘lgan talabalar chiqadi.

### Misol: View’ni o‘chirish
```sql
DROP VIEW student_orders;
```
#### Natija
```
View "student_orders" o‘chirildi.
```
**Izoh:** student_orders view’i bazadan butunlay o‘chiriladi.

---

## 5. View’lar bilan bog‘liq muammolar va best practices
- View’lar real ma’lumot saqlamaydi, har safar so‘rovda asosiy jadvaldan natija olinadi
- View’lar yordamida murakkab so‘rovlarni soddalashtirish mumkin
- View’larni haddan tashqari ko‘p va murakkab yaratishdan ehtiyot bo‘ling — samaradorlikka ta’sir qilishi mumkin
- View’lar orqali ma’lumotlarni yashirish va xavfsizlikni oshirish mumkin

---

## 6. Xulosa
- View’lar yordamida murakkab so‘rovlarni soddalashtirish va xavfsizlikni oshirish mumkin
- View’lar virtual jadval bo‘lib, real ma’lumot saqlamaydi
- View’larni yangilash va o‘chirish oson

---

## 📌 Keyingi dars:
[Lesson 22 — Stored procedure va functionlar](../lesson_22/lesson.md) 