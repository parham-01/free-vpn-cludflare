# Parham 01 — Config Panel
### پنل مدیریت کانفیگ روی Cloudflare Workers · Cloudflare Workers config panel (single file)

[فارسی](#-فارسی) · [English](#-english)

---

# 🇮🇷 فارسی

## 📁 ساختار پروژه

```text
parham01/
├── worker.js
├── README.md
└── banner/
    └── banner.jpg
```


## فهرست
1. [این پروژه چیست؟](#۱-این-پروژه-چیست)
2. [امکانات](#۲-امکانات)
3. [پیش‌نیازها](#۳-پیشنیازها)
4. [نصب قدم‌به‌قدم روی Cloudflare](#۴-نصب-قدمبهقدم-روی-cloudflare)
5. [ساخت کانفیگ؛ همه‌ی گزینه‌ها](#۷-ساخت-کانفیگ-همهی-گزینهها)
8. [لینک ساب، صفحه‌ی کاربر و برنامه‌های کلاینت](#۸-لینک-ساب-صفحهی-کاربر-و-برنامههای-کلاینت)
9. [تنظیمات پنل](#۹-تنظیمات-پنل)
10. [ربات تلگرام](#۱۰-ربات-تلگرام)
11. [آپدیت و بکاپ](#۱۱-آپدیت-و-بکاپ)
12. [عیب‌یابی](#۱۲-عیبیابی)
13. [محدودیت‌های Cloudflare](#۱۳-محدودیتهای-cloudflare)
14. [سوالات متداول](#۱۴-سوالات-متداول)

## ۱) این پروژه چیست؟
یک پنل کامل مدیریت کانفیگ که **فقط در یک فایل (`worker.js`)** روی Cloudflare Workers اجرا می‌شود؛ بدون سرور و بدون VPS.

- **کاربر عادی** با باز کردن آدرس Worker فقط «پنل کاربران» را می‌بیند (بررسی مصرف و دانلود برنامه).
- داده‌ها در **D1** (دیتابیس) و توکن ورود در **KV** ذخیره می‌شوند.

## ۲) امکانات
| امکان | توضیح |
|---|---|
| پروتکل‌های زنده روی Worker | **VLESS**، **Trojan** و **VLESS+Trojan** (هر دو با یک شناسه) روی WebSocket + TLS |
| پروتکل‌های لینکی | vmess، shadowsocks، hysteria2، tuic، wireguard (فقط ساخت لینک؛ نیاز به سرور بیرونی. WireGuard با اکانت رایگان WARP) |
| محدودیت حجم (واقعی) | MB / GB / TB؛ ترافیک رفت و برگشت شمارش می‌شود و با تمام‌شدن حجم اتصال قطع می‌شود |
| محدودیت زمان (واقعی) | روز / ماه / سال؛ گزینه‌ی «شروع از اولین اتصال» |
| محدودیت تعداد IP همزمان (واقعی) | IP جدیدی که از سقف بگذرد رد می‌شود (۰ = نامحدود) |
| ساب لینک | Base64 ، Raw ، **Clash/Mihomo** ، **sing-box** + هدر مصرف و انقضا برای برنامه‌ها |
| صفحه‌ی کاربر | `/u/<شناسه>` مصرف، زمان باقی‌مانده، QR و دکمه‌ی افزودن به برنامه |
| تشخیص خودکار دستگاه | اندروید / iOS / ویندوز / مک / لینوکس؛ متن‌ها، برنامه‌های پیشنهادی و دکمه‌ها بر اساس دستگاه عوض می‌شود و چیدمان موبایل (کارت) جدا دارد |
| IP تمیز (Clean IP) | چند آدرس؛ ساب برای هرکدام یک لینک می‌سازد |
| Proxy IP | برای سایت‌هایی که پشت خود Cloudflare هستند |
| ساخت گروهی، Clone، یادداشت، فیلتر، جستجو، حذف منقضی‌ها | مدیریت راحت‌تر |
| Kill Switch | توقف کل سرویس با یک کلید |
| بکاپ و بازگردانی | خروجی/ورودی JSON |
| امنیت ورود | قفل ۱۰ دقیقه‌ای بعد از ۵ رمز اشتباه، کوکی HttpOnly، توکن در KV |
| ربات تلگرام | `/login` ، `/new` ، `/list` ، `/stats` |

> ⚠️ **صادقانه:** Cloudflare Workers فقط TCP روی WebSocket را اجازه می‌دهد؛ UDP ندارد. پس VLESS/Trojan **واقعاً روی Worker اجرا می‌شوند** ولی vmess/shadowsocks/hysteria2/tuic/wireguard فقط **لینک** ساخته می‌شوند و باید خودت سرورشان را جای دیگر داشته باشی.

## ۳) پیش‌نیازها
- یک اکانت رایگان Cloudflare: <https://dash.cloudflare.com/sign-up>
- (پیشنهادی) یک دامنه‌ی خودت روی Cloudflare. دامنه‌ی `*.workers.dev` هم کار می‌کند ولی در بعضی شبکه‌ها فیلتر است.
- (اختیاری) توکن ربات تلگرام از [@BotFather](https://t.me/BotFather)

## ۴) نصب قدم‌به‌قدم روی Cloudflare
> اسم دکمه‌ها ممکن است در داشبورد Cloudflare کمی عوض شده باشد؛ مسیر کلی همین است.

### قدم ۱ — ساخت دیتابیس D1
1. وارد <https://dash.cloudflare.com> شو.
2. از منوی چپ: **Storage & databases** ← **D1 SQL database**.
3. روی **Create database** بزن.
4. یک اسم بده (مثلاً `parham01-db`) و **Create** را بزن.
5. هیچ جدولی نیاز نیست بسازی؛ خود Worker جدول‌ها را می‌سازد.

### قدم ۲ — ساخت KV
1. منوی چپ: **Storage & databases** ← **KV**.
2. **Create a namespace** ← اسم: `parham01-kv` ← **Add**.

### قدم ۳ — ساخت Worker
1. منوی چپ: **Compute (Workers)** ← **Workers & Pages** ← **Create application** ← **Create Worker** (یا Start with Hello World).
2. یک اسم بده (مثلاً `parham01`) ← **Deploy**.
3. روی **Edit code** بزن.
4. همه‌ی کد پیش‌فرض را پاک کن، کل فایل **`worker.js`** این پروژه را Paste کن.
5. بالا سمت راست **Deploy** بزن.

### قدم ۴ — وصل کردن D1 و KV (مهم‌ترین قدم)
1. صفحه‌ی همان Worker ← **Settings** ← **Bindings** ← **Add**.
2. نوع **D1 database** را انتخاب کن:
   - **Variable name:** دقیقاً `DB` (حروف بزرگ)
   - **D1 database:** دیتابیسی که ساختی ← **Save**
3. دوباره **Add** ← نوع **KV namespace**:
   - **Variable name:** دقیقاً `KV` (حروف بزرگ)
   - **KV namespace:** همانی که ساختی ← **Save**
4. بعد از ذخیره، Worker را **یک بار دیگر Deploy** کن (اگر دکمه‌ی Deploy فعال بود).

> بدون `DB` پنل پیام «اتصال دیتابیس لازم است» می‌دهد. بدون `KV` پنل کار می‌کند ولی توکن ورود در D1 ذخیره می‌شود (بهتر است KV را وصل کنی).

### قدم ۵ — دامنه (پیشنهادی)
1. Worker ← **Settings** ← **Domains & Routes** ← **Add** ← **Custom domain**.
2. زیر‌دامنه‌ی دلخواه را بنویس، مثلاً `p.example.com` ← **Add domain**.
3. چند دقیقه صبر کن تا گواهی TLS فعال شود.
4. حتماً مطمئن شو **WebSockets** در دامنه‌ی Cloudflare روشن است (Network ← WebSockets = On؛ به‌صورت پیش‌فرض روشن است).

### قدم ۶ — ورود
آدرس را در مرورگر باز کن:
```
https://YOUR-WORKER-DOMAIN/adminme/
```

سپس در پنل برو **تنظیمات** ← «دامنه Worker» را بنویس (مثلاً `p.example.com`) ← **ذخیره**؛ تا لینک‌ها با دامنه‌ی درست ساخته شوند.

## ۷) ساخت کانفیگ؛ همه‌ی گزینه‌ها

> 🧩 **نقشه‌ی ساخت کانفیگ**
>
> ```text
> پروتکل
>   ↓
> نام + تعداد
>   ↓
> حجم + زمان
>   ↓
> محدودیت IP
>   ↓
> تنظیمات پیشرفته
>   ↓
> 🔗 لینک / QR / Subscription
> ```
>
**پروتکل** — بالای صفحه انتخاب می‌کنی:

| پروتکل | اجرا | توضیح |
|---|---|---|
| vless | Worker | پیشنهادی |
| trojan | Worker | رمز Trojan همان شناسه‌ی کانفیگ است |
| vless+trojan | Worker | هر دو لینک با یک حجم/زمان/IP |
| vmess / shadowsocks / hysteria2 / tuic | سرور بیرونی | لینک برای سرور خودت (آدرس را در «تنظیمات پیشرفته» یا «تنظیمات» بده) |
| wireguard | WARP | کلید از Cloudflare WARP ساخته می‌شود؛ لینک + فایل `.conf` |

**نام** — کنار آن دکمه‌ی 🎲 است که نام تصادفی می‌سازد. نام خالی بماند هم خودکار پر می‌شود (پیشوند را در تنظیمات عوض کن).

**تعداد** — ساخت گروهی (۱ تا ۵۰) با نام‌های شماره‌دار.

**حجم** — عدد + واحد (MB/GB/TB). `۰` یا خالی = نامحدود. مصرف هر ۳۰ ثانیه ذخیره و بررسی می‌شود؛ وقتی تمام شود اتصال‌های باز هم قطع می‌شوند.

**مدت زمان** — عدد + روز/ماه/سال. `۰` = بدون انقضا. گزینه‌ی **شروع از اولین اتصال**: ساعت انقضا از اولین باری که کاربر وصل شد شروع می‌شود.

**محدودیت اتصال (آیپی همزمان)** — کلید را روشن کن و عدد بده. `۰` = نامحدود (No Limit). مثلاً `2` یعنی فقط ۲ IP متفاوت همزمان؛ IP سوم رد می‌شود. چند اتصال از همان IP فقط یکی حساب می‌شود. IP که ۹۰ ثانیه فعالیتی نداشته باشد از شمارش خارج می‌شود.

**یادداشت** — فقط برای خودت (نام مشتری و…).

**تنظیمات پیشرفته (پروتکل‌های Worker):**
- **آدرس / IP تمیز:** خالی = دامنه‌ی Worker (یا لیست IP تمیز تنظیمات).
- **پورت:** پیش‌فرض ۴۴۳ (با TLS) / ۸۰ (بدون TLS). پورت‌های TLS کلودفلر: 443, 8443, 2053, 2083, 2087, 2096؛ بدون TLS: 80, 8080, 8880, 2052, 2082, 2086, 2095.
- **TLS:** پیشنهاد می‌شود روشن بماند.
- **SNI سفارشی** و **Fingerprint** (chrome، firefox، safari، ios، android، edge، random).

بعد از ساخت، پنجره‌ی لینک‌ها باز می‌شود: QR، کپی ساب، Clash، sing-box، صفحه‌ی کاربر، دکمه‌های «افزودن به برنامه» مخصوص دستگاه تو، و لینک‌های مستقیم.

## ۸) لینک ساب، صفحه‌ی کاربر و برنامه‌های کلاینت

> 🔗 **مسیر کلی استفاده**
>
> ```text
> کانفیگ
>   ↓
> Subscription
>   ├── Base64
>   ├── Raw
>   ├── Clash / Mihomo
>   └── sing-box
>         ↓
>       کلاینت کاربر
> ```
>
| لینک | کاربرد |
|---|---|
| `https://دامنه/sub/<شناسه>` | ساب پیش‌فرض (Base64). برنامه‌های Clash/Mihomo را خودکار تشخیص می‌دهد |
| `...?format=raw` | لینک‌های ساده، هر خط یکی |
| `...?format=clash` | فایل Clash Meta / Mihomo |
| `...?format=singbox` | فایل sing-box (پایه) |
| `https://دامنه/u/<شناسه>` | صفحه‌ی مصرف و راهنمای کاربر |

ساب هدر `subscription-userinfo` دارد؛ برنامه‌ها مصرف و تاریخ انقضا را نشان می‌دهند.

**برنامه‌های پیشنهادی (پنل خودش بر اساس دستگاه نشان می‌دهد):**
| دستگاه | برنامه‌ها |
|---|---|
| Android | v2rayNG، Hiddify، NekoBox، sing-box |
| iPhone / iPad | Streisand، V2Box، Shadowrocket، sing-box |
| Windows | v2rayN، Hiddify، Clash Verge Rev |
| macOS | Hiddify، V2Box، Clash Verge Rev |
| Linux | Hiddify، NekoRay، v2rayA |

دکمه‌ی «افزودن به برنامه» با لینک عمیق (deep link) برنامه را باز می‌کند؛ اگر باز نشد، لینک ساب را کپی کن و در برنامه Paste کن. لینک فروشگاه‌ها ممکن است تغییر کند؛ در صورت لزوم اسم برنامه را در App Store / GitHub جستجو کن.

## ۹) تنظیمات پنل
- **دامنه Worker:** دامنه‌ای که لینک‌ها با آن ساخته می‌شود.
- **لیست IP تمیز:** هر خط یک IP/دامنه؛ ساب برای هرکدام یک لینک می‌دهد.
- **Proxy IP:** اگر کاربر به سایتی که خودش پشت Cloudflare است وصل نشد، Worker از این آدرس عبور می‌کند (`ip` یا `ip:port` یا دامنه). اختیاری.
- **آدرس سرور بیرونی:** پیش‌فرض برای vmess/ss/hysteria2/tuic.
- **پیشوند نام خودکار:** مثلاً `Parham` → `Parham_a1b2`.
- **Kill Switch:** همه‌ی اتصال‌ها متوقف می‌شوند (حداکثر ۳۰ ثانیه برای قطع اتصال‌های باز).
- **تغییر رمز عبور**، **بکاپ** (دانلود/بازگردانی JSON).

## ۱۰) ربات تلگرام
1. در [@BotFather](https://t.me/BotFather) ربات بساز و توکن را بگیر.
2. در پنل: ربات تلگرام (یا کادر سمت راست داشبورد) ← توکن ← **تایید**.
3. در تلگرام به ربات، دستور `/login` را طبق تنظیمات پروژه ارسال کن.
4. دستورها: `/new` ساخت VLESS ، `/list` لیست، `/stats` آمار.

## ۱۱) آپدیت و بکاپ
1. **تنظیمات ← دانلود بکاپ**.
2. Worker ← **Edit code** ← کد جدید را جایگزین کن ← **Deploy**.
3. داده‌ها در D1/KV می‌مانند؛ چیزی پاک نمی‌شود.
4. اگر چیزی خراب شد: تنظیمات ← بازگردانی بکاپ.

## ۱۲) عیب‌یابی

> 🛠️ **قبل از بررسی خطاها**
>
> ```text
> Worker → Bindings → D1/KV → Domain → TLS/WebSocket → Config
> ```
>
| مشکل | علت و راه‌حل |
|---|---|
| «اتصال دیتابیس لازم است» | Binding دیتابیس با نام **دقیق** `DB` وصل نیست (قدم ۴) |
| هنگام ساخت کانفیگ خطا | پیام خطا حالا علت واقعی را نشان می‌دهد. معمولاً Binding `DB` درست نیست. جدول‌های این نسخه با پیشوند `p01_` ساخته می‌شوند و با جدول‌های نسخه‌های قبلی تداخل ندارند |
| `429 ip limit reached` | سقف IP همزمان پر است؛ سقف را بالا ببر یا ۹۰ ثانیه صبر کن |
| `403 quota exceeded / expired` | حجم تمام یا زمان تمام شده؛ ویرایش یا ریست مصرف |
| `503 service paused` | Kill Switch روشن است |
| وصل می‌شود ولی بعضی سایت‌ها باز نمی‌شوند | آن سایت‌ها پشت Cloudflare هستند؛ **Proxy IP** را در تنظیمات بگذار |
| وصل نمی‌شود | دامنه‌ی Worker در تنظیمات درست باشد، TLS روشن، پورت درست، WebSocket روشن باشد |
| QR نمایش داده نمی‌شود | کتابخانه‌ی QR از cdnjs لود می‌شود؛ اینترنت/فیلتر را چک کن. لینک و ساب کپی‌شدنی هستند |
| Error 1101 | معمولاً Binding ها ناقص‌اند؛ دوباره Deploy کن |

## ۱۳) محدودیت‌های Cloudflare
- پلن رایگان Workers: حدود **۱۰۰ هزار درخواست در روز** (هر اتصال WebSocket یک درخواست).
- D1 رایگان: حدود ۱۰۰ هزار نوشتن در روز. هر اتصال فعال هر ۳۰ ثانیه چند نوشتن دارد؛ برای کاربران زیاد، `flushEvery` را در ابتدای فایل بزرگ‌تر کن (دقت قطع حجم کمتر می‌شود).
- KV رایگان: ۱۰۰۰ نوشتن در روز (فقط ورودهای ادمین).
- فقط TCP؛ UDP (مثل DNS روی VLESS) پشتیبانی نمی‌شود.
- مصرف حجم تقریباً بایت‌های عبوری از Worker است و ممکن است با آمار کلاینت چند درصد اختلاف داشته باشد.

## ۱۴) سوالات متداول
**فقط یک فایل کافی است؟** بله، `worker.js`.

**آیا کاربر عادی چیزی از ادمین می‌بیند؟** نه. `/` پنل کاربران است و مسیرهای ناشناخته 404 می‌دهند.

**می‌توانم vmess روی خود Worker داشته باشم؟** خیر؛ این نسخه فقط لینکش را می‌سازد.

**⚠️ سلب مسئولیت:** از این پروژه مطابق قوانین کشور خودت و شرایط استفاده‌ی Cloudflare استفاده کن. مسئولیت استفاده با خود شماست.

---

# 🇬🇧 English

## Contents
1. [What is it?](#1-what-is-it) · 2. [Features](#2-features) · 3. [Requirements](#3-requirements) · 4. [Cloudflare setup step by step](#4-cloudflare-setup-step-by-step) · 5. [Creating a config](#7-creating-a-config-every-option) · 8. [Subscriptions, user page & client apps](#8-subscriptions-user-page--client-apps) · 9. [Settings](#9-settings) · 10. [Telegram bot](#10-telegram-bot) · 11. [Update & backup](#11-update--backup) · 12. [Troubleshooting](#12-troubleshooting) · 13. [Cloudflare limits](#13-cloudflare-limits) · 14. [FAQ](#14-faq)

## 1) What is it?
A complete config-management panel that runs on **Cloudflare Workers in a single file (`worker.js`)** — no VPS needed.

- **Normal visitors** opening the Worker URL only see a *User Portal* (usage check + app downloads).

## 2) Features
| Feature | Details |
|---|---|
| Live protocols on the Worker | **VLESS**, **Trojan**, **VLESS+Trojan** (one ID) over WebSocket + TLS |
| Link-only protocols | vmess, shadowsocks, hysteria2, tuic, wireguard (links only; needs an external server. WireGuard uses a free WARP account) |
| Data limit (enforced) | MB / GB / TB, both directions counted; connections are cut when exhausted |
| Time limit (enforced) | days / months / years, plus “start on first use” |
| Concurrent IP limit (enforced) | A new IP over the cap is rejected (0 = unlimited) |
| Subscription | Base64, Raw, **Clash/Mihomo**, **sing-box**, with usage/expiry header |
| User page | `/u/<id>`: usage, time left, QR, “add to app” button |
| Automatic device detection | Android / iOS / Windows / macOS / Linux — texts, recommended apps and buttons adapt; mobile gets a card layout |
| Clean IPs | Multiple addresses → one link each in the subscription |
| Proxy IP | For destinations hosted behind Cloudflare itself |
| Bulk create, clone, notes, filters, search, purge expired | Easier management |
| Kill switch · Backup/restore · Login lockout · Telegram bot | Operations & safety |

> ⚠️ **Honest note:** Workers allow only TCP over WebSocket (no UDP). VLESS/Trojan **really run on the Worker**; vmess/shadowsocks/hysteria2/tuic/wireguard are **links only** and need your own server elsewhere.

## 3) Requirements
- A free Cloudflare account: <https://dash.cloudflare.com/sign-up>
- (Recommended) Your own domain on Cloudflare. `*.workers.dev` also works but is blocked in some networks.
- (Optional) A Telegram bot token from [@BotFather](https://t.me/BotFather)

## 4) Cloudflare setup step by step
> Button names may differ slightly as the dashboard evolves; the path is the same.

### Step 1 — Create the D1 database
1. Open <https://dash.cloudflare.com>.
2. Left menu: **Storage & databases** → **D1 SQL database**.
3. Click **Create database**, name it (e.g. `parham01-db`), click **Create**.
4. You don't need to create tables — the Worker creates them.

### Step 2 — Create the KV namespace
1. Left menu: **Storage & databases** → **KV**.
2. **Create a namespace** → name `parham01-kv` → **Add**.

### Step 3 — Create the Worker
1. Left menu: **Compute (Workers)** → **Workers & Pages** → **Create application** → **Create Worker**.
2. Name it (e.g. `parham01`) → **Deploy**.
3. Click **Edit code**.
4. Delete the sample code and paste the entire **`worker.js`**.
5. Click **Deploy** (top right).

### Step 4 — Bind D1 and KV (most important)
1. In the Worker: **Settings** → **Bindings** → **Add**.
2. Choose **D1 database**:
   - **Variable name:** exactly `DB` (uppercase)
   - **D1 database:** the one you created → **Save**
3. **Add** again → **KV namespace**:
   - **Variable name:** exactly `KV` (uppercase)
   - **KV namespace:** the one you created → **Save**
4. Deploy the Worker once more if the Deploy button is active.

> Without `DB` the panel shows “database connection required”. Without `KV` it still works but session tokens fall back to D1 (connect KV anyway).

### Step 5 — Domain (recommended)
1. Worker → **Settings** → **Domains & Routes** → **Add** → **Custom domain**.
2. Enter e.g. `p.example.com` → **Add domain**; wait a few minutes for TLS.
3. Make sure **WebSockets** is On for the zone (Network → WebSockets; default is On).

### Step 6 — Log in
```
https://YOUR-WORKER-DOMAIN/adminme/
```
Default password: **`parham`**

Then go to **Settings**, set **Worker domain** (e.g. `p.example.com`) and save, so links use the right host.

## 7) Creating a config (every option)
**Protocol** — pick at the top:

| Protocol | Runs on | Notes |
|---|---|---|
| vless | Worker | Recommended |
| trojan | Worker | Trojan password = config ID |
| vless+trojan | Worker | Both links share one quota/time/IP limit |
| vmess / shadowsocks / hysteria2 / tuic | External server | Link for your own server (set address in Advanced or Settings) |
| wireguard | WARP | Keys generated from Cloudflare WARP; link + `.conf` |

**Name** — the 🎲 button generates a random name; leaving it empty auto-fills (change prefix in Settings).

**Count** — bulk create (1–50) with numbered names.

**Data** — number + unit (MB/GB/TB). `0`/empty = unlimited. Usage is saved and checked every 30 s; open connections are cut when it runs out.

**Time** — number + days/months/years. `0` = no expiry. **Start on first use** starts the clock at the user's first connection.

**Connection limit (concurrent IPs)** — switch on and enter a number. `0` = unlimited (No Limit). E.g. `2` allows only 2 different IPs at once; a 3rd IP is rejected. Multiple connections from one IP count once. An IP idle for 90 s leaves the count.

**Note** — for you only (customer name…).

**Advanced (Worker protocols):**
- **Address / clean IP:** empty = Worker domain (or the clean-IP list from Settings).
- **Port:** default 443 (TLS) / 80 (no TLS). Cloudflare TLS ports: 443, 8443, 2053, 2083, 2087, 2096; non-TLS: 80, 8080, 8880, 2052, 2082, 2086, 2095.
- **TLS:** keep it on.
- **Custom SNI** and **Fingerprint** (chrome, firefox, safari, ios, android, edge, random).

After creating, the links window opens: QR, copy subscription, Clash, sing-box, user page, device-specific “Add to app” buttons, and direct links.

## 8) Subscriptions, user page & client apps
| Link | Use |
|---|---|
| `https://domain/sub/<id>` | Default (Base64); auto-detects Clash/Mihomo apps |
| `...?format=raw` | Plain links, one per line |
| `...?format=clash` | Clash Meta / Mihomo file |
| `...?format=singbox` | sing-box (basic) |
| `https://domain/u/<id>` | User usage page & guide |

The subscription sends a `subscription-userinfo` header so apps show usage and expiry.

**Recommended apps (the panel shows the right ones for the visitor's device):**
| Device | Apps |
|---|---|
| Android | v2rayNG, Hiddify, NekoBox, sing-box |
| iPhone / iPad | Streisand, V2Box, Shadowrocket, sing-box |
| Windows | v2rayN, Hiddify, Clash Verge Rev |
| macOS | Hiddify, V2Box, Clash Verge Rev |
| Linux | Hiddify, NekoRay, v2rayA |

“Add to app” uses the app's deep link; if it doesn't open, copy the subscription link and paste it in the app. Store links may change — search the app name if needed.

## 9) Settings
- **Worker domain:** host used to build links.
- **Clean IP list:** one IP/domain per line; the subscription contains a link for each.
- **Proxy IP:** if a destination behind Cloudflare doesn't respond, the Worker retries through this address (`ip`, `ip:port` or domain). Optional.
- **External server address:** default for vmess/ss/hysteria2/tuic.
- **Auto-name prefix:** e.g. `Parham` → `Parham_a1b2`.
- **Kill switch:** stops everything (open connections drop within ~30 s).
- **Change password**, **Backup** (download/restore JSON).

## 10) Telegram bot
1. Create a bot with [@BotFather](https://t.me/BotFather) and copy the token.
2. Panel → Telegram bot (or the dashboard card) → token → **Confirm**.
3. In Telegram use `/login` according to the project's configuration.
4. Commands: `/new` create VLESS, `/list`, `/stats`.

## 11) Update & backup
1. **Settings → Download backup**.
2. Worker → **Edit code** → replace with the new code → **Deploy**.
3. Data stays in D1/KV.
4. If something breaks: Settings → Restore backup.

## 12) Troubleshooting
| Problem | Cause / fix |
|---|---|
| “Database connection required” | Binding named exactly `DB` is missing (step 4) |
| Error while creating a config | The message now shows the real cause; usually the `DB` binding. This version's tables use the `p01_` prefix so they don't clash with older versions |
| `429 ip limit reached` | Concurrent-IP cap is full; raise it or wait 90 s |
| `403 quota exceeded / expired` | Data or time is over; edit or reset usage |
| `503 service paused` | Kill switch is on |
| Connects but some sites fail | Those sites sit behind Cloudflare; set **Proxy IP** |
| Cannot connect | Check Worker domain in Settings, TLS on, correct port, WebSockets on |
| No QR shown | The QR library loads from cdnjs; check your connection. Links/subscription are still copyable |
| Error 1101 | Usually incomplete bindings; redeploy |

## 13) Cloudflare limits
- Free Workers: about **100k requests/day** (each WebSocket = 1 request).
- Free D1: about 100k row-writes/day. Each active connection writes a few rows every 30 s; for many users raise `flushEvery` at the top of the file (cut-off precision drops).
- Free KV: 1000 writes/day (admin logins only).
- TCP only; no UDP (e.g. DNS over VLESS UDP).
- Counted usage is the bytes passing through the Worker; it may differ a few % from the client's numbers.

## 14) FAQ
**Is one file enough?** Yes — `worker.js`.

**Can a normal visitor see the admin?** No. `/` is the user portal and unknown paths return 404.

**Can vmess run on the Worker itself?** No; this version only builds its link.

**⚠️ Disclaimer:** Use this project in line with your local laws and Cloudflare's terms. You are responsible for how you use it.
