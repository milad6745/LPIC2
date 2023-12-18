# nginx
نصب و تنظیمات Nginx (موتور اجاره‌ای HTTP) ممکن است بسته به سیستم عامل شما وابسته باشد. در اینجا، یک راهنمای کلی برای نصب و تنظیمات اولیه Nginx بر روی سرور لینوکس ارائه می‌شود.

### برای Ubuntu/Debian:

1. **نصب Nginx:**
    ```bash
    sudo apt update
    sudo apt install nginx
    ```

2. **شروع و فعال‌سازی Nginx:**
    ```bash
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```

3. **تنظیمات پایه:**
    - فایل تنظیمات اصلی Nginx در `/etc/nginx/nginx.conf` قرار دارد. می‌توانید تنظیمات اصلی را در اینجا اعمال کنید.

4. **اجرای مجدد Nginx:**
    ```bash
    sudo systemctl restart nginx
    ```

### برای CentOS/RHEL:

1. **نصب Nginx:**
    ```bash
    sudo yum install nginx
    ```

2. **شروع و فعال‌سازی Nginx:**
    ```bash
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```

3. **تنظیمات پایه:**
    - فایل تنظیمات اصلی Nginx در `/etc/nginx/nginx.conf` قرار دارد. می‌توانید تنظیمات اصلی را در اینجا اعمال کنید.

4. **اجرای مجدد Nginx:**
    ```bash
    sudo systemctl restart nginx
    ```

### تنظیمات وبسایت اولیه:

1. **ایجاد یک فایل تنظیمات برای وبسایت:**
    - ایجاد یک فایل تنظیمات برای وبسایت در `/etc/nginx/sites-available/` با پسوند `.conf`.

    ```nginx
    server {
        listen 80;
        server_name your_domain.com www.your_domain.com;

        location / {
            root /path/to/your/web/files;
            index index.html;
        }
    }
    ```

2. **لینک کردن به `sites-enabled`:**
    - ایجاد یک لینک نمادین (symbolic link) به فایل تنظیمات وبسایت در `/etc/nginx/sites-enabled/`.

    ```bash
    sudo ln -s /etc/nginx/sites-available/your_site.conf /etc/nginx/sites-enabled/
    ```

3. **اجرای مجدد Nginx:**
    ```bash
    sudo systemctl restart nginx
    ```

4. **تست تنظیمات:**
    - باز کردن مرورگر و وارد کردن آدرس IP یا نام دامنه شما باید صفحه وبسایت شما نمایش داده شود.



بله، حالا به تنظیمات مهم تر Nginx می‌پردازیم. معمولاً تنظیمات اصلی Nginx در فایل `/etc/nginx/nginx.conf` و تنظیمات وبسایت‌ها در فایل‌های مختلفی در دایرکتوری `/etc/nginx/sites-available/` قرار دارند. در اینجا، به بخش‌های مهم از این فایل‌ها می‌پردازیم:

### فایل `/etc/nginx/nginx.conf`:

1. **تنظیمات عمومی:**
   - در این بخش، می‌توانید تنظیمات عمومی Nginx را اعمال کنید. مثلاً:

     ```nginx
     user www-data;
     worker_processes auto;
     error_log /var/log/nginx/error.log;
     ```

2. **تنظیمات انجام‌دهنده:**
   - مشخص کردن تنظیماتی که به هر دستگاه اجرا کننده اختصاص داده می‌شود:

     ```nginx
     http {
         include /etc/nginx/mime.types;
         default_type application/octet-stream;

         sendfile on;
         tcp_nopush on;
         tcp_nodelay on;
         ```

### فایل `/etc/nginx/sites-available/your_site.conf`:

1. **تنظیمات وبسایت:**
   - در این بخش، تنظیمات مربوط به هر وبسایت را مشخص می‌کنید. نام وبسایت، پورت‌ها، مسیرهای دسترسی و... را تعیین می‌کنید.

     ```nginx
     server {
         listen 80;
         server_name your_domain.com www.your_domain.com;

         location / {
             root /path/to/your/web/files;
             index index.html;
         }
     }
     ```

2. **تنظیمات لاگ:**
   - تنظیم لاگ‌های وبسایت برای رصد و ثبت رخدادها.

     ```nginx
     access_log /var/log/nginx/your_domain.access.log;
     error_log /var/log/nginx/your_domain.error.log;
     ```

3. **تنظیمات SSL (اگر از HTTPS استفاده می‌کنید):**
   - اگر می‌خواهید از HTTPS استفاده کنید، باید تنظیمات SSL را اعمال کنید.

     ```nginx
     server {
         listen 443 ssl;
         server_name your_domain.com www.your_domain.com;

         ssl_certificate /path/to/your/certificate.crt;
         ssl_certificate_key /path/to/your/private.key;
         ssl_protocols TLSv1.2 TLSv1.3;
         ssl_ciphers 'TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384';
     }
     ```

4. **انجام مجدد Nginx:**
    ```bash
    sudo systemctl restart nginx
    ```

توجه داشته باشید که این فقط یک نمونه کانفیگ است و بسته به نیازها و محیط‌های مختلف، تنظیمات ممکن است متفاوت باشند. همچنین، می‌توانید از امکانات بیشتر و پیشرفته‌تر Nginx برای بهینه‌سازی و امنیت بیشتر استفاده کنید.
