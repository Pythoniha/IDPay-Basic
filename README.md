# Implemented IDPay payment documentation library
# کتابخانه پیاده سازی شده مستندات پرداخت IDPay
این کتابخانه یک کتابخانه بیسیک برای استفاده راحت تر از مستندات پرداخت درگاه پرداخت IDPay می باشد. در ادامه کل توابع که برای استفاده از این کتابخه برای شما شرح داده می شود.

این کتابخانه با استفاده از متود های شی گرایی پایتون نوشته شده است پس برای استفاده از این کتابخانه نیاز به تنظیمات اولیه دارد که می توانید برای ست کردن تنظیم اولیه باید ابتدا چند مقدار اولیه را به نرم افزار بدهید.

1. مقدار API KEY (که باید از قسمت پروفایل کاربری / وب سرویس های من کپی کرده و در کد قرار دهید.)
2. مقدار X-SANDBOX که به صورت Boolean یا همان متغییر False یا True بوده و بیانگر حالت استفاده از درگاه پرداخت به صورت آزمایشی یا در حالت واقعی است.
3. حالت سوم به صورت کاملا ثابت می باشد که مقدار application/json را دارد که بیان گر حالت دریافت/ارسال اطلاعات و پارامتر ها به صورت رشته Json است. 
برای نمونه مثال های بالا کد زیر را در نظر بگیرید:
```python
id = idpay("19cc697a-747a-4166-a76e-103240874dda", "http://localhost:8000/")
```
توضیح کد بالا :
کد بالا یک تابع __init__ را از کلاس اصلی idpay فراخانی می کند و در قسمت اول ورودی X-API-KEY و در قسمت دوم آدرس Callback که هم در درگاه پرداخت خود در پنل مدیریت پروفایل idpay را ثبت کرده اید پاس می دهد.
در این کتابخانه حالت آزمایشی به صورت دیفالت بر روی کتابخانه True قراردارد و اگر می خواهید حالت آن را به False تغییر دهید می توانید از قطعه کد زیر استفاده کنید :
```python
id = idpay("19cc697a-747a-4166-a76e-103240874dda", "http://localhost:8000/", sandbox = False)
```
======
## تابع پرداخت
در اولین مرحله از ثبت اطلاعات سبد خرید باید ابتدا یک تراکنش را ایجاد کنید، ابتدا برای ایجاد تراکنش به صورت خودکار باید تنظیمات مرحله اول را به درستی انجام داده باشید سپس برای ایجاد یک تراکنش باید مقدار های زیر را به تابع payment از کلاس idpay پاس دهید.

نکته : همه مقدار های گفته شده در زیر ضروری نیستند و شما می توانید فقط مقدار های ضروری را به سمت سرور برای ایجاد تراکنش پاس دهید.

نکته 2 : مقدار های ضروری حتما باید به صورت صحیح به تابع اصلی پاس داده شوند.
```
*"order_id": شماره سفارشی که از سبد خرید باید پاس داده شود
*"amount": قیمت کل سبد خرید به صورت جمع خورده
"name" : نام پرداخت کننده
"phone" : شماره موبایل پرداخت کننده 
"mail" : ایمیل ادرس پرداخت کننده
"desc" : توضیحات که این تراکنش به خود اختصاص می دهد.
*"callback": آدرس صفحه ای که بعد از ثبت تراکنش به صورت موفق به آن وب سرویس ریدایرکت می شود.
```
توضیح مقدار کد بالا :

نکته : در کد بالا مقدار Order_id , Amount  و Callback حتما برای ساخت یک تراکنش ضروری هستند و باید به تابع Payment پاس داده شوند.


نکته 2 : آدرسی که برای Callback در نظر می گیرید حتما باید یک وبسرویس فعال باشد، اگر در حالت آزمایشی می خواهید یک تراکنش را تست کنید می توانید از localhost استفاده کنید اما اگر در حالت واقعی در حال ساخت یک تراکنش واقعی در درگاه بانکی هستید حتما باید یک آدرس وبسرویس فعال داشته باشید و حتما این ادرس وبسرویس شما باید در قسمت ( وب سرویس های من) در صفحه پروفایل شما قرار داشته باشد. 


بعد از در نظر گرفتن توضیحات بالا با استفاده از قطعه کد زیر یک تراکنش را ایجاد می کنید :

```python
id = idpay("6a7f99eb-7c20-4412-a972-6dfb7cd253a4", "http://localhost:8000/")
id.payment(1200 ,1000, 'dashboard')
```

توضیح کد بالا :

در خط اول کد طبق توضیحات قبلی که دادیم، متغییر X-API-KEY را برای ارسال به تنظیمات اصلی پاس دادیم و در قسمت دوم ادرس اصلی که در قسمت وب سرویس های من بوده را به تنظیمات کلاس پاس دادیم. در قسمت سوم می توانیم کل کلاس را به صورت حالت آزمایشی و یا در حالت واقعی تنظیم کنیم که اگر می خواهید تراکنش در حالت واقعی اتفاق بیوفتد باید قطعه کد بالا را به صورت زیر تنظیم کنید.

```python
id = idpay("6a7f99eb-7c20-4412-a972-6dfb7cd253a4", "http://localhost:8000/", sandbox = False)
id.payment(1200 ,1000, 'dashboard')
```

بعد از اجرا کد بالا باید یک خروجی مشابه خروجی زیر دریافت کنید :
```
Payment Successful
{'id': 'b5bbc2808e30e1169b3661a30cf9d41b', 'link': 'https://idpay.ir/p/ws-sandbox/b5bbc2808e30e1169b3661a30cf9d41b'}
```

در خروجی بالا دقت داشته باشید که رشته json حاوی مقادیر id , Link برای شما برگردانده میشوند.

توضیحات : 

در قطعه کد بالا رشته id که برای شما برگردانده می شود باید در دیتابیس خود ذخیره کرده تا بتوانید در مراحل احراز هویت اصلی تابع Callback که در ادامه به توضیح این تابع می رسیم انجام دهید.

id : یک رشته حاوی حروف و اعداد می باشد که به صورت یکتا برای احراز هویت تراکنش شما در دست شما قرار خواهد گرفت.

link : لینک هم به صورت کاملا یکتا می باشد که نشان دهنده ساخت شدن تراکنش شما از سمت سرور است و شما رو در ادامه روند پرداخت کمک خواهد کرد.


