
لجلب  آخر تعليق (commit) قمت به في مستودع Git، يمكنك استخدام أحد الأوامر التالية:


### **1. عرض آخر تعليق فقط:**

```
git log -1
```

النتيجة:


commit 6df8de41c4861d51ae122749026858ca08ad44fd (HEAD -> feature/send-message-to-support-use-case-nestjs, origin/feature/send-message-to-support-use-case-nestjs)
Author: Hazzembadran <youremail@example.com>
Date:   Fri Jan 17 10:16:06 2025 +0200

    Optimize the code based on the guidelines of Eng. Abdul Latif.

### **2.عرض رسالة آخر تعليق فقط:**


```
git log -1 --pretty=%B
```

النتيجة:

Optimize the code based on the guidelines of Eng. Abdul Latif.



### **3. عرض التعليقات بتنسيق مختصر:**

إذا كنت تريد عرض تعليقات مختصرة وبشكل مدمج، يمكن استخدام:

```
git log -1 --oneline
```

النتيجة:

6df8de4 (HEAD -> feature/send-message-to-support-use-case-nestjs, origin/feature/send-message-to-support-use-case-nestjs) Optimize the code based on the guidelines of Eng. Abdul Latif.


> هناك أوامر أخرى يمكنك البحث عنها.
