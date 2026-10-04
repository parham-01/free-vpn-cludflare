<div align="center">

<a href="https://github.com/parham-01/free-vpn-cludflare/tree/main/banner">
<img src="https://raw.githubusercontent.com/parham-01/free-vpn-cludflare/main/banner/banner.jpg" alt="Parham 01 Banner" width="100%">
</a>

<br><br>

# ⚡ PARHAM 01 · CLOUDFLARE WORKER

### پنل مدیریت مدرن • راه‌اندازی ساده • اتصال Cloudflare API

<a href="https://t.me/parham_ste01"><img src="https://img.shields.io/badge/Telegram-کانال%20اصلی-ff2d3d?style=for-the-badge&logo=telegram&logoColor=white"></a>
<a href="https://t.me/+SchgZ4s1dGU4N2Y0"><img src="https://img.shields.io/badge/Telegram-گروه%20پشتیبانی-111111?style=for-the-badge&logo=telegram&logoColor=white"></a>

</div>

---

## 🌓 فارسی | English

<details open>
<summary><b>🇮🇷 فارسی — آموزش خیلی ساده</b></summary>

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
| 10 | لینک `/banner/` |
| 11 | رفع خطاهای رایج |
| 12 | حمایت از پروژه ❤️ |

---

# 🚀 01 — ساخت Worker

### قدم ۱

وارد Cloudflare شو:

**Dashboard → Workers & Pages**

### قدم ۲

روی:

**Create → Worker**

بزن.

### قدم ۳

یک اسم برای Worker انتخاب کن.

مثلاً:

```text
parham-panel
```

بعد Worker را بساز و وارد **Edit code** شو.

### قدم ۴

کد پیش‌فرض Cloudflare را پاک کن.

فایل زیر را باز کن:

```text
worker.js
```

کل کد آن را Copy کن و داخل **Edit code** قرار بده.

### قدم ۵

روی:

```text
Save and Deploy
```

بزن.

تمام.

---

> ### 💡 نکته مهم — بعد از ساخت Worker
>
> حالا وارد Worker شو و **پنل را باز کن**:
>
> ```text
> https://YOUR-WORKER.workers.dev/panel/
> ```
>
> بعد از ورود به پنل، برو به:
>
> **API**
>
> و آموزش همان بخش را انجام بده.
>
> ساخت و اتصال **Cloudflare API، D1 و KV** از مسیر API پنل انجام می‌شود؛ لازم نیست قبل از آن جداگانه D1 و KV بسازی.

---

# 👤 02 — اولین ورود

خیلی ساده:

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

ثبت‌نام که کامل شد، رمز پنل را تعیین می‌کنی و وارد پنل می‌شوی.

---

# ⚙️ 03 — قابلیت‌های اصلی پنل

پنل برای مدیریت یک‌جا ساخته شده و بخش‌های اصلی آن شامل این موارد است:

- ◉ داشبورد و وضعیت سیستم
- ◉ ساخت و مدیریت Configuration
- ◉ مدیریت کاربران
- ◉ مدیریت Bot
- ◉ Cloudflare API
- ◉ مدیریت Worker و Update
- ◉ اعلان‌ها
- ◉ تنظیمات پنل
- ◉ مشاهده وضعیت مصرف و منابع
- ◉ لینک Subscription و QR برای کانفیگ‌ها

---

# ☁️ 04 — Cloudflare API

بعد از ساخت Worker و ورود به پنل:

```text
Panel
  ↓
API
```

وارد بخش **API** شو.

راهنمای داخل خود پنل مرحله‌به‌مرحله مسیر ساخت Token و اتصال Cloudflare را نشان می‌دهد.

پس ترتیب کار این است:

```text
ساخت Worker
      ↓
Deploy
      ↓
/panel/
      ↓
ثبت‌نام خودکار
      ↓
تعیین رمز
      ↓
ورود
      ↓
API
      ↓
ساخت / اتصال D1 و KV
```

> 🔐 **API Token را در اختیار شخص دیگری قرار نده.**

---

# 🖼️ 05 — Banner

بنر پروژه در GitHub قرار دارد:

**`/banner/banner.jpg`**

و Worker هم مسیر زیر را برای نمایش همان فایل دارد:

```text
/banner/
```

یا مستقیم:

```text
/banner/banner.jpg
```

منبع GitHub:

<a href="https://github.com/parham-01/free-vpn-cludflare/tree/main/banner">📁 مشاهده پوشه Banner در GitHub</a>

---

# 🛠️ 06 — اگر چیزی کار نکرد

اول این‌ها را بررسی کن:

```text
1. worker.js کامل آپلود شده باشد
2. Save and Deploy زده باشی
3. آدرس /panel/ را باز کرده باشی
4. از داخل پنل وارد API شده باشی
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
<img src="https://img.shields.io/badge/💬%20ورود%20به%20گروه-ff2d3d?style=for-the-badge&labelColor=090909">
</a>

<br><br>

<sub>با حمایت شما توسعه و آپدیت پروژه ادامه پیدا می‌کند.</sub>

</div>

</details>

<details>
<summary><b>🇬🇧 English — Simple Guide</b></summary>

# 🚀 Create the Worker

1. Open **Cloudflare Dashboard**.
2. Go to **Workers & Pages**.
3. Select **Create → Worker**.
4. Choose a Worker name, for example:

```text
parham-panel
```

5. Open **Edit code**.
6. Remove the default code.
7. Copy all content from `worker.js`.
8. Paste it into the Worker editor.
9. Click **Save and Deploy**.

### Important

After creating and deploying the Worker, open:

```text
https://YOUR-WORKER.workers.dev/panel/
```

Then complete registration and login.

After login, open:

```text
Panel → API
```

Use the instructions inside the API section to create/connect the Cloudflare API and set up the required D1/KV resources.

## First Login

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

## Main Features

- Dashboard
- Configuration management
- User management
- Bot management
- Cloudflare API
- Worker updates
- Notifications
- Settings
- Usage and resource status
- Subscription links and QR codes

## Banner

The project banner is stored at:

```text
/banner/banner.jpg
```

The Worker also exposes it at:

```text
/banner/
```

GitHub folder:

<a href="https://github.com/parham-01/free-vpn-cludflare/tree/main/banner">Open Banner Folder</a>

## Support

<a href="https://t.me/parham_ste01">Telegram Channel</a>

<br>

<a href="https://t.me/+SchgZ4s1dGU4N2Y0">Support Group</a>

</details>

---

<div align="center">

### ⚡ PARHAM 01

`Cloudflare Worker • API • Panel`

❤️ حمایت فراموش نشه

</div>
