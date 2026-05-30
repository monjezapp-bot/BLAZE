<div align="center">

# 🔥 BLAZE

### تطبيق إدارة المهام بمصفوفة أيزنهاور

[![Firebase](https://img.shields.io/badge/Firebase-Firestore%20%2B%20Auth-orange?logo=firebase)](https://firebase.google.com)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0.0-green.svg)]()
[![Arabic](https://img.shields.io/badge/Language-Arabic%20RTL-red.svg)]()

> **ركز على ما يهم. أنجز بذكاء. ابدأ يومك بقوة.**

</div>

---

## 📱 نظرة عامة

**BLAZE** هو تطبيق ويب متكامل لإدارة المهام مبني على مبدأ **مصفوفة أيزنهاور**، يساعدك على تصنيف مهامك حسب الأهمية والاستعجال، مما يمكّنك من التركيز على ما يحقق أهدافك الحقيقية.

التطبيق مبني كـ **Single HTML File** — لا حاجة لسيرفر، لا حاجة لبناء — افتح الملف وابدأ!

---

## ✨ المميزات

| الميزة | التفاصيل |
|--------|----------|
| 🔐 **تسجيل دخول** | Firebase Authentication (إيميل + كلمة مرور) |
| ☁️ **مزامنة سحابية** | Firestore — بيانات منفصلة لكل مستخدم |
| 📊 **مصفوفة أيزنهاور** | 4 مربعات: مهم/عاجل، مهم/غير عاجل، عاجل/غير مهم، غير مهم/غير عاجل |
| 🎙️ **إدخال صوتي** | التعرف على الصوت بالعربية وتصنيف المهمة تلقائياً |
| ⏱️ **مؤقت المهام** | تتبع الوقت الفعلي المستغرق في كل مهمة |
| 📍 **Geofencing** | تنبيه ذكي عند الابتعاد عن موقع المهمة |
| 🔔 **إشعارات** | تذكير قبل 15 دقيقة وعند موعد المهمة |
| 📤 **تصدير البيانات** | تصدير كل مهامك بصيغة JSON |
| 📱 **تصميم موبايل** | PWA-ready، يعمل على جميع الأجهزة |
| 🌙 **وضع RTL** | دعم كامل للغة العربية من اليمين إلى اليسار |

---

## 🗂️ مصفوفة أيزنهاور

```
                 عاجل              غير عاجل
           ┌──────────────┬──────────────┐
  مهم      │  🔥 افعلها  │  🎯 خطط لها │
           │    الآن!     │   بعناية    │
           ├──────────────┼──────────────┤
  غير مهم  │ ⚡ فوّضها   │ 🗑️ تخلّص   │
           │  لغيرك      │    منها     │
           └──────────────┴──────────────┘
```

---

## 🚀 التشغيل

### الطريقة الأسرع

```bash
# 1. حمّل الملف
git clone https://github.com/YOUR_USERNAME/blaze.git

# 2. افتح الملف في المتصفح
open blaze.html
# أو على Windows:
start blaze.html
```

> **ملاحظة:** التطبيق يحتاج اتصال إنترنت لتحميل Firebase و Tailwind CDN.

### التشغيل على سيرفر محلي (مُوصى به)

```bash
# باستخدام Python
python -m http.server 8080

# باستخدام Node.js
npx serve .

# ثم افتح في المتصفح:
# http://localhost:8080/blaze.html
```

---

## 🔧 الإعداد

### 1. إعداد Firebase

1. اذهب إلى [Firebase Console](https://console.firebase.google.com)
2. أنشئ مشروعاً جديداً
3. فعّل **Authentication** → Email/Password
4. فعّل **Firestore Database**
5. انسخ إعدادات المشروع وضعها في الملف

### 2. Firestore Security Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // كل مستخدم يقرأ ويكتب بياناته فقط
    match /users/{userId}/tasks/{taskId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### 3. هيكل البيانات في Firestore

```
users/
  └── {userId}/
        └── tasks/
              └── {taskId}/
                    ├── id: string
                    ├── name: string
                    ├── quad: "q1" | "q2" | "q3" | "q4"
                    ├── date: string (YYYY-MM-DD)
                    ├── timeFrom: string (HH:MM)
                    ├── timeTo: string (HH:MM)
                    ├── locationName: string
                    ├── locationCoords: { lat, lng, accuracy }
                    ├── geoRadius: number (meters)
                    ├── note: string
                    ├── done: boolean
                    ├── runSeconds: number
                    └── createdAt: ISO string
```

---

## 🏗️ هيكل المشروع

```
blaze/
├── blaze.html          # التطبيق كاملاً (HTML + CSS + JS)
├── blaze-logo.svg      # شعار التطبيق الأفقي
├── blaze-icon.svg      # أيقونة التطبيق (512×512)
└── README.md           # هذا الملف
```

---

## 🛠️ التقنيات المستخدمة

| التقنية | الغرض |
|---------|--------|
| **HTML5 / CSS3 / JavaScript** | البنية الأساسية |
| **Tailwind CSS** (CDN) | التنسيق والتصميم |
| **Cairo Font** (Google Fonts) | الخط العربي |
| **Firebase Auth** v12 | تسجيل الدخول |
| **Firebase Firestore** v12 | قاعدة البيانات السحابية |
| **Web Speech API** | الإدخال الصوتي بالعربية |
| **Geolocation API** | تحديد الموقع و Geofencing |
| **Notification API** | الإشعارات |

---

## 📸 لقطات الشاشة

> قريباً — أضف صور التطبيق هنا

---

## 🤝 المساهمة

المساهمات مرحب بها! للمساهمة:

1. Fork المشروع
2. أنشئ branch جديد: `git checkout -b feature/اسم-الميزة`
3. Commit التغييرات: `git commit -m 'إضافة ميزة جديدة'`
4. Push: `git push origin feature/اسم-الميزة`
5. افتح Pull Request

---

## 🐛 الإبلاغ عن مشكلة

إذا واجهت أي مشكلة، افتح [Issue جديد](https://github.com/YOUR_USERNAME/blaze/issues) مع:
- وصف المشكلة
- خطوات إعادة إنتاجها
- المتصفح ونظام التشغيل

---

## 📄 الرخصة

هذا المشروع مرخص بـ [MIT License](LICENSE).

---

#طارق عبد الجليلي 👨‍💻 المطور

صُنع بـ 🔥 و ☕

---

<div align="center">

**BLAZE v1.0** — ابدأ يومك بقوة 🔥

</div>
