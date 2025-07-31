# 🧪 Amaliyot: PostgreSQL — Backup va Restore

---

## 1. 🔧 SQL Dump yordamida backup yaratish

### 1.1. Quyidagi buyruq orqali `bookstore` bazasini `bookstore.sql` faylga zaxiralang:

```bash
pg_dump -U postgres -d bookstore -f bookstore.sql
```

> 🧠 Eslatma: `postgres` o‘rniga o‘z user nomingizni yozing.

---

## 2. 🏗 Yangi baza yaratish

### 2.1. `bookstore_restored` nomli yangi baza yarating:

```bash
createdb -U postgres bookstore_restored
```

---

## 3. 📤 SQL dump fayldan tiklash

```bash
psql -U postgres -d bookstore_restored -f bookstore.sql
```

✅ Tiklangandan so‘ng `bookstore_restored` bazasida barcha ma’lumotlar bo‘lishi kerak.

---

## 4. 🎒 Custom Format backup

```bash
pg_dump -U postgres -d bookstore -F c -f bookstore.backup
```

---

## 5. 📥 Custom Format restore qilish

```bash
pg_restore -U postgres -d bookstore_restored bookstore.backup
```

---

## 6. 🧪 Qo‘shimcha mashq

### Quyidagi mashqlarni bajaring:

- [ ] `pg_dump` orqali har kuni avtomatik zaxira olish uchun bash script yozing.
- [ ] `.sql.gz` formatda siqilgan backup yaratib tiklang.
- [ ] `pg_restore` bilan parallel jarayonni sinab ko‘ring (`-j 4`).

---

## ✅ Tekshiruv:

Yuqoridagi har bir bosqichdan so‘ng `\dt`, `SELECT * FROM ...` orqali bazadagi jadvallar va ma’lumotlar tiklanganini tekshiring.

---

📌 Eslatma:
Agar `pg_dump` yoki `pg_restore` buyruqlari ishlamasa, `PostgreSQL` binariy joylashgan katalogga yo‘l qo‘shilganini tekshiring yoki to‘liq yo‘lni yozing:
```bash
"C:\Program Files\PostgreSQL\16\bin\pg_dump.exe"
```

---

🏁 Amaliyot tugadi! Endi siz PostgreSQL'da professional darajada backup va restore qilishni bilasiz.