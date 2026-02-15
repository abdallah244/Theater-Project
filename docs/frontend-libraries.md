<!--
Audience: Frontend Engineer
Framework: Next.js
Purpose: Define the libraries/packages to use (minimal + optional) for MVP.
-->

# Frontend Libraries (Next.js) — قائمة المكتبات

**هدف الوثيقة:** توحيد المكتبات المستخدمة في الـ Frontend (Next.js) لتقليل إعادة الشغل وتسهيل الصيانة.

**مبدأ مهم:** نختار أقل عدد مكتبات يحقق الـ MVP. أي مكتبة "تحسين" تعتبر اختيارية ولا تدخل التنفيذ إلا إذا احتجناها فعليًا.

---

## 1) الأساسيات (Required)

> هذه مكتبات/حزم متوقعة في أي مشروع Next.js، أو لازمة لتنفيذ الـ MVP بكفاءة.

### 1.1 Framework + Core

- `next`, `react`, `react-dom`
  - تشغيل Next.js (App Router أو Pages Router حسب قرار المشروع).

### 1.2 TypeScript (مستحسن جدًا)

- `typescript`, `@types/node`, `@types/react`
  - يقلل أخطاء الـ API contracts وبيسهّل تطوير الـ Seat Map و الـ DTOs.

> لو الفريق قرر JavaScript فقط: يتم حذف TypeScript، لكن هذا يزيد احتمالية أخطاء تكامل.

### 1.3 Fetching / API Client

**الخيار الافتراضي (مُفضّل للمينيمال):**

- الاعتماد على `fetch` المدمج (سواء Server Components أو Client Components).

**بديل عند الحاجة:**

- `axios`
  - مفيد لو محتاجين interceptors / baseURL / timeouts بشكل موحّد.

> القرار: إن لم توجد حاجة واضحة، نلتزم بـ `fetch`.

### 1.4 Validation (Client-Side)

- `zod`
  - لتوحيد validation لنماذج الإدخال (وليّ الأمر) ولتعريف schema للـ responses لو حابين.

### 1.5 Forms

- `react-hook-form`
  - خفيف وسريع لتطبيق forms + error messages.
- `@hookform/resolvers`
  - لربط `zod` بسهولة.

### 1.6 Formatting / Linting

- `eslint` + إعداد Next.js الافتراضي
- `prettier`
  - لتوحيد شكل الكود.

---

## 2) تصميم/ستايل (Styling)

> لأن الديزاين النهائي لسه مش جاهز، الأفضل نستخدم طريقة ستايل بسيطة وما تقيّدناش.

**الخيار الافتراضي (Minimal):**

- CSS Modules (المدمج في Next.js)

**اختياري (لو الفريق شغال Tailwind):**

- `tailwindcss`, `postcss`, `autoprefixer`

> ملاحظة: لا نضيف UI Component Library (مثل Material/Chakra/…)، إلا إذا تم الاتفاق عليها صراحة، لأن ده بيغيّر شكل المنتج ويوسّع النطاق.

---

## 3) أدوات اختيارية (Optional Enhancements)

> لا تُستخدم إلا عند وجود سبب واضح.

### 3.1 Seat Map: Zoom/Pan

- `react-zoom-pan-pinch`
  - فقط لو الخريطة كبيرة جدًا ومحتاجين تجربة Zoom/Pan قوية.

### 3.2 Tables (Admin)

- `@tanstack/react-table`
  - لو جدول الحجوزات محتاج sorting/pagination بشكل نظيف.

### 3.3 State Management (إن احتجنا)

**الافتراضي:** State محلي + React context خفيف.

**اختياري:**

- `zustand`
  - لو بدأت الحالة تتعقّد (حجز + مقاعد + Admin) وعايزين store بسيط.

### 3.4 Dates

- `date-fns`
  - لتنسيق التاريخ/الوقت في واجهة العروض.

### 3.5 Notifications

- `react-hot-toast`
  - رسائل نجاح/خطأ بشكل واضح (اختياري).

---

## 4) أمن وAuth (Frontend)

> تفضيلًا: الـ Auth يعتمد على Cookie HttpOnly من الـ Backend.

- لا نحتاج مكتبة Auth جاهزة لو الـ Backend بيصدر JWT/Session.
- لو اضطرينا للتعامل مع توكن على الواجهة:
  - `js-cookie` (اختياري)

**تحذير:** تخزين JWT في `localStorage` يزيد المخاطر (XSS). يُستخدم فقط كحل مؤقت وبموافقة.

---

## 5) أوامر تثبيت مقترحة

> يتم تنفيذها داخل مشروع Next.js بعد إنشائه.

### Minimal MVP (مُقترح)

- `npm i zod react-hook-form @hookform/resolvers`

### Optional

- `npm i axios`
- `npm i react-zoom-pan-pinch`
- `npm i @tanstack/react-table`
- `npm i zustand`
- `npm i date-fns`
- `npm i react-hot-toast`

---

## 6) قواعد اختيار المكتبات (Governance)

- لا نضيف مكتبة جديدة إلا بسبب واضح مرتبط بميزة داخل الـ MVP.
- أي مكتبة جديدة لازم يكون لها:
  - سبب استخدام
  - بديل (إن وجد)
  - تأثيرها على الوقت/النطاق

---

## 7) توافق مع وثائق المشروع

- متطلبات التنفيذ قبل الديزاين موجودة في [frontend-nextjs.md](frontend-nextjs.md).
- الشاشات والتفاعل المطلوبين موجودين في [ui-ux-spec.md](ui-ux-spec.md).
- نطاق المشروع وخطة 14 يوم موجودة في [../report.md](../report.md).
