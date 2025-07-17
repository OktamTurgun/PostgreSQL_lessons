# 📐 Amaliy mashqlar — Lesson 05

## �� Maqsad:
PostgreSQLʼda maʼlumot turlaridan foydalanib ustunlar yaratish va maʼlumotlar kiritishni oʼrganish.

---

## 🔷 Vazifalar:
1⃣ `products` nomli jadval yarating va quyidagi ustunlarni belgilang:
   - `id` (SERIAL, primary key)
   - `nomi` (VARCHAR(100))
   - `narx` (NUMERIC(10,2))
   - `yaratilgan_sana` (DATE)
   - `aktiv` (BOOLEAN)

2⃣ Jadvalga kamida 3 ta yozuv qoʼshing.

3⃣ Yozuvlarni SELECT bilan koʼrib chiqing.

4⃣ Faqat aktiv mahsulotlarni chiqarib koʼring.

5⃣ Yangi mahsulot qoʼshib koʼring.

---

## 💻 Buyruqlar:

### Jadval yaratish va maʼlumot qoʼshish:
```sql
-- Jadval yaratish
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    nomi VARCHAR(100),
    narx NUMERIC(10,2),
    yaratilgan_sana DATE,
    aktiv BOOLEAN
);

-- Maʼlumot qoʼshish
INSERT INTO products (nomi, narx, yaratilgan_sana, aktiv) VALUES
('Telefon', 350.00, '2025-07-16', TRUE),
('Noutbuk', 1200.50, '2025-07-15', FALSE),
('Planshet', 450.75, '2025-07-14', TRUE);

-- Barcha maʼlumotlarni koʼrish
SELECT * FROM products;

-- Faqat aktiv mahsulotlarni koʼrish
SELECT * FROM products WHERE aktiv = TRUE;

-- Yangi mahsulot qoʼshish
INSERT INTO products (nomi, narx, yaratilgan_sana, aktiv) VALUES
('Tish pastasi', 2.50, '2025-07-17', TRUE);
```

---

## 📋 Kutilgan natija:

### Barcha mahsulotlar:
| id | nomi        | narx   | yaratilgan_sana | aktiv |
|----|-------------|--------|-----------------|-------|
| 1  | Telefon     | 350.00 | 2025-07-16      | t     |
| 2  | Noutbuk     | 1200.50| 2025-07-15      | f     |
| 3  | Planshet    | 450.75 | 2025-07-14      | t     |
| 4  | Tish pastasi| 2.50   | 2025-07-17      | t     |

### Faqat aktiv mahsulotlar:
| id | nomi        | narx   | yaratilgan_sana | aktiv |
|----|-------------|--------|-----------------|-------|
| 1  | Telefon     | 350.00 | 2025-07-16      | t     |
| 3  | Planshet    | 450.75 | 2025-07-14      | t     |
| 4  | Tish pastasi| 2.50   | 2025-07-17      | t     |

---

## 🔍 Qoʼshimcha topshiriqlar:
- Har xil maʼlumot turlarida jadvallar yarating (INTEGER, TEXT, TIMESTAMP, JSON)
- Maʼlumot turlarining chegaralarini sinab koʼring
- NOT NULL va DEFAULT qiymatlar bilan ishlang
- Maʼlumot turlarini oʼzgartirishni oʼrganing (ALTER TABLE)
