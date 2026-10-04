<div align="center">

<a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/banner/banner.jpg">
<img src="https://raw.githubusercontent.com/parham-01/free-vpn-cludflare/main/banner/banner.jpg" alt="Parham 01 Banner" width="100%">
</a>

<br><br>

# ⚡ PARHAM 01 · CLOUDFLARE WORKER

### Modern Panel • Simple Setup • Cloudflare API

<br>

<a href="#persian"><img src="https://img.shields.io/badge/🇮🇷%20Persian-OPEN-ff2d3d?style=for-the-badge&labelColor=090909"></a>
<a href="#english"><img src="https://img.shields.io/badge/🇬🇧%20English-OPEN-2f81f7?style=for-the-badge&labelColor=090909"></a>

<br><br>

<a href="https://t.me/parham_ste01"><img src="https://img.shields.io/badge/Telegram%20Channel-OPEN-ff2d3d?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>
<a href="https://t.me/+SchgZ4s1dGU4N2Y0"><img src="https://img.shields.io/badge/Support%20Group-OPEN-2f81f7?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>

</div>

---

<a id="persian"></a>

# 🇮🇷 Persian

<a href="#english">🇬🇧 English</a>

## ✦ Guide

| # | Guide |
|---:|---|
| 01 | <a href="#fa-01">Create a Cloudflare Worker</a> |
| 02 | <a href="#fa-02">Deploy the Worker</a> |
| 03 | <a href="#fa-03">First Registration</a> |
| 04 | <a href="#fa-04">Open the Panel</a> |
| 05 | <a href="#fa-05">Cloudflare API</a> |
| 06 | <a href="#fa-06">Main Panel Features</a> |
| 07 | <a href="#fa-07">Common Fixes</a> |
| 08 | <a href="#fa-08">Support</a> |

---

<a id="fa-01"></a>

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

برو داخل **Edit code**.

کد پیش‌فرض را پاک کن.

فایل <a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><b>worker.js</b></a> را باز کن، کل کد را Copy کن و داخل **Edit code** قرار بده.

<a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><img src="https://img.shields.io/badge/View%20worker.js-2f81f7?style=for-the-badge&labelColor=090909"></a>

### مرحله ۵

بزن:

```text
Save and Deploy
```

<a id="fa-02"></a>

# ⚡ 02 — Deploy و ورود به پنل

بعد از اینکه Worker ساخته و Deploy شد، آدرس Worker را باز کن و **آخر آدرس `/panel/` را بنویس.**

```text
https://YOUR-WORKER.workers.dev/panel/
```

> **مهم:** بعد از ساخت Worker مستقیماً وارد `/panel/` شو.

<a id="fa-03"></a>

# 👤 03 — اولین ورود و ثبت‌نام

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

ثبت‌نام انجام می‌شود و بعد از آن رمز پنل را تعیین می‌کنی.

<a id="fa-04"></a>

# 🔐 04 — ورود به پنل

بعد از تعیین رمز، با همان رمز وارد پنل می‌شوی.

آدرس:

```text
https://YOUR-WORKER.workers.dev/panel/
```

<a id="fa-05"></a>

# ☁️ 05 — Cloudflare API

بعد از ورود به پنل برو به:

```text
Panel → API
```

راهنمای ساخت و اتصال **Cloudflare API** داخل همین بخش قرار دارد.

از قسمت API می‌توانی تنظیمات و منابع موردنیاز مثل **D1 و KV** را انجام بدهی.

> 🔐 **API Token خودت را برای شخص دیگری ارسال نکن.**

<a id="fa-06"></a>

# ⚙️ 06 — قابلیت‌های اصلی پنل

- ◉ Dashboard و وضعیت سیستم
- ◉ ساخت و مدیریت Configuration
- ◉ مدیریت کاربران
- ◉ مدیریت Bot
- ◉ Cloudflare API
- ◉ مدیریت Worker و Update
- ◉ اعلان‌ها
- ◉ تنظیمات پنل
- ◉ وضعیت مصرف و منابع
- ◉ Subscription و QR کانفیگ‌ها

<a id="fa-07"></a>

# 🛠️ 07 — اگر چیزی کار نکرد

