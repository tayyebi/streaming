# احزار هویت با صفحات وب
برای احراز هویت تولید کننده‌ی محتوا باید از یک فایل پی‌اچ‌پی که از طریق http در دسترس است استفاده کنید.

ابتدا وارد ریشه‌ی وب شوید و فایل *auth.php* را برای ویرایش آماده کنید:

```
cd /var/www/html/
sudo vi auth.php
```

محتوای فایل به صورت زیر است:

<pre><code>
<\?php
// دریافت دامپ درخواست برای لاگ
ob_start();
date_default_timezone_set('Asia/Tehran');
echo $date = date('m/d/Y h:i:s a', time());
print_r($_REQUEST);
$data = ob_get_clean();

// اضافه کردن آن به فایل
$fp = fopen('.htlogs.txt', 'a');
fwrite($fp, $data . '//////');  
fclose($fp);

// انجام احراز هویت
$username = $_POST["name"];
$password = $_POST["psk"];

// لیست نام‌های کاربری و گذرواژه‌های مجاز
$valid_users = array("YOUR_LIVE_NAME" => "YOUR_SECRET_KEY",);

if ($valid_users[$username] == $password) {
http_response_code(201);
} else {
http_response_code(404);
}
?>
</code></pre>

این فایل باید از طریق آدرس زیر برای عموم کاربران مجاز شبکه در دسترس باشد:

```
http://stream.example.com/auth.php
```
