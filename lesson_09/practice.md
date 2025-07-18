# 📐 Amaliy mashqlar — Lesson 09

## 🎯 Maqsad:
SELECT buyrugʼining asosiy sintaksisi va undan amalda foydalanishni oʼrganish.

---

## 🔷 Vazifalar:
1⃣ students jadvalini yarating va maʼlumotlar kiriting  
2⃣ SELECT yordamida barcha maʼlumotlarni koʼring  
3⃣ Faqat kerakli ustunlarni tanlang  
4⃣ WHERE bilan filtrlash  
5⃣ ORDER BY bilan tartiblash  
6⃣ LIMIT bilan natijani cheklash

---

## 💻 Buyruqlar:

### 1. Jadval yaratish va maʼlumot kiritish:
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INTEGER,
    grade VARCHAR(2)
);

INSERT INTO students (name, age, grade) VALUES
('Ali Valiyev', 21, 'A'),
('Gulbahor Karimova', 19, 'B'),
('Aziz Toshmatov', 22, 'A'),
('Malika Yusupova', 18, 'C'),
('Jasur Turgunov', 20, 'B');
```

### 2. Barcha maʼlumotlarni koʼrish:
```sql
SELECT * FROM students;
```

### 3. Faqat kerakli ustunlarni tanlash:
```sql
SELECT name, grade FROM students;
```

### 4. WHERE bilan filtrlash:
```sql
SELECT * FROM students WHERE age > 20;
SELECT name FROM students WHERE grade = 'A';
```

### 5. ORDER BY bilan tartiblash:
```sql
SELECT * FROM students ORDER BY age;
SELECT name, grade FROM students ORDER BY grade DESC;
```

### 6. LIMIT bilan natijani cheklash:
```sql
SELECT * FROM students LIMIT 3;
```

---

## 📋 Kutilgan natija:

| id | name               | age | grade |
|----|--------------------|-----|-------|
| 1  | Ali Valiyev        | 21  | A     |
| 2  | Gulbahor Karimova  | 19  | B     |
| 3  | Aziz Toshmatov     | 22  | A     |
| 4  | Malika Yusupova    | 18  | C     |
| 5  | Jasur Turgunov     | 20  | B     |

---

## 🔍 Qoʼshimcha topshiriqlar:
- Faqat grade = 'B' boʼlgan talabalarni koʼring
- Eng yosh talabani toping (ORDER BY + LIMIT)
- Ustunlarga nom bering (AS)
- Faqat 2 ta eng yuqori yoshli talabani koʼring 