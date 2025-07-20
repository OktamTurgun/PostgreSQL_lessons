# 📘 Git Darslari — Terminalda mustaqil ishlash

Ushbu repozitoriy — Git versiya boshqaruvi tizimini o'zbek tilida bosqichma-bosqich o'rganish uchun to'liq darslar to'plami.

## 📚 Tuzilma

Har bir dars alohida fayl sifatida joylashgan va quyidagi mavzularni o'z ichiga oladi:
- `lesson_01_kirish.md` — Git asoslari va o'rnatish
- `lesson_02_commit.md` — Commit va o'zgarishlar
- `lesson_03_branch.md` — Branch va boshqarish
- `lesson_04_github.md` — GitHub va remote repository

## 🚀 Boshlash

1. Repozitoriyani yuklab oling:
   ```sh
   git clone https://github.com/OktamTurgun/PostgreSQL_lessons.git
   cd PostgreSQL_lessons/git_lessons
   ```

2. Har bir dars faylini o'qing va terminalda amaliyotlarni bajaring.

## 📋 Darslar ro'yxati

- [Lesson 01 — Kirish va o'rnatish](lesson_01_kirish.md)  
  *Git tushunchasi, o'rnatish va birinchi sozlashlar.*
- [Lesson 02 — Commit va o'zgarishlar](lesson_02_commit.md)  
  *Git workflow, staging area va commit jarayoni.*
- [Lesson 03 — Branch va boshqarish](lesson_03_branch.md)  
  *Branch yaratish, merge va conflict hal qilish.*
- [Lesson 04 — GitHub va remote repository](lesson_04_github.md)  
  *GitHub bilan ishlash va jamoa bilan ishlash.*

## 🎯 O'rganiladigan mavzular

### Asosiy Git tushunchalari
- ✅ Git nima va nima uchun kerak
- ✅ Repository tushunchasi
- ✅ Working Directory, Staging Area, Repository
- ✅ Commit va commit xabarlari

### Branch va boshqarish
- ✅ Branch yaratish va boshqarish
- ✅ Merge jarayoni
- ✅ Conflict hal qilish
- ✅ Branch nomlash konventsiyasi

### Remote repository
- ✅ GitHub bilan ishlash
- ✅ Push va pull jarayoni
- ✅ Fork va Pull Request
- ✅ Jamoa bilan ishlash

## 🔧 Terminal buyruqlari

### Asosiy buyruqlar:
```bash
# Git o'rnatilganini tekshirish
git --version

# Repository yaratish
git init

# Holatni ko'rish
git status

# O'zgarishlarni qo'shish
git add .

# Commit qilish
git commit -m "O'zgarishlar haqida xabar"

# Tarixni ko'rish
git log --oneline
```

### Branch bilan ishlash:
```bash
# Branch'lar ro'yxatini ko'rish
git branch

# Yangi branch yaratish
git checkout -b yangi-branch

# Branch'ga o'tish
git checkout branch-nomi

# Branch'ni merge qilish
git merge branch-nomi
```

### GitHub bilan ishlash:
```bash
# Remote repository'ni qo'shish
git remote add origin URL

# O'zgarishlarni yuklash
git push origin main

# O'zgarishlarni yuklab olish
git pull origin main

# Repository'ni klonlash
git clone URL
```

## 🎯 Amaliy mashg'ulotlar

### Har bir darsda:
- ✅ Nazariy ma'lumotlar
- ✅ Amaliy misollar
- ✅ Terminal buyruqlari
- ✅ Uy vazifalari
- ✅ Keyingi darsga tayyorgarlik

## 📋 Foydali maslahatlar

### Commit xabarlari yozish:
```bash
# Yaxshi commit xabarlari
git commit -m "README.md faylini yangiladi"
git commit -m "Xatolarni tuzatdi"
git commit -m "Yangi funksiya qo'shildi"

# Yomon commit xabarlari
git commit -m "o'zgarishlar"
git commit -m "fix"
```

### Branch nomlash:
```bash
# Yaxshi branch nomlari
git checkout -b feature/yangi-funksiya
git checkout -b bugfix/xatoni-tuzatish
git checkout -b hotfix/urgent-tuzatish

# Yomon branch nomlari
git checkout -b branch1
git checkout -b test
```

## 🤝 Hissa qo'shish

Taklif va tuzatishlar uchun pull request yoki issue qoldirishingiz mumkin.

---

**Loyiha muallifi:**  
[OktamTurgun](https://github.com/OktamTurgun)

---

## 📚 Qo'shimcha manbalar

- [Git rasmiy hujjati](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) 