# 📖 Git Darslari — Lesson 02: Commit va o'zgarishlar

## 🎯 Maqsad
Git'da o'zgarishlarni saqlash (commit) va boshqarish jarayonini o'rganish.

---

## 📖 Git workflow (Ish jarayoni)

### Git'da 3 asosiy holat:
1. **Working Directory** — fayllar ustida ishlash
2. **Staging Area** — commit uchun tayyorlash
3. **Repository** — saqlangan o'zgarishlar

```
Working Directory → Staging Area → Repository
     (ish)           (tayyorlash)    (saqlash)
```

---

## 🔷 Asosiy buyruqlar

### 1. Holatni ko'rish
```bash
git status
```

**Natija:**
- `Untracked files` — yangi fayllar
- `Changes not staged` — o'zgartirilgan fayllar
- `Changes to be committed` — tayyor commit

### 2. Fayllarni staging area'ga qo'shish
```bash
# Bitta fayl qo'shish
git add filename.txt

# Barcha fayllarni qo'shish
git add .

# Faqat o'zgartirilgan fayllarni qo'shish
git add -u
```

### 3. Commit qilish
```bash
# Oddiy commit
git commit -m "O'zgarishlar haqida xabar"

# Barcha o'zgarishlarni bir vaqtda commit qilish
git add . && git commit -m "Barcha o'zgarishlar"
```

---

## 🔷 Amaliy mashg'ulot

### 1. Yangi fayl yaratish va commit qilish:
```bash
# Yangi fayl yaratish
echo "Bu mening birinchi faylim" > first_file.txt

# Holatni ko'rish
git status

# Faylni staging area'ga qo'shish
git add first_file.txt

# Holatni qayta ko'rish
git status

# Commit qilish
git commit -m "Birinchi fayl qo'shildi"
```

### 2. Faylni o'zgartirish:
```bash
# Faylni o'zgartirish
echo "Bu yangilangan matn" > first_file.txt

# Holatni ko'rish
git status

# O'zgarishlarni qo'shish va commit qilish
git add first_file.txt
git commit -m "Fayl yangilandi"
```

### 3. Bir nechta fayl bilan ishlash:
```bash
# Bir nechta fayl yaratish
echo "Fayl 1" > file1.txt
echo "Fayl 2" > file2.txt
echo "Fayl 3" > file3.txt

# Barcha fayllarni qo'shish
git add .

# Commit qilish
git commit -m "3 ta yangi fayl qo'shildi"
```

---

## 📋 Commit xabarlari yozish

### Yaxshi commit xabarlari:
```bash
git commit -m "README.md faylini yangiladi"
git commit -m "Xatolarni tuzatdi"
git commit -m "Yangi funksiya qo'shildi"
git commit -m "Kodni optimallashtirdi"
```

### Yomon commit xabarlari:
```bash
git commit -m "o'zgarishlar"
git commit -m "fix"
git commit -m "update"
```

---

## 🔷 Tarixni ko'rish

### 1. Commit tarixini ko'rish:
```bash
# Qisqa tarix
git log --oneline

# Batafsil tarix
git log

# Grafik tarix
git log --graph --oneline --all
```

### 2. Oxirgi commit haqida ma'lumot:
```bash
# Oxirgi commit
git show

# Belgilangan commit
git show <commit_hash>
```

---

## 🔷 Fayllarni o'chirish

### 1. Faylni o'chirish va commit qilish:
```bash
# Faylni o'chirish
git rm filename.txt

# Commit qilish
git commit -m "Fayl o'chirildi"
```

### 2. Faylni saqlab qolish, lekin Git'dan olib tashlash:
```bash
# Faylni Git'dan olib tashlash, lekin saqlab qolish
git rm --cached filename.txt

# Commit qilish
git commit -m "Fayl Git'dan olib tashlandi"
```

---

## 📌 Asosiy buyruqlar jadvali

| Buyruq | Ma'nosi | Misol |
|--------|---------|-------|
| `git status` | Holatni ko'rish | `git status` |
| `git add` | Staging area'ga qo'shish | `git add filename.txt` |
| `git commit` | O'zgarishlarni saqlash | `git commit -m "Xabar"` |
| `git log` | Tarixni ko'rish | `git log --oneline` |
| `git rm` | Faylni o'chirish | `git rm filename.txt` |

---

## 🎯 Dars yakunida bilishingiz kerak:

✅ Git workflow (ish jarayoni)  
✅ Staging area tushunchasi  
✅ add va commit buyruqlari  
✅ Yaxshi commit xabarlari yozish  
✅ Tarixni ko'rish va boshqarish  

---

## 📚 Keyingi dars:
[Lesson 03 — Branch va boshqarish](../lesson_03/lesson.md)

---

## 🎯 Uy vazifasi:
1. Yangi repository yarating
2. 3 ta fayl yarating va commit qiling
3. Fayllarni o'zgartiring va yangi commit qiling
4. Tarixni ko'ring 