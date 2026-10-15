# مستندات مخزن VPS

این فایل README حاوی توضیحات و نمونه‌ٔ عملیاتی دربارهٔ سیستم‌عامل لینوکس (اوبونتو) برای استفاده‌ی عمومی روی سرورهای VPS است.

## توضیح نمونه دربارهٔ لینوکس اوبونتو

اوبونتو (Ubuntu) یکی از محبوب‌ترین توزیع‌های لینوکس است که برای سرورها و دسکتاپ‌ها استفاده می‌شود. اوبونتو مبتنی بر دبیان است و نسخه‌های LTS (پشتیبانی بلندمدت) هر ۲ سال یک‌بار منتشر می‌شود و برای محیط‌های سرور بسیار مناسب است.

ویژگی‌های کلیدی:
- پشتیبانی LTS (Long Term Support)
- مدیریت بسته با apt
- جامعهٔ بزرگ و مستندات گسترده
- مناسب برای محیط‌های ابری و VPS

## دستورات پایه‌ای و اقدامات اولیه بر روی سرور اوبونتو

1. بروزرسانی بسته‌ها:

```bash
sudo apt update && sudo apt upgrade -y
```

2. ساخت کاربر جدید و افزودن به گروه sudo:

```bash
sudo adduser myuser
sudo usermod -aG sudo myuser
```

3. تنظیم احراز هویت کلید عمومی SSH (به‌جای رمز عبور):

- روی ماشین محلی: `ssh-keygen` سپس `ssh-copy-id myuser@server_ip`
- یا دستی فایل `~/.ssh/authorized_keys` را روی سرور ویرایش کنید.

4. غیرفعال کردن ورود مستقیم با کاربر root (ویرایش `/etc/ssh/sshd_config`):

```text
PermitRootLogin no
PasswordAuthentication no
```

سپس سرویس SSH را ری‌استارت کنید:

```bash
sudo systemctl restart sshd
```

5. تنظیم فایروال با ufw:

```bash
sudo apt install ufw -y
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

6. نصب و پیکربندی اولیه ابزارهای امنیتی:

```bash
sudo apt install fail2ban -y
# فایل‌های تنظیمات را بر حسب نیاز و تعداد تلاش‌های ناموفق و مدت زمان بن تنظیم کنید
```

7. مدیریت سرویس‌ها با systemd:

```bash
sudo systemctl status nginx
sudo systemctl enable nginx
sudo systemctl restart nginx
```

8. تنظیم منطقهٔ زمانی و محلی‌ها (Locale):

```bash
sudo timedatectl set-timezone Asia/Tehran
sudo locale-gen fa_IR.UTF-8
sudo update-locale LANG=fa_IR.UTF-8
```

## توصیه‌ها و نکات امنیتی

- همیشه بسته‌ها را به‌روز نگه دارید.
- ورود با رمز عبور را غیرفعال و از کلیدهای SSH استفاده کنید.
- از فایروال و ابزارهایی مثل fail2ban استفاده کنید.
- دسترسی‌ها را بر پایهٔ حداقل امتیاز (least privilege) تنظیم کنید.
- از بکاپ منظم و مانیتورینگ بهره ببرید.

## منابع مفید

- وب‌سایت رسمی اوبونتو: https://ubuntu.com
- مستندات apt: https://help.ubuntu.com/community/AptGet/Howto

---

اگر دوست دارید این README را به انگلیسی یا با جزئیات بیشتر (مثال‌های سرویس nginx، پایگاه داده، یا اسکریپت‌های اتوماسیون) اضافه کنم، اطلاع دهید.