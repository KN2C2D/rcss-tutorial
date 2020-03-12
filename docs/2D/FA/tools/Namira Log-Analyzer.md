​	 	 	**[Namira Log-Analyzer](https://github.com/Farzin-Negahbani/Namira_LogAnalyzer)**

یک اسکریپت پایتون برای تجزیه و تحلیل بازی های شبیه سازی دوبعدی فوتبال

**کاربرد**

تولید اطلاعات جامع در مورد عملکرد تیم شما در مسابقات مختلف.ارزیابی قابلیت های مختلف تیم شما.استفاده از داده های استخراج شده برای آموزش الگوریتم های machine learning .
**شروع به استفاده** 

پیش نیاز

`sudo apt-get updatesudo apt-get install python3 python3-pip python3-setuptools python3-numpy python3-matplotlib`

نصب کردن

`git clone https://github.com/Farzin-Negahbani/Namira_LogAnalyzer.git`

`cd Namira_LogAnalyzer`

روش اول

`sudo python3 ./setup.py install`

روش دوم

`pip install .`

پاک کردن

`pip uninstall loganalyzer`

**قابلیت ها**

- پاس
  - شمارش پاس
    - پاس های طولی
    - پاس های عرضی
    - در ۹ منطقه زمین (A,B,...I)
    - پاس های صحیح
  - دقت پاس
  - پاس های قطع شده

- شوت
  - شمارش شوت
    - شوت های طولی
    - شوت های عرضی
    - در ۹ منطقه زمین (A,B,...I)
    - شوت های در چارچوب
    - شوت های خارج از چارچوب
  - دقت شوت

- مالکیت
  - مالکیت هر تیم در ۹ منطقه زمین (A,B,...I)
  - مالکیت هر بازیکن در ۹ منطقه زمین (A,B,...I)
  - مالکیت هر تیم یا هر بازیکن در هر منطقه دلخواه

- موقعیت 
  - سیکل هایی که هر بازیکن در ۹ منطقه زمین (A,B,...I) قرار داشته
    - سیکل هایی که هر بازیکن در هر منطقه دلخواه قرار داشته

- مسافت حرکت کرده هر بازیکن
- نیروی استفاده شده توسط هر بازیکن
- نیروی استفاده شده توسط هر بازیکن نسبت به مسافت طی شده
- Heatmap بازی برای هر تیم
- شمارش ضربه ها
- شمارش تکل ها
- شمارش say ها

**ناحیه های پیش فرض**



![default_regions](/docs/2D/FA/img/doc/tools/default_regions.jpeg)



**نحوه استفاده**
برای بررسی نحوه بازیابی اطلاعات ، به فایل Testcase.py نگاهی بیندازید.

**به عنوان یک اسکریپت**

```
loganalyzer --path <log file without .rcl or .rcg >
```

#### 

**به عنوان یک ماژول**

```
import loganalyzer
from loganalyzer import Parser
from loganalyzer import Game
from loganalyzer import Analyzer
parser = Parser('path to log file without .rcl or .rcg')
game = Game(parser)
analyzer = Analyzer(game)
analyzer.analyze()
left_team_pass = analyzer.pass_l
left_team_in_target_shoot = analyzer.in_target_shoot_l
left_team_agent_1 = game.left_team.agents[0].data
```

**ویدیوی آموزشی**
 [آپارات](https://www.aparat.com/v/fJE2C/Namira_Log_Analyzer_for_2D_soccer_Simulation_English) 

[یوتیوب](https://www.youtube.com/watch?v=mRuxg-xy7pY)

**مقاله**

در صورتی که این نرم افزار را مفید ارزیابی می کنید لطفا در صورت استفاده از این نرم افزار در پروژه خود، در قسمت ارجاعات (References) مقاله خود به مقالات زیر ارجاع دهید

Namira Soccer 2 D Simulation Team Description Paper 2018. [PDF](https://archive.robocup.info/Soccer/Simulation/2D/TDPs/RoboCup/2018/Namira_SS2D_RC2018_TDP.pdf)

Persian Gulf Soccer 2D Simulation Team Description Paper 2017. In The 21th annual RoboCup International Symposium, Japan, Nagoya. [PDF](https://www.robocup2017.org/file/symposium/soccer_sim_2D/TDP_PersianGulf.pdf)

**ارتباط با ما**

برای هر گونه سوال و پیشنهاد با ما ارتباط برقرار کنید یا در صفحه گیتهاب این نرم افزار یک issue باز کنید

[Farzin Negahbani](mailto:farzin.negahbani@gmail.com)

[Shahryar Bahmai](mailto:shahryarbahmeie@gmail.com)

[Ehsan Asali](mailto:ehsanasali@uga.edu)

