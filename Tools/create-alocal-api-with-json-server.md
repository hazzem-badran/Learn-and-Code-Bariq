
لتشغيل **JSON Server** على جهازك، ستحتاج أولاً إلى تثبيته ومن ثم إعداد API وهمي باستخدام ملف JSON. إليك خطوات إعداد واستخدام **JSON Server**:

### 1. **تثبيت JSON Server**:



```
npm install -g json-server
```


هذا الأمر سيقوم بتثبيت JSON Server بشكل عالمي (يمكنك استخدامه في أي مكان على جهازك).

### 2. **إنشاء ملف JSON للبيانات**:

أنشئ ملف JSON يحتوي على البيانات التي تريد محاكاتها باستخدام JSON Server. على سبيل المثال، أنشئ ملف باسم `db.json` داخل مجلد جديد.

مثال لملف `db.json`:



```
{
  "todos": [
    {
      "userId": 1,
      "id": 1,
      "title": "delectus aut autem",
      "completed": false
    },
    {
      "userId": 1,
      "id": 2,
      "title": "quis ut nam facilis et officia qui",
      "completed": false
    },
    {
      "userId": 1,
      "id": 3,
      "title": "fugiat veniam minus",
      "completed": false
    },
    {
      "userId": 1,
      "id": 4,
      "title": "et porro tempora",
      "completed": true
    },
    {
      "userId": 1,
      "id": 5,
      "title": "laboriosam mollitia et enim quasi adipisci quia provident illum",
      "completed": false
    }
  ]
}

```



هذا المثال يحتوي على بيانات افتراضية لِـ **todos**. يمكنك إضافة المزيد من الكائنات حسب الحاجة.

### 3. **تشغيل JSON Server**:

بعد إنشاء ملف `db.json`، يمكنك تشغيل JSON Server باستخدام الأمر التالي في **Terminal** أو **Command Prompt**:


```
json-server --watch db.json
```


هذا سيبدأ **JSON Server** ويقوم بمراقبة الملف `db.json` لأي تغييرات. 

ستلاحظ أنه سيبدأ تشغيل API محلي على الرابط التالي:



```
http://localhost:3000
```


يمكنك الآن الوصول إلى الـ API الخاص بك عبر هذا الرابط.


### المزايا:

- **سهل الاستخدام**: لا تحتاج لكتابة أكواد معقدة لإنشاء API وهمي.
    
- **إمكانية التخصيص**: يمكنك تعديل بيانات JSON حسب حاجتك.
    
- **بدون اتصال بالإنترنت**: يعمل بشكل محلي على جهازك.