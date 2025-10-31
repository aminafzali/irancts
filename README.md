# قالب HTML سایت IRAN CTS

این یک قالب HTML/CSS/JavaScript کامل و آماده برای استفاده در وردپرس است.

## 📁 فایل‌های موجود

- `index.html` - قالب کامل HTML با تمام بخش‌ها
- `logo.png` - لوگوی سایت
- `gomrok1.jpg` - تصویر پس‌زمینه اسلاید 1
- `Gemini_Generated_Image_12044l12044l1204.png` - تصویر پس‌زمینه اسلاید 2
- `iranyekan/` - پوشه فونت ایران یکان

## 🎨 ویژگی‌های قالب

✅ طراحی مدرن و مینیمال
✅ کاملاً ریسپانسیو (موبایل و دسکتاپ)
✅ انیمیشن‌های SVG تعاملی
✅ اسلایدر تصاویر در Hero Section
✅ سکشن نرخ لحظه‌ای ارز
✅ بخش مقالات با تصاویر
✅ فوتر کامل با لینک‌های مفید
✅ فونت فارسی ایران یکان
✅ رنگ‌بندی: آبی سرمه‌ای (#1e3a8a) و نارنجی (#f4a261)

## 🚀 راه‌اندازی و Build

این پروژه از **Tailwind CSS لوکال** استفاده می‌کند (بدون نیاز به CDN).

### نصب وابستگی‌ها
```bash
npm install
```

### تولید فایل CSS (در صورت تغییر HTML)
اگر در HTML تغییراتی ایجاد کردید و کلاس‌های Tailwind جدیدی اضافه کردید:
```bash
npm run build:css
```

این دستور فایل `assets/css/tailwind.css` را بازسازی می‌کند.

### فایل‌های لازم برای تحویل به وردپرس
```
├── assets/
│   ├── css/
│   │   └── tailwind.css          ← فایل CSS تولید شده (حتماً شامل شود)
│   ├── icons/                     ← آیکون‌های SVG
├── iranyekan/                     ← فونت‌های فارسی
├── index.html                     ← فایل HTML اصلی
└── [تصاویر]
```

⚠️ **مهم**: پوشه‌های `node_modules` و `src` نباید به وردپرس‌کار تحویل داده شوند.

## 🔧 نحوه استفاده در وردپرس

### روش 1: استفاده مستقیم از HTML
1. محتوای فایل `index.html` را باز کنید
2. بخش‌های مورد نظر (Header, Footer, یا Content) را کپی کنید
3. در قالب وردپرس خود در فایل‌های مربوطه قرار دهید

### روش 2: تبدیل به Page Template
1. یک فایل جدید با نام `template-irancts.php` در پوشه قالب وردپرس بسازید
2. در ابتدای فایل این کد را قرار دهید:
```php
<?php
/*
Template Name: IRAN CTS Homepage
*/
?>
```
3. محتوای `index.html` را در ادامه قرار دهید

### روش 3: استفاده از Shortcode
می‌توانید هر بخش را به صورت Shortcode در `functions.php` قالب وردپرس تعریف کنید.

---

## 🎬 راهنمای اضافه کردن انیمیشن منوی موبایل در وردپرس

این قالب دارای **انیمیشن‌های کشویی** برای منوی موبایل است که خیلی ساده در وردپرس قابل استفاده هستند.

### 📝 مرحله 1: اضافه کردن CSS انیمیشن‌ها

فایل `functions.php` قالب وردپرس خود را باز کنید و این کد را اضافه کنید:

```php
function irancts_mobile_menu_styles() {
    $custom_css = "
        /* Mobile Menu Animations */
        #mobile-nav {
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1),
                        opacity 0.3s ease,
                        padding 0.4s ease;
        }
        
        #mobile-nav.menu-open {
            max-height: 600px;
            opacity: 1;
            padding-bottom: 0.75rem;
        }
        
        /* Submenu Animations */
        .submenu {
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            transition: max-height 0.3s cubic-bezier(0.4, 0, 0.2, 1),
                        opacity 0.25s ease,
                        margin-top 0.3s ease;
        }
        
        .submenu.open {
            max-height: 300px;
            opacity: 1;
            margin-top: 0.5rem;
        }
        
        /* Chevron rotation animation */
        .submenu-chevron {
            transition: transform 0.3s ease;
        }
        
        .submenu-chevron.rotate {
            transform: rotate(180deg);
        }
    ";
    wp_add_inline_style('your-theme-style', $custom_css);
}
add_action('wp_enqueue_scripts', 'irancts_mobile_menu_styles');
```

⚠️ **توجه**: `'your-theme-style'` را با نام handle استایل اصلی قالب خود جایگزین کنید.

### 📝 مرحله 2: اضافه کردن JavaScript انیمیشن‌ها

در همان فایل `functions.php` این کد را نیز اضافه کنید:

```php
function irancts_mobile_menu_script() {
    ?>
    <script>
    document.addEventListener('DOMContentLoaded', function() {
        // Mobile menu toggle با انیمیشن slide
        const mobileMenuBtn = document.getElementById('mobile-menu-btn');
        const mobileNav = document.getElementById('mobile-nav');
        
        if (mobileMenuBtn && mobileNav) {
            mobileMenuBtn.addEventListener('click', function() {
                const isOpen = mobileNav.classList.contains('menu-open');
                
                if (isOpen) {
                    // بستن منو
                    mobileNav.classList.remove('menu-open');
                    setTimeout(() => {
                        const allSubmenus = mobileNav.querySelectorAll('.submenu');
                        allSubmenus.forEach(sub => sub.classList.remove('open'));
                        const allChevrons = mobileNav.querySelectorAll('.submenu-chevron');
                        allChevrons.forEach(ch => ch.classList.remove('rotate'));
                    }, 300);
                } else {
                    // باز کردن منو
                    mobileNav.classList.add('menu-open');
                }
                
                // تغییر آیکن
                const icon = mobileMenuBtn.querySelector('img');
                if (icon) {
                    if (isOpen) {
                        icon.src = icon.src.replace('xmark-solid-full.svg', 'bars-solid-full.svg');
                        icon.alt = 'Menu';
                    } else {
                        icon.src = icon.src.replace('bars-solid-full.svg', 'xmark-solid-full.svg');
                        icon.alt = 'Close';
                    }
                }
            });

            // انیمیشن زیرمنوها
            const submenuParents = mobileNav.querySelectorAll('.has-submenu');
            submenuParents.forEach(parent => {
                const btn = parent.querySelector('button');
                const sub = parent.querySelector('.submenu');
                const chevron = parent.querySelector('.submenu-chevron');
                
                if (btn && sub) {
                    btn.addEventListener('click', () => {
                        const isOpen = sub.classList.contains('open');
                        
                        // بستن سایر زیرمنوها
                        submenuParents.forEach(p => {
                            if (p !== parent) {
                                const submenuEl = p.querySelector('.submenu');
                                const ch = p.querySelector('.submenu-chevron');
                                if (submenuEl) submenuEl.classList.remove('open');
                                if (ch) ch.classList.remove('rotate');
                            }
                        });
                        
                        // باز/بسته کردن زیرمنوی فعلی
                        if (isOpen) {
                            sub.classList.remove('open');
                            if (chevron) chevron.classList.remove('rotate');
                        } else {
                            sub.classList.add('open');
                            if (chevron) chevron.classList.add('rotate');
                        }
                    });
                }
            });
        }
    });
    </script>
    <?php
}
add_action('wp_footer', 'irancts_mobile_menu_script');
```

### ✅ تمام! همین!

حالا انیمیشن‌های منوی موبایل شما در وردپرس کار می‌کنند:
- منو از بالا به پایین باز می‌شود ✨
- زیرمنوها با انیمیشن کشویی باز می‌شوند 🎯
- آیکون chevron می‌چرخد ↓ ↑

### 🔍 نکات مهم:

1. **ID های مهم**: مطمئن شوید در HTML خود این ID ها موجود باشند:
   - `mobile-menu-btn` - دکمه باز/بسته کردن منو
   - `mobile-nav` - منوی موبایل
   - کلاس `has-submenu` - برای آیتم‌های منو که زیرمنو دارند
   - کلاس `submenu` - برای خود زیرمنوها
   - کلاس `submenu-chevron` - برای آیکون chevron

2. **سازگاری با jQuery**: اگر قالب شما از jQuery استفاده می‌کند، نگران نباشید! این کدها با jQuery تداخل ندارند.

3. **تست در موبایل**: حتماً سایت را در موبایل یا حالت Responsive مرورگر تست کنید.

### 🎨 سفارشی‌سازی:

اگر می‌خواهید سرعت انیمیشن را تغییر دهید:
- `max-height 0.4s` → عدد `0.4` را تغییر دهید (مثلاً `0.6` برای آهسته‌تر)
- `opacity 0.3s` → عدد `0.3` را تغییر دهید

### ❓ اگر کار نکرد:

1. Cache سایت را پاک کنید
2. Console مرورگر را چک کنید (F12)
3. مطمئن شوید ID ها در HTML درست هستند
4. اگر قالب شما از jQuery استفاده می‌کند، ممکن است نیاز باشد کد را در `jQuery(document).ready()` بگذارید

## 📂 آپلود تصاویر و فونت‌ها

1. پوشه `iranyekan` را در مسیر `/wp-content/themes/your-theme/fonts/` آپلود کنید
2. تصاویر را در مسیر `/wp-content/uploads/` آپلود کنید
3. مسیرهای فایل‌ها در HTML را به‌روزرسانی کنید:
   - `iranyekan/IRANYekanWebRegular.woff2` → `/wp-content/themes/your-theme/fonts/iranyekan/...`
   - `logo.png` → `/wp-content/uploads/2024/logo.png`
   - `gomrok1.jpg` → `/wp-content/uploads/2024/gomrok1.jpg`

## 🎯 بخش‌های قالب

1. **Header** - هدر چسبان با منوی navigation
2. **Hero Slider** - اسلایدر 2 تصویری با متن و دکمه‌ها
3. **Services** - 6 کارت خدمات با آیکون
4. **SVG Animations** - 3 انیمیشن SVG تعاملی
5. **Articles** - 6 مقاله با تصویر
6. **Exchange Rates** - جدول نرخ لحظه‌ای ارز
7. **Footer** - فوتر 3 ستونه با لینک‌ها

## 🌐 فونت

قالب از فونت **ایران یکان** استفاده می‌کند که در پوشه `iranyekan` موجود است.

## 📱 ریسپانسیو

قالب کاملاً ریسپانسیو است و در تمام سایزهای صفحه به خوبی نمایش داده می‌شود:
- موبایل (375px+)
- تبلت (768px+)
- دسکتاپ (1024px+)

## 🎨 رنگ‌بندی

- **Primary (آبی سرمه‌ای)**: #1e3a8a
- **Secondary (سفید)**: #ffffff
- **Accent (نارنجی)**: #f4a261
- **متن اصلی**: #1e3a8a
- **متن ثانویه**: #6b7280

## 📞 پشتیبانی

برای هرگونه سوال یا مشکل، با تیم توسعه تماس بگیرید.

---

**نسخه**: 1.0.0  
**تاریخ**: اکتبر 2024  
**توسعه‌دهنده**: IRAN CTS Development Team
