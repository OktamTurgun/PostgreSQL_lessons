
# 📐 Amaliy mashqlar — Lesson 02

## 🎯 Maqsad:
Windows’da PostgreSQL’ni o‘rnatish va ishga tushirishni amalda bajarish.

---

## 🔷 Vazifalar:
1️⃣ PostgreSQL rasmiy saytiga kiring: [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/)  
2️⃣ Installer faylini yuklab oling.  
3️⃣ Installer’ni ishga tushiring va quyidagi qadamlarni bajaring:
   - `Next` tugmalarini bosing  
   - Data Directory-ni qoldiring  
   - Superuser uchun parol yarating  
   - Portni (5432) o‘zgartirmasdan davom eting  
   - pgAdmin va Command Line Tools’larni belgilab qo‘ying  
   - `Install` tugmasini bosing

4️⃣ O‘rnatish tugagach, pgAdmin va psql ishga tushayotganini tekshirib ko‘ring.

---

## 💻 Tekshirish:
### Command Prompt ochib quyidagilarni yozing:
```cmd
psql --version
```

### pgAdmin’ni ishga tushirib, browser orqali kiring:
```
http://localhost:5050/
```

---

## 📋 Kutilgan natija:
```text
psql (PostgreSQL) 16.2
```

✅ pgAdmin ochiladi va serverga ulanishni so‘raydi.

---

## 📌 Qo‘shimcha topshiriqlar:
✅ O‘rnatish jarayonida belgilagan parolingizni xavfsiz joyga yozib qo‘ying.  
✅ `postgres` foydalanuvchi nomi bilan ulanishni sinab ko‘ring.  
✅ pgAdmin’da yangi ma’lumotlar bazasi yaratib ko‘ring.

---

## 📝 Qayd:
Agar `psql` buyruqlari ishlamasa:
— Kompyuterni qayta yoqing  
— PATH o‘zgaruvchilarini tekshiring  
— Administrator sifatida CMD ochib ko‘ring
