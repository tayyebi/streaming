# سیستم‌عامل سرور
سرور می‌تواند بر پایه‌ی هر سیستم‌عامل استانداری در نظر گرفته شود.
> در این سند از سیستم‌عامل ubuntu server 18.04 استفاده شده است.

# نصب ngnix
با استفاده از پکیج منیجر
```
mkdir ngnix
cd ngnix
sudo apt --print-uris --yes install ngnix | grep ^\' | cut -d\' -f2 > ngnix.txt
wget -i ngnix
sudo dpkg -i *.deb
‍‍‍‍‍cd ..
```
یا به صورت خلاصه
```
sudo apt install ngnix
```

# نصب rtmp-mod
```
sudo add-apt-repository universe
sudo apt install libnginx-mod-rtmp
```

# کانفیگ ngnix برای پشتیبانی از rtmp
ابتدا فایل کانفیگ را برای ویرایش آماده کنید

```
sudo vi /etc/ngnix/ngnix.conf
```

بخش زیر را به انتهای فایل اضافه کنید:

<pre><code>
rtmp {
    server {
        listen 1935;
        chunk_size 16384;

        application live {
            live on;
            on_publish http://stream.example.com/auth.php;
            push rtmp://live-fra05.twitch.tv/app/LIVE_SECRET_CODE_HERE;
            push rtmp://rtmp.cdn.asset.aparat.com:443/event/LIVE_SECRET_CODE_HERE;
            record off;
        }
    }
}
</code></pre>

دقت کنید که چنانچه قصد استریم همزمان بر روی سرور‌های دیگر را ندارید می‌توانید خطوط *push* را حذف کنید.

درباره‌ی *on_publish* و احراز هویت در بخش‌های بعدی توضیح داده شده است.

برای ترتیب اثر ابتدا از صحت کانفیگ فایل تست اطمینان حاصل کنید:
```
sudo ngnix -t
```

در صورت وجود نداشتن هیچ خطایی،
سرویس مربوطه را بازنشانی کنید:
```
sudo service ngnix restart
```
و یا
```
sudo systemctl restart ngnix
```