```text
1. worker.js کامل قرار گرفته باشد
2. Save and Deploy زده باشی
3. بعد از ساخت Worker آدرس /panel/ را باز کرده باشی
4. داخل پنل به بخش API رفته باشی
5. مراحل API را کامل کرده باشی
```

<a id="fa-08"></a>

# ❤️ 08 — حمایت از پروژه

<div align="center">

## اگر پروژه برات مفید بود، حمایت فراموش نشه ❤️

<a href="https://t.me/parham_ste01"><img src="https://img.shields.io/badge/Telegram%20Channel-OPEN-ff2d3d?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>

<br><br>

<a href="https://t.me/+SchgZ4s1dGU4N2Y0"><img src="https://img.shields.io/badge/Support%20Group-OPEN-2f81f7?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>

</div>

---

<a id="english"></a>

# 🇬🇧 English

<a href="#persian">🇮🇷 Persian</a>

## ✦ Guide

| # | Guide |
|---:|---|
| 01 | <a href="#en-01">Create a Cloudflare Worker</a> |
| 02 | <a href="#en-02">Deploy the Worker</a> |
| 03 | <a href="#en-03">First Registration</a> |
| 04 | <a href="#en-04">Open the Panel</a> |
| 05 | <a href="#en-05">Cloudflare API</a> |
| 06 | <a href="#en-06">Main Panel Features</a> |
| 07 | <a href="#en-07">Common Fixes</a> |
| 08 | <a href="#en-08">Support</a> |

---

<a id="en-01"></a>

# 🚀 01 — Create a Cloudflare Worker

### Step 1

Open **Cloudflare Dashboard**.

### Step 2

Go to:

```text
Workers & Pages
```

Then click:

```text
Create → Worker
```

### Step 3

Choose a Worker name.

Example:

```text
parham-panel
```

### Step 4

Open **Edit code**.

Delete the default code.

Open <a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><b>worker.js</b></a>, copy the complete code and paste it into **Edit code**.

<a href="https://github.com/parham-01/free-vpn-cludflare/blob/main/worker.js"><img src="https://img.shields.io/badge/View%20worker.js-2f81f7?style=for-the-badge&labelColor=090909"></a>

### Step 5

Click:

```text
Save and Deploy
```

<a id="en-02"></a>

# ⚡ 02 — Deploy and Open the Panel

After the Worker is created and deployed, open the Worker URL and **add `/panel/` at the end.**

```text
https://YOUR-WORKER.workers.dev/panel/
```

> **Important:** After creating the Worker, go directly to `/panel/`.

<a id="en-03"></a>

# 👤 03 — First Registration

```text
/panel/
   ↓
Registration
   ↓
Automatic registration
   ↓
Set password
   ↓
Login to the panel
```

Registration is completed automatically. After that, set your panel password.

<a id="en-04"></a>

# 🔐 04 — Open the Panel

After setting your password, use it to log in.

```text
https://YOUR-WORKER.workers.dev/panel/
```

<a id="en-05"></a>

# ☁️ 05 — Cloudflare API

After logging in, go to:

```text
Panel → API
```

The **Cloudflare API** setup guide is available inside this section.

Use the API section to configure required resources such as **D1 and KV**.

> 🔐 **Never share your API Token with anyone.**

<a id="en-06"></a>

# ⚙️ 06 — Main Panel Features

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

<a id="en-07"></a>

# 🛠️ 07 — Common Fixes

```text
1. Make sure the complete worker.js was pasted
2. Click Save and Deploy
3. Open /panel/ after creating the Worker
4. Open the API section inside the panel
5. Complete the API setup
```

<a id="en-08"></a>

# ❤️ 08 — Support

<div align="center">

## If this project helped you, please support it ❤️

<a href="https://t.me/parham_ste01"><img src="https://img.shields.io/badge/Telegram%20Channel-OPEN-ff2d3d?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>

<br><br>

<a href="https://t.me/+SchgZ4s1dGU4N2Y0"><img src="https://img.shields.io/badge/Support%20Group-OPEN-2f81f7?style=for-the-badge&logo=telegram&logoColor=white&labelColor=090909"></a>

</div>

---

<div align="center">

### ⚡ PARHAM 01

`Cloudflare Worker • API • Panel`

❤️ Thank you for supporting the project.

</div>
