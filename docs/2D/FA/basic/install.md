# نصب و راه اندازی محیط شبیه‌سازی و تیم پایه

<div id="71789765072"><script type="text/JavaScript" src="https://www.aparat.com/embed/7Z0ha?data[rnddiv]=71789765072&data[responsive]=yes"></script></div>

> تیم رباتیک خواجه نصیر - آموزش نصب ابزارهای پلتفرم دوبعدی فوتبال

این صفحه شامل اطلاعات نصب محیط شبیه‌سازی (سرور و مانیتور) و تیم پایه است که برای اجرای یک مسابقه در این پلتفورم ضروریست.

برای اجرای درست تیم پایه شبیه ساز دوبعدی فوتبال (**Helios Base**) باید ابزار های زیر را نصب داشته باشیم . 

1.  نصب وابستگی های لازم برای build شدن کد lib و همچنین نصب لایبرری های QT مانیتور کردن بازی ها 
2. نصب سرور رسمی مسابقات robocup
3. وابستگی (lib) مورد نیاز برای build شدن تیم پایه
4. نصب یک مانیتور برای مشاهده روند بازی (rcssmonitor یا soccerwindow)



> این آموزش برای نصب سرور و مانیتور پلتفورم شبیه‌سازی دوبعدی فوتبال در سیستم‌عامل **اوبونتو**(ubuntu) است. آموزش زیر بر روی نسخه‌های مختلف سیستم‌عامل اوبونتو (از ۱۶.۰۴ الی ۱۹.۰۴) تست شده است.

<note>
در صورتی که سیستم‌عامل اوبونتو را روی سیستم خود نصب ندارید میتوانید از 
<a href="http://linux-zone.org/forums/%D8%A7%D9%86%D8%AC%D9%85%D9%86-%D9%84%DB%8C%D9%86%D9%88%DA%A9%D8%B3-linux-forum/%D8%AA%D9%88%D8%B2%DB%8C%D8%B9-%D9%87%D8%A7%DB%8C-%D9%84%DB%8C%D9%86%D9%88%DA%A9%D8%B3-linux-distributions/debian-ubuntu-mint/3870-%D8%A2%D9%85%D9%88%D8%B2%D8%B4-%D9%86%D8%B5%D8%A8-ubuntu-16-10-16-04-%D8%AF%D8%B1-%DA%A9%D9%86%D8%A7%D8%B1-%D9%88%DB%8C%D9%86%D8%AF%D9%88%D8%B2-8-10-%D8%A8%D9%87-%D8%B5%D9%88%D8%B1%D8%AA-dual-boot"> اینجا</a>
شروع کنید.
</note>



