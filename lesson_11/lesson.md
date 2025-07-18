# 📖 Lesson 11 — AND, OR, NOT operatorlari

## 🎯 Maqsad
PostgreSQLʼda mantiqiy operatorlar (AND, OR, NOT) yordamida murakkab shartlar bilan soʼrovlar tuzishni oʼrganish.

---

## 📖 Nazariya

Mantiqiy operatorlar yordamida bir nechta shartlarni birlashtirib, aniq va murakkab soʼrovlar yozish mumkin.

- **AND** — barcha shartlar bajarilganda natija qaytaradi
- **OR** — kamida bitta shart bajarilganda natija qaytaradi
- **NOT** — shart natijasini teskarisiga oʼzgartiradi

---

## 🔷 Sintaksis va asosiy misollar

### 📋 AND operatori
```sql
SELECT * FROM students WHERE age > 18 AND grade = 'A';
```
**Izoh:** Ikkala shart ham bajarilishi kerak.

### 📋 OR operatori
```sql
SELECT * FROM students WHERE grade = 'A' OR grade = 'B';
```
**Izoh:** Kamida bitta shart bajarilsa, natija chiqadi.

### 📋 NOT operatori
```sql
SELECT * FROM students WHERE NOT (grade = 'C');
```
**Izoh:** grade 'C' boʼlmaganlar chiqadi.

---

## 🔷 Bir nechta operatorlarni birlashtirish

```sql
SELECT * FROM students WHERE (grade = 'A' OR grade = 'B') AND age >= 20;
SELECT * FROM students WHERE NOT (age < 18 OR grade = 'C');
```

---

## 🔷 Amaliy maslahatlar
- Qavslar yordamida shartlar ustuvorligini boshqaring
- AND va OR ni birga ishlatganda, qavsdan foydalaning
- NOT operatori bilan shartlarni teskarisiga oʼgiring

---

## 📌 Eng koʼp ishlatiladigan mantiqiy operatorlar
✅ `AND` — bir nechta shartlar bajarilganda  
✅ `OR` — kamida bitta shart bajarilganda  
✅ `NOT` — shart natijasini teskarisiga oʼzgartirish

---

## 📌 Keyingi dars:
[Lesson 12 — LIKE, ILIKE, BETWEEN, IN, IS NULL](../lesson_12/lesson.md) 