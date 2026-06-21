# Backend — مدرسة الشهاب

Backend جاهز للإنتاج المبدئي باستخدام:

- Node.js + Express
- SQLite
- JWT Authentication
- RBAC (admin/supervisor/teacher)
- نظام دفعات ثلاثي: `t1`, `t2`, `t3`, `summer`
- يخدم الواجهة الأمامية من نفس الرابط (Single Service)

## 1) التثبيت

```bash
cd backend
npm install
copy .env.example .env
```

## 2) تهيئة قاعدة البيانات

```bash
npm run db:init
npm run db:seed
```

## 3) التشغيل

```bash
npm run dev
```

السيرفر:

`http://localhost:4000`

فحص الصحة:

`GET /api/health`

## حسابات افتراضية

- `admin` / `admin123`
- `supervisor` / `sup123`

## أهم الـ Endpoints

- `POST /api/auth/login`
- `GET /api/auth/me`
- `GET/POST/PUT/DELETE /api/students`
- `GET/POST/PUT/DELETE /api/teachers`
- `GET/POST/PUT/DELETE /api/groups`
- `GET /api/attendance?date=YYYY-MM-DD&groupId=...`
- `POST /api/attendance/bulk`
- `GET /api/payments/matrix/:groupId?academicYear=2025-2026`
- `POST /api/payments/matrix/:groupId`
- `GET /api/dashboard/kpis`

## ملاحظة الترحيل

`npm run db:seed` يستورد تلقائيًا البيانات من:

`../database/school_data.json`

ويحوّل الدفعات الشهرية القديمة إلى نظام الثلاثيات + الصيفية.

> ملاحظة: السكربت لن يعيد التهيئة إذا كانت القاعدة تحتوي مستخدمين. لإعادة التهيئة القسرية:
>
> `FORCE_SEED=true npm run db:seed`

## نشر مباشر على Render

- ملف النشر موجود في جذر المشروع: `render.yaml`
- عند أول Deploy سيتم:
  - مزامنة الواجهة تلقائيًا إلى `backend/public`
  - إنشاء القاعدة
  - استيراد البيانات الأولية
  - تشغيل API والواجهة معًا على نفس الرابط
- بعد النشر استخدم:
  - `https://YOUR-APP.onrender.com/login.html`
  - الحساب: `admin` / `admin123`
