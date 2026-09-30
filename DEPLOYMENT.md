# 🚀 دليل النشر - منصة فلاحين

## النشر على Vercel

### الطريقة 1: عبر واجهة Vercel (الأسهل)

1. **انتقل إلى** [vercel.com](https://vercel.com) وسجّل دخولك
2. اضغط على **"Add New Project"**
3. ارفع مجلد المشروع `fla7in/`
4. اضغط **"Deploy"**
5. انتظر دقيقة واحدة - المشروع سينشر تلقائياً ✅

### الطريقة 2: عبر GitHub + Vercel

```bash
# 1. أنشئ مستودع GitHub جديد
git init
git add .
git commit -m "Initial commit - فلاحين platform"
git remote add origin https://github.com/username/fla7in.git
git push -u origin main

# 2. اربط المستودع بـ Vercel من Dashboard
```

---

## إعداد Firebase

### 1. قواعد Firestore

انتقل إلى Firebase Console > Firestore > Rules واستبدل بـ:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // الاستشارات - قراءة وكتابة عامة
    match /consultations/{docId} {
      allow read, write: if true;
    }
    // الحلول - قراءة عامة فقط
    match /solutions/{docId} {
      allow read: if true;
      allow write: if false; // فقط Admin
    }
    // اختبار
    match /test_consultations/{docId} {
      allow read, write: if true;
    }
  }
}
```

### 2. إضافة بيانات الحلول

**استخدم Firebase Console > Firestore > Add Document في `solutions`:**

**مثال - زيتون فترة التزهير:**
```json
{
  "crop": "olive",
  "cropArabic": "زيتون",
  "treeStage": "flowering",
  "periodName": "فترة التزهير",
  "problem": "دعم التزهير وتحسين عقد الثمار",
  "products": [
    {
      "name": "بوران 11",
      "dosage": "2 كغ / هكتار",
      "purpose": "تحفيز التزهير وتحسين جودة حبوب اللقاح",
      "icon": "🌸"
    },
    {
      "name": "NPK 10-52-10",
      "dosage": "3 كغ / هكتار",
      "purpose": "توفير الفوسفور للجذور ودعم النمو",
      "icon": "🌿"
    },
    {
      "name": "كالسيوم + بور",
      "dosage": "1.5 كغ / هكتار",
      "purpose": "منع تساقط الأزهار وتحسين العقد",
      "icon": "💊"
    }
  ],
  "active": true,
  "addedBy": "admin",
  "createdAt": "(serverTimestamp)"
}
```

**مثال - طماطم مرحلة 15-45 يوم:**
```json
{
  "crop": "tomato",
  "cropArabic": "طماطم",
  "period": "short",
  "periodName": "من 15 إلى 45 يوم",
  "problem": "دفعة قوية للنمو الخضري",
  "products": [
    {
      "name": "سماد NPK متوازن (20-20-20)",
      "dosage": "2 كغ / هكتار",
      "purpose": "دعم النمو الخضري المتوازن وتكوين الجذور",
      "icon": "🌿"
    },
    {
      "name": "هيومات البوتاسيوم",
      "dosage": "1 كغ / هكتار",
      "purpose": "تحسين امتصاص العناصر وتطوير المجموع الجذري",
      "icon": "🌱"
    }
  ],
  "active": true,
  "addedBy": "admin"
}
```

---

## التحقق من النشر

بعد النشر، تحقق من:

1. **الصفحة الرئيسية:** `https://your-domain.vercel.app/`
2. **الاستشارة:** `https://your-domain.vercel.app/consultation.html`
3. **لوحة التحكم:** `https://your-domain.vercel.app/admin/consultations.html`
4. **اختبار Firebase:** `https://your-domain.vercel.app/test-firebase.html`

---

## استكشاف الأخطاء

| المشكلة | الحل |
|---------|------|
| Firebase لا يتصل | تحقق من قواعد Firestore |
| لا تظهر الحلول | تأكد من وجود documents في `solutions` collection |
| خطأ في الكتابة | تأكد من قواعد الـ write في Firestore |
| الصفحة لا تفتح | تأكد من رفع جميع الملفات بشكل صحيح |

---

## ملاحظات مهمة

- ملفات `test-firebase.html` و`check-firebase.html` **للاختبار المحلي فقط**
- يمكنك حذفها قبل النشر النهائي أو إبقاؤها (لا تؤثر)
- admin panel لا يحتاج authentication حالياً - يمكنك إضافته لاحقاً
