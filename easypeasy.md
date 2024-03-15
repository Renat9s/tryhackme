easy peasy CTF > tryhackm

 

أولًا نسوي سكان بحثًا عن اي بورت مفتوح : -> <nmap -A <ip> 
![1](https://github.com/Renat9s/tryhackme/assets/126417250/cb469e12-3cc5-4079-8823-f8631aceebeb)



هنا نلاحظ ان يوحد عندنا robots.txt لكن غير مسموح لنا ندخله! و نخليه على جنب و نبحث عن أشياء ثانية لعلها توصلنا له


الآن مرة اخرى للتأكد من اني غطيت جميع البورتات : -> nmap -Pn -p- <ip> —open



![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/bfd953cb-7df2-4f28-acb1-4cbe4b7aed1e/Untitled.png)

ايضًا ابحث الآن عن هالبورتات تحديدًا > Aggressive scan
وجدت أن بورت 6498 يشتغل على SSH

نقطة جيّدة لنا  : )
الآن بما ان عندنا متفصح نبدأ نشيك عليه و على الـ source page
و ماظهر معنا شيء, ببدأ أسوي  brute force  ``` gobuster dir -u htttp://IP/  -w /usr/share/dirb/wordlists/common.txt```



![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/2de474c5-5e78-4ef3-8f4d-44143315265d/Untitled.png)

طلع معنا hidden و نشيك عليه 

وكذلك لايوجد شيء به, برجع اسوي مرة اخرى فحص لكن مع هالمسار  الجديد اللي طلع لنا ``` gobuster dir -u htttp://IP/hidden -w /usr/share/dirb/wordlists/common.txt ```


![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/5769aad3-ffb1-483d-a64d-645f21400c11/Untitled.png)

و هنا يطلع شيء جديد نروح نشيّك عليه
و هذا اللي طلع لي له فايدة بالـ source page


![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/db94756e-d977-415d-bc54-8bb7c60db5e9/Untitled.png)

مشفر بالـ base64 

بعد البحث تم الإكتشاف و لله الحمد, فكوه و إكتشفوا : )

بما إن اسم الصفحة  dead end فأتوقع كذا كفاية
 برجع اشيك على البورتات المفتوحة واللي موجود عندي بورت على SSH

و البورت الثاني http > server apache

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/9c19f802-b617-4779-8a0a-b781b9d227a7/Untitled.png)

تقدرون تبحثون عن الفلاق بهالصفحة

 و شيكت على السورس بيج و طلع معي هالشيء و مبين انه مشفر ولازم نفك تشفيره عشان نفهم وش مكتوب

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/fc59d450-d1db-4155-877c-a25a205cd78a/Untitled.png)

و استخدمت موقع [https://www.dcode.fr/en](dcode)

بعد ما فكيت التشفير طلع معي انه مسار جديد 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/2efb8bb0-3ac0-477a-997a-ecef6b8fc13a/Untitled.jpeg)

دخلت عالمسار بهالشكل

هنا لاحظت به كلام بلون غير واضح و برضو صورة فكرت استخرج المعلومات منها لعلي القى شيء و بالنهاية بجرب كل شيء .

دخلت السورس بيج و نسخت الكلام و جربت افكه بأكثر من موقع 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/aca55cf5-a116-4c3b-a3fa-eea184eb6111/Untitled.png)

 “و طلع معي كلام يبين انه كلمة سر ليوزر معيّن “

و بعد ما حملت الصورة سويت كالتالي :

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/ee6cb0a1-439d-4905-b7a5-2e8ac27b82ae/Untitled.png)

طلع معي هالملف بعد ماستخرجت المعلومات من الصورة و الرمز اللي طلعته من فك التشفير اللي لقيته بالسورس كود كان رمز للملف المخفي اللي قاعدة احاول استخرجه ,

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/99b2cdbe-48e7-492b-aa6d-9c5938e3a926/Untitled.png)

^ محتوى الملف اللي استخرجته من الصورة

مكتوب بالـ باينري بعد فكه من موقع CyberChef 

قدرت اعرف الرمز و سجلت دخول عن طريق ssh

====

لكن برضو هذا اكتشفته لان بالبداية كان غير مسموح لنا الإطلاع عليه

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/18e6b67a-67bf-44f9-b92c-0e386b56417d/Untitled.png)

نلاحظ ان يوجد به قيمة للـ user agent 

نسوي crack له و نشوف وش يطلع معنا و جربت هالموقع

[Hash, hashing, and encryption toolkit](https://md5hashing.net/)

و يطلع لنا فلاق بعد الفك .

---

بعد ما دخلنا على المشين من ssh 

بحثنا شوي و طلع معي اليوزر فلاق 

لكن تم تشفيره برضو 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/349110bd-1326-4911-a513-6e3517041dee/Untitled.png)

عطانا تلميح سريع

rotated or something!

معناته نجرب rot13 

و فعلاً طلع معي على طول و خلصنا منه و نجي عند الروت فلاق

كيف اجيبه ؟ لازم ارفع صلاحياتي عشان اقدر اجيبه,

عانيت قليلًا من التعليق بالـ المشين اللي داخله عليه و اضطريت اسويه داخل الموقع نفسه

وكذا كانت طريقتي برفع صلاحياتي

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6a76636a-3b7d-4f44-acf5-41050d2e3986/6d937212-1acc-4475-bca2-2beb9dd42a83/Untitled.png)

و قدرت اجيب الروت فلاق و تم بنجاح

happy hacking < 3
