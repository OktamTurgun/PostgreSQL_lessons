# 📖 Lesson 05 — Maʼlumot turlari

## 🎯 Maqsad
PostgreSQLʼda mavjud maʼlumot turlari bilan tanishish va ulardan toʼgʼri foydalanishni oʼrganish.

---

## 📖 Nazariya

PostgreSQL juda boy va kuchli maʼlumot turlarini qoʼllab-quvvatlaydi.  
Maʼlumot turi ustunlar (columns) uchun belgilanadi va qaysi turdagi maʼlumot saqlanishini belgilaydi.

**Maʼlumot turi nima uchun muhim?**
- Maʼlumotlarni toʼgʼri saqlash
- Xotiradan tejash
- Tezlikni oshirish
- Xatolarni oldini olish

---

## 🔷 Asosiy maʼlumot turlari

### 📋 Sonli turlar
| Turi       | Tavsif                       | Misol  | Xotiradan joy |
|------------|-----------------------------|--------|---------------|
| `INTEGER`  | Butun son                   | 42     | 4 bayt        |
| `SERIAL`   | Avtomatik oshib boruvchi    | 1,2,3… | 4 bayt        |
| `BIGINT`   | Katta butun son            | 9223372036854775807 | 8 bayt |
| `DECIMAL`  | Aniqligi yuqori son         | 10.50  | Oʼzgaruvchan   |
| `NUMERIC`  | Pul kabi aniqlik uchun     | 99.99  | Oʼzgaruvchan   |
| `REAL`     | Haqiqiy son (float)        | 3.14   | 4 bayt        |

**Qachon qaysi sonli tur?**
- Oson sonlar uchun → `INTEGER`
- Avtomatik ID uchun → `SERIAL`
- Pul hisoblar uchun → `NUMERIC(10,2)`
- Katta sonlar uchun → `BIGINT`

---

### 📋 Matn turlari
| Turi         | Tavsif                 | Misol       | Maksimal uzunlik |
|--------------|-----------------------|-------------|------------------|
| `TEXT`       | Cheksiz matn          | "Salom"     | Cheksiz          |
| `CHAR(n)`    | Belgilangan uzunlik   | "A"         | n belgi          |
| `VARCHAR(n)` | Maksimal uzunlik      | "Hello"     | n belgi          |

**Qachon qaysi matn turi?**
- Oʼzgaruvchan uzunlik → `TEXT` yoki `VARCHAR`
- Belgilangan uzunlik → `CHAR`
- Qisqa matnlar → `VARCHAR(50)`
- Uzun matnlar → `TEXT`

---

### 📋 Sana va vaqt
| Turi            | Tavsif                  | Misol               | Format |
|-----------------|------------------------|---------------------|--------|
| `DATE`          | Sana                   | 2025-07-16          | YYYY-MM-DD |
| `TIME`          | Vaqt                   | 14:30:00            | HH:MM:SS |
| `TIMESTAMP`     | Sana + Vaqt            | 2025-07-16 14:30:00 | YYYY-MM-DD HH:MM:SS |
| `INTERVAL`      | Vaqt oraligʼi          | 2 hours             | Oʼzgaruvchan |

**Qachon qaysi vaqt turi?**
- Faqat sana → `DATE`
- Faqat vaqt → `TIME`
- Sana va vaqt → `TIMESTAMP`
- Vaqt oraligʼi → `INTERVAL`

---

### 📋 Boolean
| Turi      | Tavsif           | Misol | Qiymatlar |
|-----------|-----------------|-------|-----------|
| `BOOLEAN` | True/False qiymat | TRUE  | TRUE, FALSE, NULL |

**Boolean qachon ishlatiladi?**
- Aktiv/passiv holatlar
- Ha/yoʼq savollari
- Bayroqlar (flags)

---

### 📋 Boshqa muhim turlar
| Turi    | Tavsif                    | Misol |
|---------|---------------------------|-------|
| `UUID`   | Universally Unique ID    | 550e8400-e29b-41d4-a716-446655440000 |
| `JSON`   | JavaScript Object Notation | {"name": "Ali", "age": 25} |
| `ARRAY`  | Massiv                    | {1,2,3,4,5} |
| `BYTEA`  | Binary maʼlumot          | Binary data |

---

### 📌 Eng koʼp ishlatiladigan turlar
✅ **ID uchun** — `SERIAL` yoki `UUID`  
✅ **Matn uchun** — `TEXT` yoki `VARCHAR`  
✅ **Pul uchun** — `NUMERIC(10,2)`  
✅ **Sana uchun** — `DATE` yoki `TIMESTAMP`  
✅ **Bayroq uchun** — `BOOLEAN`

---

## 📌 Keyingi dars:
[Lesson 06 — Foydali buyruqlar](../lesson_06/lesson.md)