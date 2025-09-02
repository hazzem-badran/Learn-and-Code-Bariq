# 🚀 استخدام Husky للتحكم في أسماء الفروع

## ما هو Husky؟
[Husky](https://typicode.github.io/husky) هي مكتبة JavaScript تساعدك في إدارة [Git Hooks](https://git-scm.com/docs/githooks).  
بواسطتها يمكنك تنفيذ أوامر أو سكربتات **قبل تنفيذ عمليات Git** مثل:  
- `commit`  
- `push`  
- `merge`  
- وغيرها...  

> الهدف: فرض قواعد معينة على التيم بشكل أوتوماتيكي بدل الاعتماد على التذكير اليدوي.

---

## الهدف من الإعداد
نريد أن نسمح فقط بالعمل على الفروع التي تبدأ بالأسماء التالية:  
- `feature/`  
- `bugfix/`  
- `hotfix/`  

بمعنى: أي محاولة **commit** أو **push** على فرع باسم مختلف → يتم رفضها.

---

## خطوات الإعداد

### 1. تثبيت Husky
```bash
npm install husky --save-dev

```

### 2. تهيئة Husky
```
npx husky install

```

ثم نضيف في ملف `package.json`:

```
{
  "scripts": {
    "prepare": "husky install"
  }
}

```

## إعداد Git Hooks

### 📌 ملف `.husky/pre-commit`

هذا الملف يتم تشغيله **قبل كل commit**.  
نقوم فيه بالتحقق من اسم الفرع، وإذا كان صحيحًا، نشغل `npm run lint`.

```
#!/bin/sh
branch=$(git symbolic-ref --short HEAD)

# السماح فقط بالعمل على feature/, bugfix/, أو hotfix/
if ! echo "$branch" | grep -qE "^(feature/|bugfix/|hotfix/)"; then
  echo "❌ Commits are only allowed on feature/, bugfix/, or hotfix/ branches."
  echo "Your current branch is '$branch'."
  echo "Please create a branch with a valid name before committing."
  exit 1
fi

# إذا كان اسم الفرع صحيح → شغّل lint
npm run lint

```

### 📌 ملف `.husky/pre-push`

هذا الملف يتم تشغيله **قبل كل push**.  
نقوم فيه بالتحقق من اسم الفرع قبل إرسال الكود إلى الـ remote.

```

#!/bin/sh
branch=$(git symbolic-ref --short HEAD)

# السماح فقط بالعمل على feature/, bugfix/, أو hotfix/
if ! echo "$branch" | grep -qE "^(feature/|bugfix/|hotfix/)"; then
  echo "❌ Pushes are only allowed on feature/, bugfix/, or hotfix/ branches."
  echo "Your current branch is '$branch'."
  echo "Please push from a valid branch."
  exit 1
fi

echo "✅ Branch '$branch' is valid. Proceeding with push..."


```
## النتيجة 🎉

- أي **commit** أو **push** على فرع باسم غير مسموح → يتم منعه.
    
- هيك بنضمن Naming Convention موحد داخل التيم.
    
- يمكن التوسع وإضافة استثناءات (مثل `main` أو `develop`) بسهولة عبر تعديل الـ `regex`.