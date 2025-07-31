# 📦 PostgreSQL Darsi — Lesson 26: Backup va Restore

---

## 🎯 Maqsad:
Ushbu darsda siz PostgreSQL ma’lumotlar bazasini qanday qilib **zaxiralash (backup)** va keyinchalik qanday **tiklash (restore)** mumkinligini o‘rganasiz.

---

## 🧩 1. Backup va Restore nima?

- **Backup** — bu ma’lumotlar bazasining nusxasini saqlab qo‘yishdir. Bunday nusxa tizim nosozligi, xatoliklar yoki foydalanuvchi xatolari yuz bersa, ma’lumotlarni tiklash imkonini beradi.
- **Restore** — bu oldindan yaratilgan backup fayldan ma’lumotlar bazasini qayta tiklash jarayonidir.

---

## 📦 2. PostgreSQL-da Backup turlari

| Tur | Tavsif |
|-----|--------|
| 📄 SQL Dump | Ma’lumotlar va strukturani `.sql` faylga saqlaydi. |
| 🗃 Custom Format | `.backup` fayl formatida. `pg_dump` va `pg_restore` orqali ishlatiladi. |
| 💾 File System Level | Fayl tizimi nusxasi (odatda xizmatni to‘xtatib olinadi). |

---

## 🔧 3. SQL Dump yordamida Backup yaratish

### 🛠 Buyruq:
```bash
pg_dump -U postgres -d mydb -f backup.sql
```

### 📝 Izoh:
- `-U postgres` — foydalanuvchi nomi.
- `-d mydb` — bazaning nomi.
- `-f backup.sql` — chiqariladigan fayl nomi.

---

## 🧾 4. SQL Dump yordamida Restore qilish

### 🛠 Buyruq:
```bash
psql -U postgres -d mydb_restored -f backup.sql
```

### 📌 Muhim:
`mydb_restored` bazasini avvaldan yaratib qo‘yishingiz kerak:
```bash
createdb -U postgres mydb_restored
```

---

## 📁 5. Custom Format Backup

### 🛠 Buyruq:
```bash
pg_dump -U postgres -d mydb -F c -f mydb.backup
```

- `-F c` — custom format.

---

## 📥 6. Custom Format Restore qilish

### 🛠 Buyruq:
```bash
pg_restore -U postgres -d mydb_restored mydb.backup
```

Yoki parallel jarayon uchun:
```bash
pg_restore -U postgres -d mydb_restored -j 4 mydb.backup
```

---

## 📦 7. Faylni siqib saqlash

```bash
pg_dump -U postgres mydb | gzip > mydb.sql.gz
```

Tiklash:
```bash
gunzip < mydb.sql.gz | psql -U postgres -d mydb_restored
```

---

## 🛡️ 8. Real Hayot Maslahati

- Har kuni avtomatik backup sozlang (cron + bash script).
- Har hafta backup faylni bulutga yuklang (Dropbox, S3).
- Restore qilishni test qilib boring — zaxirani tekshirmasdan unga ishonib bo‘lmaydi.

---

## 📚 Qo‘shimcha manbalar:
- https://www.postgresql.org/docs/current/backup.html
- https://www.postgresql.org/docs/current/app-pgdump.html

---

✅ Endi amaliy mashqlarni bajaring:  
[➡️ practice.md faylga o‘ting](practice.md)