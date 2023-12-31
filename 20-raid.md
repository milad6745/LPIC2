RAID (Redundant Array of Independent Disks) 

نقشه‌های زیرساختی هستند که از چندین درایو (دیسک سخت) برای افزایش کارایی یا ایمنی داده‌ها استفاده می‌کنند. در لینوکس، انواع مختلفی از RAID پشتیبانی می‌شوند. در زیر، چند نوع معمولی از RAID در لینوکس آورده شده‌اند:

1. **RAID 0 (Stripe):**
   - این نوع RAID به صورت تقسیم داده بین درایوها (striping) عمل می‌کند.
   - افزایش عملکرد با افزایش سرعت خواندن/نوشتن به دلیل توزیع داده‌ها بین چندین درایو.
   - بدیهی است که از نظر ایمنی، اگر یکی از درایوها باشکوه شود، داده‌ها از دست می‌روند.

   ```bash
   mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdX /dev/sdY
   ```

2. **RAID 1 (Mirror):**
   - این نوع RAID به صورت آینه‌ای عمل می‌کند، به این معنا که داده‌ها روی هر دو درایو به یکتا تکرار می‌شوند.
   - افزایش ایمنی، اما کاهش ظرفیت فضای ذخیره‌سازی.
   
   ```bash
   mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdX /dev/sdY
   ```

3. **RAID 5 (Stripe with Parity):**
   - این نوع RAID داده‌ها را بین درایوها تقسیم می‌کند و یک درایو برای ذخیره‌سازی اطلاعات باقیمانده (پیرامونی) را اختصاص می‌دهد.
   - افزایش عملکرد و ایمنی نسبت به RAID 0 با حفظ یک درایو برای پیرامونی.

   ```bash
   mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdX /dev/sdY /dev/sdZ
   ```

4. **RAID 6 (Stripe with Double Parity):**
   - مانند RAID 5، اما دو درایو برای پیرامونی استفاده می‌شود.
   - افزایش ایمنی نسبت به RAID 5 با قابلیت تحمل خرابی حداقل دو درایو.

   ```bash
   mdadm --create /dev/md0 --level=6 --raid-devices=4 /dev/sdX /dev/sdY /dev/sdZ /dev/sdW
   ```

این دستورات توسط `mdadm` (مدیر RAID در لینوکس) صادر می‌شوند. حتماً قبل از استفاده از RAID، به مطالعه‌ی مستندات و نکات مرتبط با این ابزار توجه کنید و از اهمیت پشتیبان‌گیری مداوم اطمینان حاصل کنید.


# spare disk


در سیستم‌های RAID (Redundant Array of Independent Disks)، "Spare Disk" یک درایو اضافی است که در نوعی از RAID به عنوان یک رزرو برای جایگزینی درایوهایی که احتمال خرابی دارند، استفاده می‌شود. در صورتی که یکی از درایوهای عضو RAID خراب شود، Spare Disk به عنوان جایگزین فوری و خودکار فعال می‌شود تا سیستم RAID از داده‌ها محافظت کند.

استفاده از Spare Disk از این مزیت برخوردار است که در صورت خرابی یک درایو، جایگزینی فوری و بدون نیاز به دخالت دستی انجام می‌شود. این اقدام به افزایش ایمنی و پایداری سیستم RAID کمک می‌کند.

برای افزودن یک Spare Disk به یک سیستم RAID، معمولاً باید تنظیمات RAID با افزودن درایو جدید به عنوان Spare تغییر داده شود. به عنوان مثال، در mdadm (مدیر RAID در لینوکس)، می‌توان از دستورات مانند زیر استفاده کرد:

```bash
mdadm --add /dev/md0 /dev/sdX
```

در این دستور، `/dev/md0` نمایانگر آرایه RAID است و `/dev/sdX` نمایانگر درایو Spare است که به آرایه اضافه می‌شود. این درایو به عنوان Spare Disk برای تعویض خودکار در صورت خرابی یکی از درایوهای عضو به کار می‌رود.
