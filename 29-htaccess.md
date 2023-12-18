
### نمونه استفاده از فایل `.htaccess`:

1. **محافظت از دسترسی به فایل‌ها:**
   - اگر می‌خواهید از دسترسی به یک فایل یا دایرکتوری خاص جلوگیری کنید، می‌توانید از دستورات زیر در فایل `.htaccess` استفاده کنید:
     ```apache
     <Files "filename.txt">
       Deny from all
     </Files>
     ```
     در اینجا `filename.txt` نام فایل یا دایرکتوری مورد نظر است.

2. **ریدایرکت:**
   - برای انجام ریدایرکت‌های مختلف، از دستورات `Redirect` یا `RewriteRule` استفاده می‌شود. مثال:
     ```apache
     # ریدایرکت از یک مسیر به مسیر دیگر
     Redirect 301 /old-page.html http://example.com/new-page.html
     ```
     یا
     ```apache
     # استفاده از ماژول Rewrite برای ریدایرکت
     RewriteEngine On
     RewriteRule ^old-page\.html$ http://example.com/new-page.html [L,R=301]
     ```

3. **تنظیم هدرها:**
   - از دستورات `Header` برای تنظیم هدرهای HTTP استفاده می‌شود. مثال:
     ```apache
     # اجازه‌دهی فرمت‌های مختلف فایل‌های فشرده
     <FilesMatch "\.(js|css|xml|gz)$">
       Header append Vary Accept-Encoding
     </FilesMatch>
     ```

4. **احراز هویت HTTP:**
   - برای اعمال احراز هویت HTTP، می‌توان از دستورات `AuthType` و `AuthUserFile` استفاده کرد. مثال:
     ```apache
     AuthType Basic
     AuthName "Restricted Area"
     AuthUserFile /path/to/.htpasswd
     Require valid-user
     ```

5. **غیرفعال‌سازی لیستینگ دایرکتوری:**
   - اگر نخواهید لیستینگ دایرکتوری فعال باشد، از دستور زیر استفاده کنید:
     ```apache
     Options -Indexes
     ```

به عنوان توجه، برخی از این تنظیمات باید توسط مدیران سرور یا مالکان سیستم پیکربندی شوند و برخی از قابلیت‌ها بسته به تنظیمات سرور Apache قابل دسترسی نیستند.
