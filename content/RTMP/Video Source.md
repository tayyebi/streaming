# راهکار اول - استفاده از نرم‌افزار OBS

1. ابتدا نرم‌افزار متناسب با سیستم‌عامل خود را از وب‌سایت پروژه دانلود نمایید:
<https://obsproject.com>

2. سپس وارد قسمت تنظیمات (Settings) شوید.

3. چنانچه قصد استریم مستقیم بر روی هر یک از سرویس‌های پیشنهاد شده را دارید، از گزینه‌ی مربوطه استفاده نمایید. در غیر این صورت برای استفاده اتصال به سرور استریم این پروژه، سرویس را «دلخواه...» (Custom) انتخاب کنید.

4. آدرس استریم را به صورت زیر تنظیم کنید (Server)
    ```
    rtmp://stream.example.com/live/
    ```

5. کلید استریم را به صورت زیر تنظیم کنید:
    ```
    STREAMTITLE?psk=SECRETKEY
    ```
    دقت کنید که به جای STREAMTITLE باید مقدار واقعی متغیر قرار گیرد. این امر در مورد SECRETKEY نیز صادق است.

6. تنظیمات خروجی (Output) را طبق حالت پیشنهادی زیر تغییر دهید:
    Streaming:
    ```
    Encoder: x264
    Rescale Ouptut: 1366x768
    Enforce streaming service encoder settings: checked
    Rate Control: CRF
    CPU Usage Preset: ultrafast
    ```
    Recording:
    ```
    Type: Standard
    Recording Path: مسیر دلخواه خود را انتخاب نمایید (هشدار: چنانچه ظرفیت دیسک سیستم‌عامل پایین است، از دسکتاپ استفاده نکنید)
    Recording Format: mp4
    Encoder: Use stream encoder
    ```
7. سپس وارد قسمت ویدئو (Video) شده و تنظیمات پیشنهادی زیر را اعمال نمایید:
    ```
    Base (Canvas) Resolution: 1366x768
    Output (Scaled) Resolution: 1366x768
    Downscale Filter: Lanczos (Sharpened Scaling, 36 Samples)
    Integer FPS Value: 15
    ```