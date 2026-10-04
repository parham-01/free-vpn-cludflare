<div align="center">

<a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/banner/banner.jpg">
<img src="https://raw.githubusercontent.com/parham-01/free-vpn-cludflare/main/banner/banner.jpg" alt="Parham 01 Banner" width="100%">
</a>

<br><br>

# ⚡ PARHAM 01 · CLOUDFLARE WORKER

### پنل مدیریت مدرن • راه‌اندازی ساده • Cloudflare API

<a href="#-فارسی"><img src="https://img.shields.io/badge/🇮🇷%20فارسی-ورود-ff2d3d?style=for-the-badge&labelColor=090909"></a>
<a href="#-english"><img src="https://img.shields.io/badge/🇬🇧%20English-Open-2f81f7?style=for-the-badge&labelColor=090909"></a>

<br><br>

<a href="https://t.me/parham_ste01"><img src="https://img.shields.io/badge/Telegram-کانال%20اصلی-ff2d3d?style=for-the-badge&logo=telegram&logoColor=white"></a>
<a href="https://t.me/+SchgZ4s1dGU4N2Y0"><img src="https://img.shields.io/badge/Telegram-گروه%20پشتیبانی-111111?style=for-the-badge&logo=telegram&logoColor=white"></a>

</div>

---

<a id="-فارسی"></a>

# 🇮🇷 فارسی

<a href="#-english">🇬🇧 رفتن به بخش English</a>

## ✦ فهرست آموزش‌ها

| # | آموزش |
|---:|---|
| 01 | ساخت حساب Cloudflare |
| 02 | ساخت Worker |
| 03 | قرار دادن `worker.js` |
| 04 | Deploy کردن Worker |
| 05 | اولین ورود و ثبت‌نام |
| 06 | ورود به پنل |
| 07 | اتصال Cloudflare API |
| 08 | ساخت خودکار D1 و KV از بخش API |
| 09 | قابلیت‌های اصلی پنل |
| 10 | رفع خطاهای رایج |
| 11 | حمایت از پروژه ❤️ |

---

# 🚀 01 — ساخت Worker

### مرحله ۱

وارد **Cloudflare Dashboard** شو.

### مرحله ۲

برو به:

```text
Workers & Pages
```

بعد بزن:

```text
Create → Worker
```

### مرحله ۳

یک اسم برای Worker انتخاب کن.

مثلاً:

```text
parham-panel
```

### مرحله ۴

وارد **Edit code** شو.

کد پیش‌فرض را پاک کن.

حالا فایل <a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><b>worker.js</b></a> را باز کن، کل کد را Copy کن و داخل **Edit code** قرار بده.

### مرحله ۵

بزن:

```text
Save and Deploy
```

---

# ⚠️ بعد از ساخت Worker

بعد از اینکه Worker ساخته و Deploy شد، **حتماً در آخر آدرس Worker این را بنویس:**

```text
/panel/
```

مثلاً:

```text
https://YOUR-WORKER.workers.dev/panel/
```

---

# 👤 02 — اولین ورود

```text
/panel/
   ↓
ثبت‌نام
   ↓
ثبت‌نام به صورت خودکار انجام می‌شود
   ↓
تعیین رمز
   ↓
ورود به پنل
```

---

# ☁️ 03 — Cloudflare API

بعد از ساخت Worker و ورود به پنل برو به:

```text
Panel → API
```

راهنمای ساخت و اتصال **Cloudflare API** داخل همین بخش قرار دارد.

از همین قسمت برای راه‌اندازی منابع موردنیاز مثل **D1 و KV** استفاده کن.

> 🔐 **API Token خودت را برای شخص دیگری ارسال نکن.**

---

# ⚙️ 04 — قابلیت‌های اصلی پنل

- ◉ Dashboard و وضعیت سیستم
- ◉ ساخت و مدیریت Configuration
- ◉ مدیریت کاربران
- ◉ مدیریت Bot
- ◉ Cloudflare API
- ◉ مدیریت Worker و Update
- ◉ اعلان‌ها
- ◉ تنظیمات پنل
- ◉ مشاهده وضعیت مصرف و منابع
- ◉ Subscription و QR کانفیگ‌ها

