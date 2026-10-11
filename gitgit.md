# Git va GitHub buyruqlari

Barcha buyruqlar terminalda loyiha papkasi ichida ishga tushiriladi
(VS Code: **Terminal → New Terminal**).

---

## 1. Bir martalik sozlash (har bir kompyuterda)

| Buyruq | Nima qiladi |
|---|---|
| `git --version` | Git o'rnatilganini tekshiradi |
| `git config --global user.name "Fayzulla"` | Ismingizni sozlaydi |
| `git config --global user.email "email@example.com"` | Emailingizni sozlaydi |
| `git config --global --list` | Barcha sozlamalarni ko'rsatadi |
| `git config --global init.defaultBranch main` | Yangi loyihalarda asosiy branch `main` bo'ladi |

---

## 2. Loyihani boshlash

| Buyruq | Nima qiladi |
|---|---|
| `git init` | Joriy papkada yangi git loyiha yaratadi |
| `git clone https://github.com/USER/REPO.git` | GitHub'dagi loyihani kompyuterga yuklab oladi |
| `git remote add origin https://github.com/USER/REPO.git` | Loyihani GitHub repo bilan bog'laydi |
| `git remote -v` | Qaysi GitHub repoga bog'langanini ko'rsatadi |

> Bo'sh loyihani push qilib bo'lmaydi — avval kamida bitta commit kerak.

---

## 3. Har kunlik ish (eng kerakli)

| Buyruq | Nima qiladi |
|---|---|
| `git pull` | GitHub'dagi yangi o'zgarishlarni yuklab oladi |
| `git status` | Qaysi fayllar o'zgarganini ko'rsatadi |
| `git add fayl.txt` | Bitta faylni commitga tayyorlaydi |
| `git add .` | Barcha o'zgargan fayllarni tayyorlaydi |
| `git commit -m "Xabar"` | O'zgarishlarni kompyuterda saqlaydi |
| `git push` | Commitlarni GitHub'ga yuboradi |
| `git push -u origin main` | Birinchi marta push (branchni GitHub bilan bog'laydi) |

**Tartib:**

```bash
git pull
# ... ishlaysiz ...
git add .
git commit -m "Nima qildim"
git push
```

> Commit = faqat kompyuterda saqlash. Push = GitHub'ga yuborish.
> Boshqa kompyuterga o'tirganda **birinchi** `git pull`.

---

## 4. Tarix va o'zgarishlarni ko'rish

| Buyruq | Nima qiladi |
|---|---|
| `git log --oneline` | Commitlar tarixi (qisqa) |
| `git log --oneline --graph --all` | Tarixni daraxt ko'rinishida |
| `git diff` | Hali `add` qilinmagan o'zgarishlar |
| `git diff --staged` | `add` qilingan, lekin commit qilinmagan o'zgarishlar |
| `git show <commit>` | Bitta commitda nima o'zgarganini ko'rsatadi |
| `git fetch` | GitHub'dagi yangiliklarni tekshiradi (fayllarga tegmaydi) |
| `git status -sb` | Qisqa holat + GitHub'dan necha commit oldinda/orqada |

---

## 5. Xatolarni tuzatish

| Buyruq | Nima qiladi |
|---|---|
| `git restore fayl.txt` | Faylni oxirgi commitdagi holatiga qaytaradi (o'zgarish yo'qoladi!) |
| `git restore --staged fayl.txt` | Faylni `add` dan chiqaradi (o'zgarish qoladi) |
| `git commit --amend -m "Yangi xabar"` | Oxirgi commit xabarini o'zgartiradi (push qilinmagan bo'lsa) |
| `git revert <commit>` | Commitni bekor qiluvchi yangi commit yaratadi (xavfsiz) |
| `git mv eski.txt yangi.txt` | Fayl nomini o'zgartiradi |
| `git rm fayl.txt` | Faylni o'chiradi va buni gitga bildiradi |

> `git reset --hard` va `git push --force` — ishni butunlay o'chirib yuborishi mumkin.
> Nima qilayotganingizni aniq bilmasangiz ishlatmang.

---

## 6. Branchlar (shoxlar)

| Buyruq | Nima qiladi |
|---|---|
| `git branch` | Barcha branchlar ro'yxati |
| `git switch -c yangi-branch` | Yangi branch yaratib, unga o'tadi |
| `git switch main` | `main` branchga qaytadi |
| `git merge yangi-branch` | Branchdagi o'zgarishlarni joriy branchga qo'shadi |
| `git branch -d yangi-branch` | Branchni o'chiradi (merge qilingan bo'lsa) |
| `git push -u origin yangi-branch` | Branchni GitHub'ga yuboradi |

---

## 7. Vaqtincha saqlash (stash)

| Buyruq | Nima qiladi |
|---|---|
| `git stash` | Tugallanmagan ishni vaqtincha chetga qo'yadi |
| `git stash pop` | Chetga qo'yilgan ishni qaytaradi |
| `git stash list` | Saqlangan ishlar ro'yxati |

Foydali holat: `git pull` "o'zgarishlaringiz bor" deb xato bersa →
`git stash` → `git pull` → `git stash pop`.

---

## 8. GitHub CLI (`gh`)

O'rnatish: Windows — `winget install GitHub.cli`, Mac — `brew install gh`.

| Buyruq | Nima qiladi |
|---|---|
| `gh auth login` | GitHub'ga kirish |
| `gh auth status` | Kirilganmi yoki yo'qmi tekshiradi |
| `gh repo create NOM --private --source . --push` | GitHub'da private repo yaratib, kodni yuklaydi |
| `gh repo clone USER/REPO` | Repoyni yuklab oladi |
| `gh repo list` | Barcha repolaringiz ro'yxati |
| `gh repo view --web` | Joriy repoyni brauzerda ochadi |
| `gh pr create` | Pull request yaratadi |
| `gh pr list` | Ochiq pull requestlar |
| `gh issue list` | Issue (vazifa) lar ro'yxati |

---

## 9. `.gitignore` — gitga kirmasligi kerak bo'lgan fayllar

Loyiha papkasida `.gitignore` faylini yarating va ichiga yozing:

```
.env
__pycache__/
.venv/
node_modules/
*.log
```

> Parollar, API kalitlar (`.env`) hech qachon GitHub'ga yuklanmasin.

---

## 10. Ko'p uchraydigan xatolar

| Xato | Sabab va yechim |
|---|---|
| `src refspec main does not match any` | Hali commit yo'q → avval `git add .` va `git commit` |
| `Please tell me who you are` | Ism/email sozlanmagan → 1-bo'limni bajaring |
| `rejected ... fetch first` | GitHub'da yangi o'zgarish bor → `git pull`, keyin `git push` |
| `not a git repository` | Papka git loyiha emas → `git init` yoki to'g'ri papkaga o'ting |
| `CONFLICT (content)` | Bitta faylni ikki joyda o'zgartirgansiz → faylni ochib, `<<<<<<<` belgilari orasidagini tuzating, keyin `add` + `commit` |
| `Your branch is behind` | GitHub'da yangilik bor → `git pull` |
| `Your branch is ahead` | Push qilinmagan commit bor → `git push` |
