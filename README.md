# Parham 01 — Config Panel
### پنل مدیریت کانفیگ روی Cloudflare Workers · Cloudflare Workers config panel (single file)

![Parham 01 Banner](banner/banner.jpg)

[فارسی](#-فارسی) · [English](#-english)

---

# 🇮🇷 فارسی

## فهرست
1. [این پروژه چیست؟](#۱-این-پروژه-چیست)
2. [امکانات](#۲-امکانات)
3. [پیش‌نیازها](#۳-پیشنیازها)
4. [نصب قدم‌به‌قدم روی Cloudflare](#۴-نصب-قدمبهقدم-روی-cloudflare)
5. [اولین ورود و امنیت](#۵-اولین-ورود-و-امنیت)
6. [راهنمای Panel](#۶-راهنمای-panel)
7. [ساخت کانفیگ؛ همه‌ی گزینه‌ها](#۷-ساخت-کانفیگ-همهی-گزینهها)
8. [لینک ساب، صفحه‌ی کاربر و برنامه‌های کلاینت](#۸-لینک-ساب-صفحهی-کاربر-و-برنامههای-کلاینت)
9. [تنظیمات Panel](#۹-تنظیمات-panel)
10. [ربات تلگرام](#۱۰-ربات-تلگرام)
11. [آپدیت و بکاپ](#۱۱-آپدیت-و-بکاپ)
12. [عیب‌یابی](#۱۲-عیبیابی)
13. [محدودیت‌های Cloudflare](#۱۳-محدودیتهای-cloudflare)
14. [سوالات متداول](#۱۴-سوالات-متداول)

## ۱) این پروژه چیست؟
یک پنل کامل مدیریت کانفیگ که **فقط در یک فایل (`worker.js`)** روی Cloudflare Workers اجرا می‌شود؛ بدون سرور و بدون VPS.

- **کاربر عادی** با باز کردن آدرس Worker فقط «صفحه‌ی کاربر» را می‌بیند.
- **Panel** برای مدیریت کانفیگ‌ها، کاربران، تنظیمات و آمار استفاده می‌شود.
- داده‌ها در **D1** و اطلاعات موقت/توکن‌های لازم در **KV** ذخیره می‌شوند.

## ۲) امکانات
| امکان | توضیح |
|---|---|
| پروتکل‌های زنده روی Worker | **VLESS**، **Trojan** و **VLESS+Trojan** روی WebSocket + TLS |
| پروتکل‌های لینکی | vmess، shadowsocks، hysteria2، tuic، wireguard |
| محدودیت حجم | MB / GB / TB |
| محدودیت زمان | روز / ماه / سال و شروع از اولین اتصال |
| محدودیت IP همزمان | تعداد IP همزمان قابل تنظیم |
| ساب لینک | Base64، Raw، **Clash/Mihomo**، **sing-box** |
| صفحه‌ی کاربر | مصرف، زمان باقی‌مانده، QR و لینک‌ها |
| تشخیص دستگاه | Android / iOS / Windows / macOS / Linux |
| IP تمیز | چند Clean IP |
| Proxy IP | برای مقصدهای خاص |
| ساخت گروهی و Clone | ساخت سریع چند کانفیگ |
| Kill Switch | توقف سرویس |
| بکاپ و بازگردانی | خروجی/ورودی JSON |
| ربات تلگرام | مدیریت از طریق Telegram |

> ⚠️ **صادقانه:** Cloudflare Workers فقط TCP روی WebSocket را اجازه می‌دهد؛ UDP ندارد. VLESS/Trojan روی Worker اجرا می‌شوند ولی vmess/shadowsocks/hysteria2/tuic/wireguard در این پروژه به‌صورت لینک/کانفیگ استفاده می‌شوند و برای اجرای واقعی به سرور مربوط نیاز دارند.

## ۳) پیش‌نیازها
- یک اکانت Cloudflare
- یک Worker
- در صورت نیاز دامنه‌ی متصل به Cloudflare
- یک D1 Database
- یک KV Namespace
- در صورت استفاده از ربات، Telegram Bot Token

---

# 🟦 ۴) نصب قدم‌به‌قدم روی Cloudflare

## 🗄️ مرحله ۱ — ساخت D1 Database

### مسیر خیلی ساده

```text
☁️ Cloudflare Dashboard
        │
        ▼
🗃️ Storage & databases
        │
        ▼
🟦 D1 SQL database
        │
        ▼
➕ Create database
        │
        ▼
✏️ اسم دیتابیس
        │
        ▼
✅ Create
```

### دقیقاً چه اسمی بگذارم؟

در قسمت نام، این را بگذار:

```text
parham01-db
```

پس:

```text
Database name
      │
      ▼
parham01-db
```

بعد روی **Create database** بزن.

### آیا باید Table بسازم؟

❌ نه.

```text
D1 ساخته شد
    │
    ▼
Table دستی نساز
    │
    ▼
Worker خودش جدول‌های موردنیاز را می‌سازد
```

یعنی کار تو در این مرحله فقط ساخت خود D1 است.

### 🎯 شکل نهایی D1

```text
┌──────────────────────────────┐
│        Cloudflare            │
├──────────────────────────────┤
│ Storage & databases          │
│                              │
│  🗄️ D1                       │
│      └── parham01-db         │
│                              │
│  📌 Table؟                   │
│      ❌ لازم نیست             │
└──────────────────────────────┘
```

---

# 🟪 مرحله ۲ — ساخت KV Namespace

### مسیر خیلی ساده

```text
☁️ Cloudflare Dashboard
        │
        ▼
🗃️ Storage & databases
        │
        ▼
🟪 KV
        │
        ▼
➕ Create a namespace
        │
        ▼
✏️ اسم KV
        │
        ▼
✅ Add
```

### دقیقاً چه اسمی بگذارم؟

اسم Namespace را این بگذار:

```text
parham01-kv
```

پس:

```text
KV Namespace
      │
      ▼
parham01-kv
```

### 🎯 شکل نهایی KV

```text
┌──────────────────────────────┐
│        Cloudflare            │
├──────────────────────────────┤
│ Storage & databases          │
│                              │
│  🟪 KV                        │
│      └── parham01-kv         │
└──────────────────────────────┘
```

---

# 🟨 مرحله ۳ — ساخت Worker

```text
☁️ Cloudflare Dashboard
        │
        ▼
⚙️ Workers & Pages
        │
        ▼
➕ Create application
        │
        ▼
Create Worker
        │
        ▼
✏️ اسم Worker
        │
        ▼
parham01
        │
        ▼
🚀 Deploy
        │
        ▼
Edit code
        │
        ▼
📄 worker.js
        │
        ▼
🚀 Deploy
```

### اسم Worker

پیشنهاد این پروژه:

```text
parham01
```

---

# 🔗 مرحله ۴ — وصل کردن D1 و KV به Worker

این قسمت خیلی مهم است.

## اتصال D1

```text
Worker
  │
  ▼
Settings
  │
  ▼
Bindings
  │
  ▼
Add
  │
  ▼
D1 database
  │
  ├── Variable name → DB
  │
  └── D1 database → parham01-db
```

### دقیقاً این‌طور پر کن:

```text
┌─────────────────────────────────┐
│ Add Binding                     │
├─────────────────────────────────┤
│ Type:                           │
│ 🗄️ D1 database                  │
│                                 │
│ Variable name:                  │
│ DB                              │
│                                 │
│ D1 database:                    │
│ parham01-db                     │
└─────────────────────────────────┘
```

⚠️ اسم Variable را دقیقاً بگذار:

```text
DB
```

نه:

```text
db
database
D1
PARHAM_DB
```

فقط:

```text
DB
```

---

## اتصال KV

دوباره:

```text
Worker
  │
  ▼
Settings
  │
  ▼
Bindings
  │
  ▼
Add
  │
  ▼
KV namespace
```

بعد:

```text
┌─────────────────────────────────┐
│ Add Binding                     │
├─────────────────────────────────┤
│ Type:                           │
│ 🟪 KV namespace                 │
│                                 │
│ Variable name:                  │
│ KV                              │
│                                 │
│ KV namespace:                   │
│ parham01-kv                     │
└─────────────────────────────────┘
```

⚠️ Variable name دقیقاً:

```text
KV
```

---

# 🧠 نقشه‌ی کامل برای کسی که اولین بار انجام می‌دهد

اگر هیچ‌چیز از Cloudflare نمی‌دانی، فقط این نقشه را دنبال کن:

```text
                 ☁️ CLOUDFLARE
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       🗄️ D1        🟪 KV        ⚙️ Worker
          │            │            │
          │            │            │
  parham01-db    parham01-kv     parham01
          │            │            │
          └──────┐  ┌──┘            │
                 │  │               │
                 ▼  ▼               ▼
                DB  KV         📄 worker.js
                 \  /               │
                  \/                │
              🔗 Bindings ◄─────────┘
                       │
                       ▼
                    🚀 Deploy
```

### اسم‌هایی که باید داشته باشی

| چیز | اسم پیشنهادی |
|---|---|
| Worker | `parham01` |
| D1 Database | `parham01-db` |
| D1 Variable | `DB` |
| KV Namespace | `parham01-kv` |
| KV Variable | `KV` |
| فایل کد | `worker.js` |

### ✅ چک نهایی

```text
☑️ Worker = parham01
☑️ D1 = parham01-db
☑️ D1 Binding = DB
☑️ KV = parham01-kv
☑️ KV Binding = KV
☑️ worker.js داخل Worker قرار گرفته
☑️ Deploy انجام شده
```

اگر همه‌ی تیک‌ها درست است، اتصال اصلی آماده است.

---

## ۵) اولین ورود و امنیت

بعد از Deploy، آدرس Worker را باز کن و وارد **Panel** شو.

> مسیر ورود دقیق Panel را مطابق کد `worker.js` پروژه استفاده کن. این README عمداً مسیر قدیمی `adminme` را استفاده نمی‌کند.

---

## ۶) راهنمای Panel

| صفحه | کار |
|---|---|
| **Dashboard** | آمار، جدول کانفیگ‌ها، نمودار و اعلان‌ها |
| **Configs / Users** | لیست، فیلتر، جستجو، Clone، ریست مصرف و فعال/غیرفعال |
| **Add config** | ساخت کانفیگ |
| **Update** | آپدیت Worker |
| **Settings** | دامنه، Clean IP، Proxy IP، Kill Switch و بکاپ |
| **Telegram bot** | اتصال ربات تلگرام |

دکمه‌های هر ردیف:

```text
✏️ ویرایش
🗑️ حذف
▦ QR و لینک‌ها
🔗 کپی Subscription
📋 کپی لینک مستقیم
📑 Clone
🔄 Reset
⏸️ / ▶️ فعال و غیرفعال
```

## ۷) ساخت کانفیگ؛ همه‌ی گزینه‌ها

**پروتکل** — بالای صفحه انتخاب می‌کنی:

| پروتکل | اجرا | توضیح |
|---|---|---|
| vless | Worker | پروتکل اصلی Worker |
| trojan | Worker | رمز Trojan همان شناسه کانفیگ |
| vless+trojan | Worker | هر دو با یک محدودیت |
| vmess / shadowsocks / hysteria2 / tuic | سرور بیرونی | ساخت لینک |
| wireguard | WARP | لینک + فایل `.conf` |

**نام** — دکمه‌ی 🎲 نام تصادفی می‌سازد.

**تعداد** — ساخت گروهی ۱ تا ۵۰.

**حجم** — MB / GB / TB؛ صفر یا خالی = نامحدود.

**مدت زمان** — روز / ماه / سال؛ صفر = بدون انقضا.

**محدودیت IP همزمان** — مثلاً `2` یعنی حداکثر دو IP همزمان.

**یادداشت** — برای اطلاعات داخلی خودت.

**تنظیمات پیشرفته** — آدرس، پورت، TLS، SNI و Fingerprint.

بعد از ساخت:

```text
کانفیگ
  │
  ├── 🔗 Subscription
  ├── 📱 Add to app
  ├── ▦ QR
  ├── 🔗 Direct link
  └── 👤 User page
```

## ۸) لینک ساب، صفحه‌ی کاربر و برنامه‌های کلاینت

| لینک | کاربرد |
|---|---|
| `/sub/<id>` | Subscription |
| `?format=raw` | لینک‌های ساده |
| `?format=clash` | Clash Meta / Mihomo |
| `?format=singbox` | sing-box |
| `/u/<id>` | صفحه‌ی کاربر |

## ۹) تنظیمات Panel

- **Worker domain:** دامنه‌ای که لینک‌ها با آن ساخته می‌شوند.
- **Clean IP list:** هر خط یک IP یا دامنه.
- **Proxy IP:** آدرس Proxy در صورت نیاز.
- **External server address:** آدرس پیش‌فرض پروتکل‌های خارجی.
- **Auto-name prefix:** پیشوند نام خودکار.
- **Kill Switch:** توقف اتصال‌ها.
- **Backup:** دانلود و بازگردانی JSON.

## ۱۰) ربات تلگرام

1. با BotFather ربات بساز.
2. Token را دریافت کن.
3. در **Panel → Telegram bot** وارد کن.
4. ربات را طبق دستورهای پروژه استفاده کن.

دستورهای اصلی:

```text
/new
/list
/stats
```

## ۱۱) آپدیت و بکاپ

```text
Panel
  │
  ▼
Settings
  │
  ├── Download backup
  │
  ▼
Worker
  │
  ▼
Edit code
  │
  ▼
worker.js جدید
  │
  ▼
Deploy
```

داده‌های D1 و KV جدا از کد Worker نگهداری می‌شوند.

## ۱۲) عیب‌یابی

| مشکل | علت و راه‌حل |
|---|---|
| Database connection required | Binding با نام دقیق `DB` را بررسی کن |
| مشکل ذخیره‌سازی | Binding با نام دقیق `KV` را بررسی کن |
| خطا هنگام ساخت کانفیگ | اتصال D1 و Deploy را بررسی کن |
| `429 ip limit reached` | سقف IP همزمان پر شده |
| `403 quota exceeded / expired` | حجم یا زمان تمام شده |
| `503 service paused` | Kill Switch روشن است |
| بعضی سایت‌ها باز نمی‌شوند | Proxy IP را بررسی کن |
| وصل نمی‌شود | Domain، TLS، Port و WebSocket را بررسی کن |
| Error 1101 | Bindingها و Deploy را بررسی کن |

## ۱۳) محدودیت‌های Cloudflare

- Workers محدودیت مصرف و درخواست دارد.
- D1 برای ذخیره داده‌های پروژه استفاده می‌شود.
- KV برای داده‌های کلیدی/موقت استفاده می‌شود.
- Worker در این پروژه برای اتصال‌های WebSocket استفاده می‌شود.
- مصرف واقعی ممکن است با آمار کلاینت کمی اختلاف داشته باشد.

## ۱۴) سوالات متداول

**آیا Table را باید دستی بسازم؟**  
خیر؛ طبق ساختار پروژه Worker جدول‌های لازم را می‌سازد.

**اسم D1 چه باشد؟**  
```text
parham01-db
```

**اسم KV چه باشد؟**  
```text
parham01-kv
```

**اسم Binding D1 چه باشد؟**  
```text
DB
```

**اسم Binding KV چه باشد؟**  
```text
KV
```

**فایل اصلی پروژه چیست؟**  
```text
worker.js
```

**ساختار پروژه چیست؟**

```text
parham01/
├── worker.js
├── README.md
└── banner/
    └── banner.jpg
```

**آیا `adminme` در این README وجود دارد؟**  
خیر؛ در این نسخه از عبارت `adminme` استفاده نشده و بخش مدیریت با نام **Panel** توضیح داده شده است.

**⚠️ سلب مسئولیت:** از این پروژه مطابق قوانین محل استفاده و شرایط Cloudflare استفاده کن.

---

# 🇬🇧 English

## Contents
1. What is it?
2. Features
3. Requirements
4. Cloudflare setup
5. First login & security
6. Panel guide
7. Creating a config
8. Subscriptions & user page
9. Panel settings
10. Telegram bot
11. Update & backup
12. Troubleshooting
13. Cloudflare limits
14. FAQ

## 1) What is it?

A config-management panel running on Cloudflare Workers using a single `worker.js` file.

- Normal visitors see the user page.
- **Panel** is used for configuration and user management.
- Project data is stored in D1 and required temporary/key-value data can be stored in KV.

## 2) Features

- VLESS
- Trojan
- VLESS + Trojan
- vmess / shadowsocks / hysteria2 / tuic links
- WireGuard/WARP configuration
- Data and time limits
- Concurrent IP limits
- Subscription formats
- QR codes
- User page
- Clean IP
- Proxy IP
- Bulk creation
- Clone
- Search and filters
- Kill Switch
- Backup / restore
- Telegram bot

## 3) Requirements

- Cloudflare account
- Worker
- D1 database
- KV namespace
- Optional custom domain
- Optional Telegram bot

## 4) Cloudflare setup

### D1

```text
Cloudflare
   ↓
Storage & databases
   ↓
D1 SQL database
   ↓
Create database
   ↓
Name: parham01-db
```

No manual tables are required.

### KV

```text
Cloudflare
   ↓
Storage & databases
   ↓
KV
   ↓
Create a namespace
   ↓
Name: parham01-kv
```

### Worker

```text
Workers & Pages
   ↓
Create application
   ↓
Create Worker
   ↓
Name: parham01
   ↓
Edit code
   ↓
worker.js
   ↓
Deploy
```

### Bindings

D1:

```text
Type: D1 database
Variable name: DB
Database: parham01-db
```

KV:

```text
Type: KV namespace
Variable name: KV
Namespace: parham01-kv
```

Final structure:

```text
                 CLOUDFLARE
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   D1 Database   KV Namespace   Worker
   parham01-db   parham01-kv    parham01
        │            │             │
        ▼            ▼             ▼
       DB           KV        worker.js
        └────────────┴─────────────┘
                    │
                 Deploy
```

## 5) First login & security

Open the Worker URL and use the project's **Panel** entry point.

> This README does not use the old `adminme` path/name. The exact Panel route should match the current `worker.js`.

## 6) Panel guide

The Panel provides:

- Dashboard
- Configs / Users
- Add config
- Update
- Settings
- Telegram bot
- QR and subscription links
- Clone / reset / enable / disable

## 7) Creating a config

Choose the protocol, name, count, data limit, time limit, concurrent IP limit and advanced settings.

## 8) Subscriptions & user page

```text
/sub/<id>
/sub/<id>?format=raw
/sub/<id>?format=clash
/sub/<id>?format=singbox
/u/<id>
```

## 9) Panel settings

Configure Worker domain, Clean IPs, Proxy IP, external server address, auto-name prefix, Kill Switch and backup.

## 10) Telegram bot

Create the bot with BotFather, add the token in the **Panel**, then use the supported commands.

## 11) Update & backup

```text
Panel
  ↓
Settings
  ↓
Download backup
  ↓
Worker
  ↓
Edit code
  ↓
worker.js
  ↓
Deploy
```

## 12) Troubleshooting

Check the D1 binding `DB`, KV binding `KV`, domain, TLS, port, WebSocket and Deploy status.

## 13) Cloudflare limits

Cloudflare Workers, D1 and KV have plan-specific usage limits. Check the current Cloudflare plan documentation for exact limits.

## 14) FAQ

**D1 name:** `parham01-db`  
**D1 binding:** `DB`  
**KV name:** `parham01-kv`  
**KV binding:** `KV`  
**Worker:** `parham01`  
**Code file:** `worker.js`

Project structure:

```text
parham01/
├── worker.js
├── README.md
└── banner/
    └── banner.jpg
```

---

## 📁 ساختار فایل نهایی

```text
parham01/
├── worker.js
├── README.md
└── banner/
    └── banner.jpg
```