در این قسمت و یا قسمت‌های دیگر اصطلاح **Build** به فرایند ساخت فایل اجرایی از کد گفته می‌شود این فرایند ممکن است شامل مراحل زیادی باشد. در شبیه‌سازی دوبعدی اکثرا از ابزار [GNU Make](https://www.gnu.org/software/make/) اسفتاده میشود که با دستور **make** خود مراحل لازم برای این فرایند را خودکار اجرا میکند.



## نصب وابستگی‌ها 

پیش از نصب وابستگی‌ها **بهتر** است که مخازن سیستم‌عامل خود را به روز رسانی کنید:‌

```bash
sudo apt-get update
```

حال برای نصب شدن وابستگی‌های مورد نیاز سرور دستور زیر را در ترمینال وارد کنید :‌

```bash
sudo apt-get install g++ build-essential libboost-all-dev qt4-dev-tools libaudio-dev libgtk-3-dev libxt-dev bison flex
```



##   دانلود و نصب rcssserver

برای دانلود سرور رسمی مسابقات به [این آدرس](https://github.com/rcsoccersim/rcssserver/releases) مراجعه کنید و آخرین نسخه سرور را دانلود کنید. 

پس از دانلود شدن آن با استفاده از دستور زیر فایل‌ها را از حالت فشرده خارج کنید:‌

```bash
tar -zxpf rcssserver-x.x.x.tar.gz
```

*توجه کنید که به جای x.x.x باید نسخه‌ی سرور دانلود شده را بزنید.*

حال با استفاده از دستورات زیر وارد محل اطلاعات سرور شوید و آن را Build و سپس نصب کنید: 

```bash
cd rcssserver-x.x.x
./configure && make
sudo make install
```

در صورتی که تمامی مراحل با موفقیت طی شود سرور مسابقات به صورت کامل نصب می‌شود و شما میتوانید با زدن دستور زیر سرور را با اجرای یک بازی تست کنید:

```bash
rcssserver
```

در صورت برخورد با ارور زیر:

```bash
rcssserver:error while loading shared libraries: librcssclangparser.so.2: cannot open shared object file: No such file or directory
```

دستور زیر را اجرا کرده و  فایل  `librcssclangparser.so`  پیدا کنید.

در صورت پیدا نشدن این فایل باید دوباره rcssserver را نصب کنید.

```bash
sudo find / -name librcssclangparser.so
```

سپس فایل `ld.so.conf` در حالت سوپر یوزر باز کنید.

```bash
sudo gedit /etc/ld.so.conf
```

و آدرس زیر را به انتهای فایل اضافه و فایل را ذخیره کنید.

```conf
include /usr/local/lib 
```

برای ذخیره شدن تغییرات دستور زیر را در ترمینال اجرا کنید.

```bash
sudo ldconfig
```

حال شما میتوانید با زدن دستور زیر سرور را اجرا کنید.

```bash
rcssserver
```



## نصب مانیتور رسمی مسابقات

برای مشاهده مسابقات این پلتفورم می توانید از مانیتور رسمی مسابقات یا **rcssmonitor** استفاده کنید. که از [این آدرس](https://github.com/rcsoccersim/rcssmonitor/releases) قابل دریافت است.

پس از دریافت فایل اخرین نسخه‌ی rcssmonitor آن را از حالت فشرده خارج کنید.

```bash
tar -zxpf rcssmonitor-x.x.x.tar.gz
```

و سپس نصب کنید.

```bash
cd rcssmonitor-x.x.x
./configure 
make 
sudo make install 
```

برای تست درستی نصب مانیتور میتوانید با دستور زیر مانیتور را اجرا کنید.

```bash
rcssmonitor
```

توجه کنید برای مشاهده بازی‌ها و همینطور استفاده از ابزار‌های دیباگ شما میتوانید از ابزار [soccerwindow2](https://rcss.ir/2D/FA/tools/soccerwindow2) نیز استفاده کنید.



## نصب کتابخانه‌ی Librcsc

کتابخانه تیم پایه‌ی Agent2D موسوم به Librcsc را میتوانید از [اینجا](https://osdn.net/projects/rctools/releases/p3777) دانلود کنید. نصب این کتابخانه برای Build کردن کد Agent ضروری است. 

پس از دانلود، باید آن را از حالت فشرده خارج کنید. 

```bash
tar -zxpf librcsc-x.x.x.tar.gz
```

در ادامه با استفاده از دستور زیر وارد پوشه Lib شوید. 

```bash
cd librcsc-x.x.x/
```

حال برای Build و نصب کتابخانه دستورات زیر را وارد کنید.

```bash
./configure 
make
sudo make install
```



## نصب تیم پایه‌ی Agent2D

برای دانلود تیم پایه‌ی Agent2D یا همان Helios Base به [این](https://osdn.net/projects/rctools/releases/55186) لینک مراجعه کنید. 

پس از آن که فایل Agent2D را دانلود کردید حال باید آن را با استفاده از دستورات زیر از حالت فشرده خارج کنید.

```bash
tar -zxpf agent2d-x.x.x.tar.gz
```

در ادامه با استفاده از دستور زیر وارد پوشه Agent شوید. 

```bash
cd agent2d-x.x.x/
```

در نهایت برای ساخت فایل اجرایی آن را Build کنید. دقت کنید در این مرحله نیازی به نصب نیست.

```bash
./configure CXXFLAGS='-std=c++05'
make
```



## اجرای یک بازی

حال که سرور، مانیتور، کتابخانه Agent2D و کد تیم پایه Agent2D به طور کامل نصب شد حال میتوانیم یک بازی اجرا کنیم. برای اجرای این بازی اول نیاز است در یک ترمینال دستور زیر را وارد کنید.

```bash
rcssserver
```

با اجرا این دستور سرور اجرا شده و منتظر اتصال مانیتور و همینطور بازیکنان می‌شود.

حال در ترمینالی دیگر وارد پوشه کد Agent2D شده و با دستور زیر اولین تیم را با نام team1 اجرا میکنیم.

```bash
cd src
./start.sh -t team1
```

حال ترمینال دیگری را باز در محل کد Agent2D باز کرده و تیم دیگری را مقابل این تیم با نام team2 اجرا میکنیم.

```bash
cd src
./start.sh -t team2
```

در صورتی که دستورات به طور کامل درست انجام شده باشد در ترمینالی که سرور در آن ران شده است با همچین تصویری رو به رو میشوید.

<ImageZoom 
  src="/docs/2D/FA/img/doc/basic/rcssserver_run_a_game.jpg" 
  :border="false" 
  width="auto"
/>

حال با اجرای مانیتور در ترمینالی دیگر میتوانید بازی را مشاهده کنید.

```bash
rcssmonitor
```

در صورت اجرای درست دستورات با همچین صحنه‌ای روبه‌رو می‌شوید.



<ImageZoom 
  src="/docs/2D/FA/img/doc/basic/rcssmonitor_run_a_game.jpg" 
  :border="false" 
  width="auto"
/>



تبریک، حالا شما توانستید اولین بازی خود را در این پلتفورم اجرا کنید.