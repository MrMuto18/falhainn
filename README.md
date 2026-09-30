# 🌿 فلاحين - منصة استشارات زراعية ذكية

منصة ويب كاملة تقدم استشارات زراعية مجانية ومخصصة للفلاحين التونسيين.

---

## 📂 هيكل الملفات

```
fla7in/
├── index.html                  # الصفحة الرئيسية
├── consultation.html           # صفحة الاستشارة (7 أسئلة)
├── test-firebase.html          # اختبار الاتصال بـ Firebase (محلي)
├── check-firebase.html         # فحص بيانات المحاصيل (محلي)
├── README.md                   # هذا الملف
├── DEPLOYMENT.md               # خطوات النشر
└── admin/
    └── consultations.html      # لوحة تحكم الاستشارات
```

---

## 🚀 الصفحات

### 1. `index.html` - الصفحة الرئيسية
- Hero section مع شعار وزر استشارة مجانية
- عرض 12 محصول مدعوم مع أيقونات
- إحصائيات المنصة
- ميزات وطريقة العمل

### 2. `consultation.html` - صفحة الاستشارة
**7 أسئلة متتالية:**
1. المحصول (12 خيار)
2. المساحة (3 خيارات)
3. نظام الري (4 خيارات)
4. نوع التربة (3 خيارات)
5. ملوحة الماء (3 خيارات)
6. الفترة/المرحلة (يتغير حسب المحصول)
7. البيانات الشخصية (الاسم، الهاتف، المنطقة)

**المميزات:**
- Auto-advance بعد كل اختيار (500ms)
- Progress bar تفاعلي
- Validation للحقول الإجبارية
- حفظ تلقائي في Firebase
- Modal لعرض الحلول الزراعية

### 3. `admin/consultations.html` - لوحة التحكم
- إحصائيات (إجمالي، اليوم، جديدة)
- فلاتر (بحث، محصول، منطقة)
- جدول الاستشارات مع حالات ملونة
- Modal لعرض التفاصيل
- تغيير حالة الاستشارة (جديد / تم الاتصال / مكتمل)

---

## 🔥 Firebase Collections

### `consultations` (للكتابة من consultation.html والقراءة من admin)
```json
{
  "name": "محمد بن علي",
  "phone": "55123456",
  "region": "تونس",
  "crop": "olive",
  "cropName": "زيتون",
  "cropType": "tree",
  "area": "small",
  "water": "drip",
  "soil": "mixed",
  "salinity": "low",
  "period": "flowering",
  "periodName": "فترة التزهير",
  "createdAt": "Timestamp",
  "status": "new"
}
```

### `solutions` (للقراءة من consultation.html)
```json
{
  "crop": "olive",
  "cropArabic": "زيتون",
  "treeStage": "flowering",
  "period": null,
  "periodName": "فترة التزهير",
  "problem": "دعم التزهير وتحسين العقد",
  "products": [
    {
      "name": "بوران 11",
      "dosage": "2 كغ / هكتار",
      "purpose": "تحفيز التزهير وتحسين جودة حبوب اللقاح",
      "icon": "🌸"
    }
  ],
  "active": true,
  "createdAt": "Timestamp"
}
```

**ملاحظة للحقل `period`:**
- للأشجار: استخدم `treeStage` = `dormancy` / `flowering` / `fruit-set` / `ripening`
- للخضروات والحبوب: استخدم `period` = `short` / `medium` / `long` / `harvest`

---

## 🌾 المحاصيل والفترات

| المحصول | النوع | الفترات |
|---------|-------|---------|
| زيتون | tree | dormancy, flowering, fruit-set, ripening |
| لوز | tree | dormancy, flowering, fruit-set, ripening |
| عنب | tree | dormancy, flowering, fruit-set, ripening |
| قوارص | tree | dormancy, flowering, fruit-set, ripening |
| طماطم | vegetable | short, medium, long, harvest |
| فلفل | vegetable | short, medium, long, harvest |
| بطاطا | vegetable | short, medium, long, harvest |
| بطيخ | vegetable | short, medium, long, harvest |
| دلاع | vegetable | short, medium, long, harvest |
| فراولة | vegetable | short, medium, long, harvest |
| حبوب | grains | short, medium, long |
| بسباس | fennel | short, medium, long |

---

## ⚙️ إضافة حلول جديدة في Firebase

لإضافة حلول لمحصول جديد، أضف وثيقة في `solutions` collection:

**للأشجار:**
```javascript
{
  crop: "olive",           // معرف المحصول
  cropArabic: "زيتون",
  treeStage: "flowering",  // الفترة
  periodName: "فترة التزهير",
  problem: "دعم التزهير وتحسين العقد",
  products: [
    { name: "بوران 11", dosage: "2 كغ/هكتار", purpose: "...", icon: "🌸" },
    { name: "NPK 10-52-10", dosage: "3 كغ/هكتار", purpose: "...", icon: "🌿" }
  ],
  active: true,
  createdAt: new Date()
}
```

**للخضروات:**
```javascript
{
  crop: "tomato",
  cropArabic: "طماطم",
  period: "short",         // استخدم period بدل treeStage
  periodName: "من 15 إلى 45 يوم",
  problem: "دفعة قوية للنمو الخضري",
  products: [...],
  active: true
}
```

---

## 🎨 الألوان

```css
--primary: #2d8659
--primary-light: #4caf50
--primary-dark: #1e6b45
--beige: #f5f1e8
--text: #2c3e50
--text-light: #6c757d
```

---

## 📱 Responsive Breakpoints

- Desktop: 1200px+
- Tablet: 768px - 1199px
- Mobile: < 768px

---

## 🔧 أدوات الاختبار

- **test-firebase.html**: اختبار الاتصال، الكتابة، والقراءة
- **check-firebase.html**: فحص وجود حلول لكل محصول وكل فترة

---

## ✅ Checklist قبل النشر

- [ ] تأكد من قواعد Firestore تسمح بالقراءة/الكتابة
- [ ] أضف حلولاً لكل المحاصيل في `solutions` collection
- [ ] اختبر الاستشارة كاملاً من البداية للنهاية
- [ ] تحقق من admin panel وفلاتر البحث
- [ ] اختبر على موبايل وديسكتوب
