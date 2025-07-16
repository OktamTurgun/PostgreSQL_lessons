# 📖 Lesson 03 — Maʼlumotlar va Jadvallar

## 🎯 Maqsad
PostgreSQL’da maʼlumotlar va ularni jadvallar ko‘rinishida saqlash asoslarini tushunish.

---

## 📖 Nazariya

Maʼlumotlar bazasi (DB) — maʼlumotlarni tartiblangan va bog‘langan holatda saqlash imkonini beruvchi tizim.

PostgreSQL’da maʼlumotlar **jadvallar (tables)** ichida saqlanadi.  
Jadval — bu satrlar (qatorlar, *rows*) va ustunlardan (*columns*) iborat.

### Jadvalning tarkibi:
✅ Ustun (column) — maʼlumot turi va nomiga ega.  
✅ Qator (row) — bir butun yozuv.  
✅ Primary Key — jadvaldagi qatorni unikal aniqlovchi ustun. Primary Key har bir qator uchun yagona (takrorlanmas) qiymatga ega bo‘lishi kerak va ko‘pincha identifikator sifatida ishlatiladi. Primary Key bo‘lgan ustunda NULL qiymat bo‘lishi mumkin emas.

**Primary Key misoli:**
| id (Primary Key) | ism     | yosh |
|------------------|---------|------|
| 1                | Ali     | 25   |
| 2                | Vali    | 30   |

Bu yerda `id` ustuni Primary Key bo‘lib, har bir qator uchun unikal qiymatga ega.

---

## 📋 Misol Jadval:
| id  | ism     | yosh |
|-----|---------|------|
| 1   | Ali     | 25   |
| 2   | Vali    | 30   |

Bu jadvalda:
- `id` — unikal identifikator (Primary Key)
- `ism` — foydalanuvchi ismi
- `yosh` — foydalanuvchi yoshi

---

### SQL buyruqlari va misollar:

#### Jadval yaratish: `CREATE TABLE`
```sql
CREATE TABLE foydalanuvchilar (
  id SERIAL PRIMARY KEY,
  ism VARCHAR(50),
  yosh INT
);
```

#### Jadvalga maʼlumot qoʻshish: `INSERT INTO`
```sql
INSERT INTO foydalanuvchilar (ism, yosh) VALUES ('Ali', 25);
INSERT INTO foydalanuvchilar (ism, yosh) VALUES ('Vali', 30);
```

#### Jadvaldagi maʼlumotni o‘chirish: `DELETE FROM`
```sql
DELETE FROM foydalanuvchilar WHERE id = 1;
```

#### Jadvaldagi maʼlumotni yangilash: `UPDATE`
```sql
UPDATE foydalanuvchilar SET yosh = 26 WHERE id = 1;
```

---

## 📌 Keyingi dars:
[Lesson 04 — Maʼlumotlar bazasini yaratish](../lesson_04/lesson.md)