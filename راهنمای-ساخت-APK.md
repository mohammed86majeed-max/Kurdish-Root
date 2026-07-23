# راهنمای تبدیل این پروژه به APK اندروید

این پوشه شامل یک اپلیکیشن وب کامل (پوشه‌ی `www/`) است که با ابزار متن‌باز **Capacitor**
می‌توانید آن را به یک اپلیکیشن اندروید واقعی (APK) تبدیل کنید. این کار باید روی
کامپیوتر خودتان انجام شود، چون به Android Studio و اینترنت نیاز دارد.

## پیش‌نیازها (یک‌بار نصب می‌کنید)
1. **Node.js** (نسخه ۱۸ به بالا) — از nodejs.org
2. **Android Studio** — از developer.android.com/studio
   (هنگام نصب، Android SDK هم همراهش نصب می‌شود)

## مراحل

### ۱. باز کردن ترمینال در همین پوشه
همین پوشه (`kurdish-app`) که `package.json`, `capacitor.config.json` و `www/` در آن است.

### ۲. نصب پکیج‌ها
```bash
npm install
```

### ۳. افزودن پلتفرم اندروید
```bash
npx cap add android
```
این دستور یک پوشه‌ی `android/` می‌سازد که پروژه‌ی کامل اندروید استودیویی است.

### ۴. همگام‌سازی فایل‌های وب با پروژه‌ی اندروید
```bash
npx cap sync android
```
هر بار که محتوای `www/index.html` را عوض کردید، همین دستور را دوباره اجرا کنید.

### ۵. باز کردن در Android Studio
```bash
npx cap open android
```
Android Studio باز می‌شود و پروژه را لود می‌کند (بار اول کمی طول می‌کشد چون Gradle
دانلود می‌شود).

### ۶. گرفتن APK
داخل Android Studio:
- از منو: **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- بعد از تمام شدن، پیغامی می‌آید با لینک «locate» — فایل APK آنجاست
  (معمولاً در مسیر `android/app/build/outputs/apk/debug/app-debug.apk`)

این APK را می‌توانید مستقیم روی گوشی اندروید خودتان نصب کنید (نیاز به فعال‌کردن
«نصب از منابع ناشناس» دارید)، یا برای انتشار در Google Play باید نسخه‌ی
امضاشده (signed / release) بسازید که راهنمایش در همان بخش Build داخل
Android Studio هست («Generate Signed Bundle / APK»).

## نکته درباره‌ی آیکون و نام اپ
- نام و شناسه‌ی اپ در `capacitor.config.json` تنظیم شده (`appId`, `appName`) —
  قبل از مرحله‌ی ۳ می‌توانید این‌ها را به دلخواه عوض کنید.
- آیکون‌های ساده در `www/icons/` گذاشته شده‌اند؛ اگر خواستید آیکون حرفه‌ای‌تر
  بسازید، بهتر است از ابزار Capacitor Assets استفاده کنید:
  ```bash
  npm install @capacitor/assets --save-dev
  npx capacitor-assets generate
  ```

## اگر فقط می‌خواهید سریع روی گوشی امتحان کنید (بدون APK)
فایل `www/index.html` را در گوشی با مرورگر Chrome باز کنید (یا آن را روی یک
هاست ساده مثل GitHub Pages بگذارید)، سپس از منوی Chrome گزینه‌ی
«Add to Home screen» را بزنید — دقیقاً مثل یک اپ روی صفحه‌ی اصلی نصب می‌شود.