---

# 🛠️ 05 — اگر چیزی کار نکرد

این موارد را بررسی کن:

```text
1. worker.js کامل قرار گرفته باشد
2. Save and Deploy زده باشی
3. بعد از ساخت Worker آدرس /panel/ را باز کرده باشی
4. داخل پنل به بخش API رفته باشی
5. مراحل API را کامل کرده باشی
```

---

# ❤️ حمایت از پروژه

<div align="center">

## اگر پروژه برات مفید بود، حمایت فراموش نشه ❤️

### 🔥 کانال تلگرام

<a href="https://t.me/parham_ste01">
<img src="https://img.shields.io/badge/🚀%20ورود%20به%20کانال-ff2d3d?style=for-the-badge&labelColor=090909">
</a>

<br><br>

### 💬 گروه پشتیبانی

<a href="https://t.me/+SchgZ4s1dGU4N2Y0">
<img src="https://img.shields.io/badge/💬%20ورود%20به%20گروه-2f81f7?style=for-the-badge&labelColor=090909">
</a>

</div>

---

<a id="-english"></a>

# 🇬🇧 English

<a href="#-فارسی">🇮🇷 Go to Persian</a>

## ✦ Guide

| # | Guide |
|---:|---|
| 01 | Create a Cloudflare account |
| 02 | Create a Worker |
| 03 | Add `worker.js` |
| 04 | Deploy the Worker |
| 05 | First registration |
| 06 | Open the panel |
| 07 | Connect Cloudflare API |
| 08 | Create D1 and KV from the API section |
| 09 | Main panel features |
| 10 | Common fixes |
| 11 | Support the project ❤️ |

---

# 🚀 01 — Create the Worker

### Step 1

Open **Cloudflare Dashboard**.

### Step 2

Go to:

```text
Workers & Pages
```

Then:

```text
Create → Worker
```

### Step 3

Choose a Worker name, for example:

```text
parham-panel
```

### Step 4

Open **Edit code** and remove the default code.

Open <a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><b>worker.js</b></a>, copy all of its code and paste it into the Worker editor.

### Step 5

Click:

```text
Save and Deploy
```

---

# ⚠️ After creating the Worker

After the Worker is created and deployed, **add `/panel/` to the Worker URL:**

```text
https://YOUR-WORKER.workers.dev/panel/
```

---

# 👤 02 — First Login

```text
/panel/
   ↓
Registration
   ↓
Automatic registration
   ↓
Set password
   ↓
Login
   ↓
Panel
```

---

# ☁️ 03 — Cloudflare API

After creating the Worker and opening the panel, go to:

```text
Panel → API
```

The API section contains the instructions for creating and connecting the **Cloudflare API**.

Use this section to set up required resources such as **D1 and KV**.

> 🔐 **Never share your API Token with anyone.**

---

# ⚙️ 04 — Main Panel Features

- ◉ Dashboard and system status
- ◉ Configuration management
- ◉ User management
- ◉ Bot management
- ◉ Cloudflare API
- ◉ Worker management and updates
- ◉ Notifications
- ◉ Panel settings
- ◉ Usage and resource status
- ◉ Subscription and configuration QR codes

---

# 🛠️ 05 — Common Fixes

Check these first:

```text
1. worker.js was pasted completely
2. Save and Deploy was completed
3. /panel/ was added after creating the Worker
4. The API section was opened
5. The API setup was completed
```

---

# ❤️ Support the Project

<div align="center">

## If this project helped you, please support it ❤️

<a href="https://t.me/parham_ste01">
<img src="https://img.shields.io/badge/🚀%20Telegram%20Channel-ff2d3d?style=for-the-badge&labelColor=090909">
</a>

<br><br>

<a href="https://t.me/+SchgZ4s1dGU4N2Y0">
<img src="https://img.shields.io/badge/💬%20Support%20Group-2f81f7?style=for-the-badge&labelColor=090909">
</a>

</div>

---

<div align="center">

### ⚡ PARHAM 01

`Cloudflare Worker • API • Panel`

❤️ حمایت فراموش نشه

</div>
