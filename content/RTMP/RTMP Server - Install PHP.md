# نصب php
```
sudo apt-get install php-fpm
```

# کانفیگ پی‌اچ‌پی
```
sudo vi /etc/php/7.2/fpm/php.ini
```

# مشاهده‌ی خطا‌های پی‌اچ‌پی
```
sudo cat /var/log/php7.2-fpm.log
```

# کانفیگ ngnix برای پردازش php

فایل زیر را برای ویرایش باز کنید:

```
sudo vi /etc/ngnix/sites-enabled/default
```

و محتوای آن را به صورت زیر تغییر دهید:

<pre><code>
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;
    
	index index.html index.htm index.php;

    # تنظیم آی‌پی یا نام دامنه سرور
	server_name stream.example.com;

	location / {
		try_files $uri $uri/ =404;
	}

	# بخش فعال ساز اینترپرتر پی‌اچ‌پی
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
	
		# With php-fpm (or other unix sockets):
		fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
		# With php-cgi (or other tcp sockets):
		#fastcgi_pass 127.0.0.1:9000;
	}

    # بستن دسترسی به فایل‌های اچ‌تی
	location ~ /\.ht {
		deny all;
	}
}
</code></pre>

> توجه: بازنشانی سرویس وب سرور ضروری است