<base target="_blank">

<div dir="ltr" >



[**🇺🇸 English**](README.md)
</div>
<br>
<div align=center markdown="1">
 

![Hiddify Logo](https://user-images.githubusercontent.com/125398461/227777845-a4d0f86b-faa2-4f2b-a410-4aa5f68bfe19.png)

</div>

<div dir="rtl" align="right">

# اسکنر ریالیتی هیدیفای
این یک اسکنر TLS است که به شما کمک می‌کند شبکه‌های مختلف را اسکن کنید و بر اساس لیستی از SNI‌ها بهترین SNI را برای ریالیتی روی شبکه خود پیدا کنید. برای اطلاعات بیشتر در خصوص توسعه می‌توانید [دستورالعمل‌های مشارکت](CONTRIBUTING.md) در پروژه ما را مطالعه نمایید.

## ⚙️ نصب
نصب این اسکنر دارای دو بخش است. بخش نخست یک اپلیکیشن سمت سرور است که باید روی سرور شما نصب شود و بخش دوم نیز یک اسکریپت سمت کلاینت است که باید روی کامپیوتر شما نصب گردد.


#### 🛠️ نصب سمت سرور
* ابتدا نیاز است شما هسته Xray کاستوم شده ما را روی سرور خود با استفاده از دستور زیر نصب کنید:
</div>

<div dir=ltr>
 
```
# نصب ایکس‌ری قدیمی
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ remove 

# تنها اگر هیدیفای‌منیجر دارید
systemctl stop hiddify-xray 

# نصب ایکس‌ری کاستوم شده هیدیفای
 
bash -c "$(curl -L https://github.com/hiddify/Xray-core-custom/raw/main/install-release.sh)" @ install

# تنها اگر هیدیفای‌منیجر دارید
systemctl start hiddify-xray

```
</div>


<div dir="rtl" align="right">
 
* حالا باید یک فایل کانفیگ با SNI خالی را روی پنل خود ایجاد کنید یا از کانفیگ زیر استفاده نمایید:
</div>

<div dir=ltr>
 
```
curl -o server_config.json https://raw.githubusercontent.com/hiddify/Hiddify_Reality_Scanner/main/server_config.json

echo "---------------IPV6---------"
echo "vless://hiddify@$(curl -6 ip.sb):11443/?fp=chrome&security=reality&pbk=Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw&sid=6ba85179e30d4fc2&sni=www.google.com&type=tcp&flow=xtls-rprx-vision&encryption=none#Hiddify"

echo "---------------IPV4---------"
echo "vless://hiddify@$(curl -4 ip.sb):11443/?fp=chrome&security=reality&pbk=Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw&sid=6ba85179e30d4fc2&sni=www.google.com&type=tcp&flow=xtls-rprx-vision&encryption=none#Hiddify"

```
</div>

<div dir="rtl" align="right">

* سپس می‌بایست کانفیگ را با Xray مثل کامند زیر اجرا نمایید. این کار یک سرور Xray موقت برای تست ایجاد می‌کند:
</div>


<div dir=ltr>
 
```
xray run -c server_config.json
```
</div>

<div dir="rtl" align="right">
 
* می‌توانید کانفیگ ریالیتی را به شکل زیر استفاده نمایید:
</div>

<div dir=ltr>
 
```
vless://hiddify@SERVER_IP:11443/?fp=chrome&security=reality&pbk=Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw&sid=6ba85179e30d4fc2&sni=www.yahoo.com&type=tcp&flow=xtls-rprx-vision&encryption=none#Hiddify
```
</div>

<div dir="rtl" align="right">
 

#### 🛠️ نصب سمت کلاینت
برای سمت کلاینت کافیه از Pypi استفاده نمایید و کامند زیر را ارا نمایید:
</div>

<div dir=ltr>
 
```bash
pip install -U hiddify_reality_scanner
```
</div>

<br>

<div dir="rtl" align="right">

## 🚀 استفاده پایه
جهت اجرای این اسکنر ابتدا [پایتون](https://www.python.org/downloads/) را روی سیستم خود نصب کنید، سپس یکی از دستورات زیر را روی کلاینت خود اجرا نمایید:
</div>

<div dir=ltr>
 
```bash
python -m hiddify_reality_scanner "vless_link"
#or
hiddify_reality_scanner "vless_link"
```
</div>

> دقت شود که به جای `vless_link` می‌بایست کانفیگ ریالیتی خود را جایگزین نمایید.

<div dir="rtl" align="right">
 
## 🚀 استفاده پیشرفته
* اگر بخواهید پارامترهای بیشتری را هنگام اسکن در نظر بگیرید، می‌بایست از دستور زیر روی کلاینت خود استفاده نمایید:
</div>

<div dir=ltr>

```bash
hiddify_reality_scanner --jobs 10 --limit 100 --sni yahoo.com,google.com "vless_link"
```
</div>

<div dir="rtl" align="right">


- در اینجا:
  - پارامتر ` jobs 10--` تعداد اسکن همزمان را تعیین می‌کند. اگر از این پارامتر استفاده نکنید، مقدار دیفالت اسکن همزمان ۱۰ می‌باشد.
  - پارامتر `sni--` نیز SNIهای مورد نظر را برای اسکن مشخص می‌کند.
  - پارامتر `limit 100--` تعداد دامنه‌هایی که کار می‌کند را در لیست نتایج خروجی به ۱۰۰ دامنه محدود می‌کند.اگر از این پارامتر استفاده نکنید، مقدار دیفالت لیست خروجی ۱۰ می‌باشد.
 
* اگر بخواهید لیستی از SNIها را به اسکنر بدهید، می‌بایست از دستور زیر استفاده نمایید:
</div>

<div dir=ltr>
 
 ```bash
hiddify_reality_scanner --jobs 10 --limit 100 --sni path_to_the_list "vless_link"
```

</div>

<div dir="rtl" align="right">
 
- در اینجا:
  - پارامتر ` jobs 10--` تعداد اسکن همزمان را تعیین می‌کند. اگر از این پارامتر استفاده نکنید، مقدار دیفالت اسکن همزمان ۱۰ می‌باشد.
  - پارامتر `sni path_to_the_list--` مسیر مربوط به لیست SNI مورد نظر را مشخص می‌کند.
  - پارامتر `limit 100--` تعداد دامنه‌هایی که کار می‌کند را در لیست نتایج خروجی به ۱۰۰ دامنه محدود می‌کند.اگر از این پارامتر استفاده نکنید، مقدار دیفالت لیست خروجی ۱۰ می‌باشد.
 
> نکته: در حین اسکن، اگر می خواهید آن را قطع کنید، می‌توانید به سادگی از `ctrl+c` استفاده کنید.

## 📊 نتایج
خروجی اسکنر در فایل‌های `results.txt` و `results.json` روی کلاینت شما ذخیره می‌گردد. شما می‌توانید از این SNIها برای ایجاد دامنه‌های ریالیتی در سرور خود استفاده نمایید. [نحوه ثبت دامنه ریالیتی در هیدیفای‌منیجر](https://github.com/hiddify/Hiddify-Manager/wiki/%D8%A2%D9%85%D9%88%D8%B2%D8%B4-%D8%A7%D8%B3%D8%AA%D9%81%D8%A7%D8%AF%D9%87-%D8%A7%D8%B2-Reality-%D8%AF%D8%B1-%D9%87%DB%8C%D8%AF%DB%8C%D9%81%D8%A7%DB%8C)

> نکته: اگر اسکنر سمت سرور را روی Hiddify Manager خود نصب کرده‌اید، پس از اتمام اسکن باید دستور زیر را اجرا کنید تا هسته اصلی Xray سرور شما فعال گردد.

</div>

<div dir=ltr>
 
```
systemctl start hiddify-xray
```

</div>

