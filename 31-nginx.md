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

برای تنظیمات بیشتر و اطلاعات پیشرفته‌تر، به مستندات رسمی Nginx مراجعه کنید: [Nginx Documentation](https://nginx.org/en/docs/)
