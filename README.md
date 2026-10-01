# Parham 01 — Cloudflare Worker VPN

این پروژه برای اجرای سرویس روی **Cloudflare Workers** طراحی شده است.  
در نسخه جدید، بخش پنل مدیریت و مسیر `adminme` از راهنما حذف شده و تمرکز README فقط روی بخش کاربری، کانفیگ‌ها، ساب‌لینک‌ها و استفاده از بنر است.

---

## 📁 ساختار فایل‌ها

```text
parham01/
├── worker.js
├── README.md
└── banner.jpg
```

> فایل تصویر باید دقیقاً با نام `banner.jpg` کنار `worker.js` قرار بگیرد.

### 🖼️ بنر از کجا خوانده می‌شود؟

```text
Worker
  │
  ├── worker.js
  │
  └── banner.jpg
        │
        └── بنر سایت / صفحه کاربری
```

یعنی هر زمان کد برای نمایش بنر به فایل تصویر نیاز داشته باشد، فایل زیر را استفاده می‌کند:

```text
/banner.jpg
```

اگر بنر را عوض کردی، فقط تصویر جدید را با همین نام جایگزین کن:

```text
banner.jpg
```

---

# 🇮🇷 راهنمای فارسی

## 1) این پروژه چیست؟

یک پروژه مدیریت و ارائه کانفیگ روی Cloudflare Workers است که بدون VPS اجرا می‌شود.

قابلیت‌های اصلی:

- VLESS
- Trojan
- VLESS + Trojan
- ساخت لینک‌های vmess، shadowsocks، hysteria2 و tuic
- ساخت لینک WireGuard/WARP
- محدودیت حجم
- محدودیت زمانی
- محدودیت IP همزمان
- ساب‌لینک
- QR Code
- صفحه کاربر
- تشخیص دستگاه
- Clean IP
- Proxy IP
- ساخت گروهی کانفیگ
- Clone
- جستجو و فیلتر
- Kill Switch
- بکاپ و بازگردانی
- ربات تلگرام

> توجه: طبق ساختار فعلی پروژه، VLESS و Trojan روی Worker اجرا می‌شوند؛ پروتکل‌های vmess، shadowsocks، hysteria2، tuic و wireguard در حالت لینک/کانفیگ خارجی استفاده می‌شوند.

---

## 2) پیش‌نیازها

- اکانت Cloudflare
- یک Worker
- در صورت نیاز دامنه متصل به Cloudflare
- D1 برای اطلاعات پروژه
- در صورت استفاده از قابلیت‌های مربوط، KV
- در صورت استفاده از ربات، توکن Telegram Bot

---

## 3) نصب روی Cloudflare

### مرحله ۱ — ساخت D1

```text
Cloudflare Dashboard
      │
      ▼
Storage & databases
      │
      ▼
D1 SQL database
      │
      ▼
Create database
```

یک دیتابیس بساز.

---

### مرحله ۲ — ساخت KV

```text
Cloudflare Dashboard
      │
      ▼
Storage & databases
      │
      ▼
KV
      │
      ▼
Create a namespace
```

---

### مرحله ۳ — ساخت Worker

```text
Workers & Pages
      │
      ▼
Create application
      │
      ▼
Create Worker
      │
      ▼
Edit code
      │
      ▼
worker.js
      │
      ▼
Deploy
```

کد پروژه را داخل `worker.js` قرار بده و Deploy کن.

---

## 4) اتصال D1 و KV

در تنظیمات Worker، Bindingهای پروژه را وصل کن.

```text
Worker
  │
  ├── DB  ───────► D1
  │
  └── KV  ───────► KV Namespace
```

نام Binding دیتابیس باید مطابق کدی باشد که در Worker استفاده شده است.

---

# 🖼️ بخش بنر

بنر در کنار فایل Worker قرار می‌گیرد:

```text
parham01/
│
├── worker.js
│
├── README.md
│
└── banner.jpg
```

### تعویض بنر

1. تصویر جدید را آماده کن.
2. نام آن را دقیقاً `banner.jpg` بگذار.
3. تصویر قبلی را جایگزین کن.
4. Worker را Deploy کن.

```text
banner.jpg
    │
    ▼
صفحه کاربری
    │
    ▼
نمایش بنر
```

---

## 5) ساخت کانفیگ

کانفیگ را با گزینه‌های زیر می‌توان تنظیم کرد:

```text
┌─────────────────────────┐
│       ساخت کانفیگ       │
├─────────────────────────┤
│ پروتکل                  │
│ نام                     │
│ تعداد                   │
│ حجم                     │
│ مدت زمان                │
│ محدودیت IP              │
│ یادداشت                 │
│ تنظیمات پیشرفته         │
└─────────────────────────┘
```

### پروتکل‌ها

| پروتکل | حالت استفاده |
|---|---|
| VLESS | Worker |
| Trojan | Worker |
| VLESS + Trojan | Worker |
| VMess | لینک / سرور خارجی |
| Shadowsocks | لینک / سرور خارجی |
| Hysteria2 | لینک / سرور خارجی |
| TUIC | لینک / سرور خارجی |
| WireGuard | WARP |

---

## 6) محدودیت حجم

می‌توان برای هر کانفیگ حجم تعیین کرد:

```text
100 MB
   │
   ▼
500 MB
   │
   ▼
1 GB
   │
   ▼
10 GB
   │
   ▼
...
```

