## 📐 `practice_04.md`

```markdown
# 📐 Amaliy mashqlar — Lesson 4## 🎯 Maqsad:
PostgreSQLʼda yangi maʼlumotlar bazasi yaratish va unga ulanishni amalda bajarish.

---

## 🔷 Vazifalar:
1⃣ PostgreSQLʼga ulaning (psql yoki pgAdmin orqali) 2 `my_first_db` nomli baza yarating  
3 Baza ichiga kirib uni tekshirib koʼring  4Yaratilgan bazalar roʼyxatini chiqarib koʼring  
5ana bitta test bazasi yarating va uni oʼchirib tashlang

---

## 💻 Buyruqlar:

### SQL orqali:
```sql
-- Maʼlumotlar bazasi yaratish
CREATE DATABASE my_first_db;

-- Bazalar roʼyxatini koʼrish
\l

-- Bazaga ulanish
\c my_first_db

-- Yana bitta test bazasi yaratish
CREATE DATABASE test_db;

-- Test bazasini oʼchirish
DROP DATABASE test_db;
```

### CLI orqali:
```bash
-- Maʼlumotlar bazasini yaratish
createdb my_first_db

-- Bazaga ulanish
psql -d my_first_db

-- Bazani oʼchirish (agar kerak boʼlsa)
dropdb my_first_db
```

---

## 📋 Kutilgan natija:
✅ `my_first_db` nomli baza yaratilgan boʼladi  
✅ `\l` orqali roʼyxatda koʼrinasiz  
✅ `\c my_first_db` orqali ulanish amalga oshadi  
✅ Test bazasi yaratiladi va oʼchiriladi

---

## 🔍 Qoʼshimcha topshiriqlar:
- Har xil nomdagi 2-3 ta baza yarating
- Ularni roʼyxatini koʼring
- Keraksiz bazalarni oʼchirib tashlang
- Bazalar haqida maʼlumot olishni oʼrganing (`\l+` buyrugʼi bilan)
