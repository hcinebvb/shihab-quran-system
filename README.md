# نظام إدارة مدرسة شهاب للقرآن الكريم

نظام ويب متكامل لإدارة مدرسة قرآنية — واجهة عربية RTL، تخزين محلي، وجاهز للربط بـ Backend.

## المتطلبات

- متصفح حديث (Chrome, Firefox, Edge)
- لا حاجة لخادم — يعمل مباشرة من الملفات
- (اختياري) Live Server أو أي خادم محلي للتطوير

## طريقة التشغيل

### 1. فتح مباشر
افتح الملف `login.html` في المتصفح.

### 2. عبر خادم محلي (موصى به)
```bash
cd shihab-quran-system
npx serve .
# أو
python -m http.server 8080
```
ثم افتح: `http://localhost:8080/login.html`

## حسابات تجريبية

| الدور | المستخدم | كلمة المرور |
|-------|----------|-------------|
| مدير النظام | admin | admin123 |
| مشرف | supervisor | sup123 |
| أستاذ | aziz | teacher123 |

## الصلاحيات

- **مدير النظام**: جميع الصلاحيات + الإعدادات
- **مشرف**: التلاميذ، الحضور، الأفواج، المالية، التقارير، الاستيراد
- **أستاذ**: تلاميذه، الحفظ، الحضور

## هيكلة المشروع

```
shihab-quran-system/
├── index.html              → تحويل تلقائي لصفحة الدخول
├── login.html              → تسجيل الدخول
├── dashboard.html          → لوحة التحكم
├── students.html           → إدارة التلاميذ
├── teachers.html           → إدارة الأساتذة
├── groups.html             → إدارة الأفواج
├── attendance.html         → الحضور والغياب
├── memorization.html       → إدارة الحفظ
├── finance.html            → الإدارة المالية
├── reports.html            → التقارير والتصدير
├── import.html             → الاستيراد الذكي
├── settings.html           → الإعدادات
├── assets/
│   ├── css/                → variables.css, main.css
│   └── js/
│       ├── db.js           → طبقة البيانات (LocalStorage)
│       ├── ui.js           → أدوات الواجهة
│       ├── app.js          → Sidebar, Navbar, Auth
│       ├── icons.js        → أيقونات SVG
│       ├── surahs.js       → قائمة السور
│       └── pages/          → منطق كل صفحة
├── components/             → قوالب HTML مرجعية
└── database/
    └── schema.sql          → هيكل SQLite جاهز للربط
```

## الميزات

- واجهة عربية RTL احترافية
- الوضع الليلي / النهاري
- Responsive — يعمل على الجوال
- LocalStorage للتخزين الفوري
- تصدير CSV / JSON
- طباعة التقارير ووصول الدفع
- استيراد CSV للتلاميذ، وJSON/CSV للحضور والغياب
- بحث متقدم عن التلاميذ بالاسم، الهاتف، الفوج، الأستاذ أو الحالة
- بيانات تجريبية جاهزة (10 تلاميذ، 5 أساتذة، 4 أفواج)

## الربط بـ Backend مستقبلاً

1. استخدم `database/schema.sql` لإنشاء قاعدة SQLite/MySQL
2. استبدل دوال `store.get/set` في `db.js` بـ `fetch()` إلى API
3. دوال `exportAll()` و `importAll()` جاهزة للمزامنة

### مثال API (Node.js / PHP / Django)
```
GET  /api/students
POST /api/students
PUT  /api/students/:id
DELETE /api/students/:id
```

## استيراد CSV

استخدم ملف `database/sample_students.csv` كنموذج:

```csv
الاسم,اللقب,الجنس,هاتف الولي
أحمد,بن محمد,ذكر,0550123456
```

لاستيراد الغيابات استخدم ملف `database/sample_attendance.html` كنسخة HTML، أو `database/sample_attendance.csv` كنسخة CSV:

```csv
اسم التلميذ,التاريخ,الحالة,ملاحظات
محمد بن علي,2026-06-02,غائب,
```

## النسخ الاحتياطي

من صفحة **الإعدادات** → تصدير نسخة احتياطية (JSON)

## الترخيص

مشروع مفتوح للاستخدام والتطوير — مدرسة شهاب للقرآن الكريم

---

## Backend جاهز

تمت إضافة مشروع Backend كامل داخل:

`backend/`

وللنشر العام على الإنترنت (Render) يوجد ملف:

`render.yaml`

لتشغيله:

```bash
cd backend
npm install
copy .env.example .env
npm run db:init
npm run db:seed
npm run dev
```