`0` یا خالی بودن مقدار، در صورتی که کد همین رفتار را تنظیم کرده باشد، به معنی نامحدود است.

---

## 7) محدودیت زمانی

مدت زمان می‌تواند بر اساس روز، ماه یا سال تنظیم شود.

```text
کاربر
  │
  ▼
فعال شدن کانفیگ
  │
  ▼
شروع زمان
  │
  ▼
اتمام زمان
  │
  ▼
انقضا
```

---

## 8) محدودیت IP همزمان

برای جلوگیری از استفاده همزمان از IPهای بیشتر از مقدار تعیین‌شده، می‌توان سقف IP تعریف کرد.

مثال:

```text
Limit = 2

IP 1  ──► ✅
IP 2  ──► ✅
IP 3  ──► ❌
```

---

## 9) ساب‌لینک

بعد از ساخت کانفیگ، می‌توان لینک Subscription دریافت کرد.

فرمت‌های پروژه شامل مواردی مانند:

```text
Base64
Raw
Clash / Mihomo
sing-box
```

همچنین صفحه کاربر می‌تواند اطلاعات مصرف و زمان باقی‌مانده را نمایش دهد.

---

## 10) تشخیص دستگاه

صفحه کاربر می‌تواند بر اساس دستگاه، راهنمای مناسب را نشان دهد.

```text
                 کاربر
                   │
          ┌────────┼────────┐
          ▼        ▼        ▼
       Android    iOS     Windows
          │        │        │
          ▼        ▼        ▼
       برنامه    برنامه    برنامه
       مناسب     مناسب     مناسب
```

---

## 11) برنامه‌های کلاینت

نمونه برنامه‌های قابل استفاده:

| دستگاه | نمونه برنامه |
|---|---|
| Android | v2rayNG، Hiddify، NekoBox، sing-box |
| iPhone / iPad | Streisand، V2Box، Shadowrocket، sing-box |
| Windows | v2rayN، Hiddify، Clash Verge Rev |
| macOS | Hiddify، V2Box، Clash Verge Rev |
| Linux | Hiddify، NekoRay، v2rayA |

---

## 12) Clean IP

می‌توان چند IP یا دامنه تمیز تعریف کرد.

```text
Clean IP 1
Clean IP 2
Clean IP 3
     │
     ▼
Subscription
     │
     ├── Link 1
     ├── Link 2
     └── Link 3
```

---

## 13) Proxy IP

اگر بعضی مقصدها پشت Cloudflare باشند و اتصال مستقیم مشکل داشته باشد، در صورت پشتیبانی کد می‌توان Proxy IP تعریف کرد.

---

## 14) Kill Switch

با فعال شدن Kill Switch، سرویس‌های مربوط به اتصال‌ها متوقف می‌شوند.

```text
Kill Switch
     │
     ▼
فعال
     │
     ▼
توقف اتصال‌ها
```

---

## 15) ربات تلگرام

در صورت فعال بودن قابلیت ربات، توکن Telegram Bot را در تنظیمات مربوط به Worker قرار بده.

دستورهای مستندشده در نسخه اصلی:

```text
/login
/new
/list
/stats
```

---

## 16) بکاپ و بازگردانی

برای نگهداری اطلاعات، قبل از تغییرات مهم از داده‌ها بکاپ بگیر.

```text
Backup
  │
  ▼
JSON
  │
  ▼
ذخیره امن
```

در صورت نیاز می‌توان بکاپ را بازگردانی کرد.

---

## 17) عیب‌یابی

### اتصال دیتابیس برقرار نیست

Binding دیتابیس Worker را بررسی کن.

### کانفیگ ساخته نمی‌شود

Bindingها و تنظیمات D1 را بررسی کن.

### IP Limit

اگر خطای مربوط به سقف IP دریافت شد، مقدار محدودیت همزمان را بررسی کن.

### Quota / Expired

حجم یا زمان کانفیگ تمام شده است.

### Service Paused

Kill Switch فعال است.

### بعضی سایت‌ها باز نمی‌شوند

دامنه Worker، TLS، پورت، WebSocket و در صورت نیاز Proxy IP را بررسی کن.

---

## 18) محدودیت‌های Cloudflare

محدودیت‌های Cloudflare با توجه به پلن و قوانین فعلی سرویس ممکن است تغییر کنند؛ قبل از استفاده گسترده، محدودیت‌های همان پلن را در داشبورد Cloudflare بررسی کن.

---

# 🇬🇧 English — Short Guide

## Project structure

```text
parham01/
├── worker.js
├── README.md
└── banner.jpg
```

The banner file must be named exactly:

```text
banner.jpg
```

and placed next to `worker.js`.

### Banner flow

```text
Worker
  │
  ▼
banner.jpg
  │
  ▼
User page / banner area
```

Replace `banner.jpg` with a new image whenever you want to change the banner.

## Main features

- VLESS
- Trojan
- VLESS + Trojan
- Subscription links
- Clash / Mihomo
- sing-box
- QR codes
- User page
- Data limits
- Time limits
- Concurrent IP limits
- Clean IP
- Proxy IP
- Bulk configuration
- Kill Switch
- Backup / restore
- Telegram bot

## Important note

This README intentionally documents the user-facing configuration and deployment flow and does not document or expose an admin panel or an `adminme` route.

---

## ⚠️ مسئولیت استفاده

از پروژه مطابق قوانین محل استفاده و شرایط سرویس Cloudflare استفاده کن.
