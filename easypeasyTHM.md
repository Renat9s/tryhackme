easy peasy CTF > tryhackm

 

أولًا نسوي سكان بحثًا عن اي بورت مفتوح : -> nmap -A ip
![1](https://github.com/Renat9s/tryhackme/assets/126417250/4bcc7a1c-5283-4530-8ae7-3c470583abb4)



هنا نلاحظ ان يوحد عندنا robots.txt لكن غير مسموح لنا ندخله! و نخليه على جنب و نبحث عن أشياء ثانية لعلها توصلنا له

الآن مرة اخرى للتأكد من اني غطيت جميع البورتات : -> nmap -Pn -p- <ip> —open
![2](https://github.com/Renat9s/tryhackme/assets/126417250/b56dd07d-b572-4fe3-a411-1192e31c5572)





ايضًا ابحث الآن عن هالبورتات تحديدًا > Aggressive scan
وجدت أن بورت 6498 يشتغل على SSH

نقطة جيّدة لنا  : )
الآن بما ان عندنا متفصح نبدأ نشيك عليه و على الـ source page
و ماظهر معنا شيء, ببدأ أسوي  brute force 

``` gobuster dir -u htttp://IP/  -w /usr/share/dirb/wordlists/common.txt```




![3](https://github.com/Renat9s/tryhackme/assets/126417250/8e0944ab-367d-44d1-ae52-0e1f7173ec89)

طلع معنا hidden و نشيك عليه 

وكذلك لايوجد شيء به, برجع اسوي مرة اخرى فحص لكن مع هالمسار  الجديد اللي طلع لنا 

``` gobuster dir -u htttp://IP/hidden -w /usr/share/dirb/wordlists/common.txt ```



![4](https://github.com/Renat9s/tryhackme/assets/126417250/7a1938b4-1223-40f1-906e-6177e086053f)

و هنا يطلع شيء جديد نروح نشيّك عليه
و هذا اللي طلع لي له فايدة بالـ source page


![vmware_qyTD7wKAwd](https://github.com/Renat9s/tryhackme/assets/126417250/5f158d3c-af5f-4172-b2d7-5d22c59c73f1)

مشفر بالـ base64 

بعد البحث تم الإكتشاف و لله الحمد, فكوه و إكتشفوا : )

بما إن اسم الصفحة  dead end فأتوقع كذا كفاية
 برجع اشيك على البورتات المفتوحة واللي موجود عندي بورت على SSH

و البورت الثاني http > server apache

![5](https://github.com/Renat9s/tryhackme/assets/126417250/f877ebb1-41ed-4949-bac2-2eaeffd3efc3)

تقدرون تبحثون عن الفلاق بهالصفحة

 و شيكت على السورس بيج و طلع معي هالشيء و مبين انه مشفر ولازم نفك تشفيره عشان نفهم وش مكتوب

![6](https://github.com/Renat9s/tryhackme/assets/126417250/6f941264-6aa3-44d3-ae6a-46935e85e26c)

و استخدمت موقع [https://www.dcode.fr/en](dcode)

بعد ما فكيت التشفير طلع معي انه مسار جديد 

![juUt7EUeCD](https://github.com/Renat9s/tryhackme/assets/126417250/da765367-5e07-4722-9726-3bf46582294c)

دخلت عالمسار بهالشكل

هنا لاحظت به كلام بلون غير واضح و برضو صورة فكرت استخرج المعلومات منها لعلي القى شيء و بالنهاية بجرب كل شيء .

دخلت السورس بيج و نسخت الكلام و جربت افكه بأكثر من موقع 

![vmware_fbdKtOXaEI](https://github.com/Renat9s/tryhackme/assets/126417250/64aa2ee8-7026-4863-9b5a-8d5939d17e9c)

 “و طلع معي كلام يبين انه كلمة سر ليوزر معيّن “

و بعد ما حملت الصورة سويت كالتالي :

![يب](https://github.com/Renat9s/tryhackme/assets/126417250/be555899-a580-4655-815b-01a77c55cdd2)

طلع معي هالملف بعد ماستخرجت المعلومات من الصورة و الرمز اللي طلعته من فك التشفير اللي لقيته بالسورس كود كان رمز للملف المخفي اللي قاعدة احاول استخرجه ,

^ محتوى الملف اللي استخرجته من الصورة

مكتوب بالـ باينري بعد فكه من موقع CyberChef 

قدرت اعرف الرمز و سجلت دخول عن طريق ssh

====

لكن برضو هذا اكتشفته لان بالبداية كان غير مسموح لنا الإطلاع عليه

![vmware_XGe0VBnqTt](https://github.com/Renat9s/tryhackme/assets/126417250/738aad5e-e075-43cb-8b7e-931ff19a49b6)

نلاحظ ان يوجد به قيمة للـ user agent 

نسوي crack له و نشوف وش يطلع معنا و جربت هالموقع

[Hash, hashing, and encryption toolkit](https://md5hashing.net/)

و يطلع لنا فلاق بعد الفك .

---

بعد ما دخلنا على المشين من ssh 

بحثنا شوي و طلع معي اليوزر فلاق 

لكن تم تشفيره برضو 

![vmware_NLOX8MW6wL](https://github.com/Renat9s/tryhackme/assets/126417250/8ff1443a-58c2-4d20-a058-c956feafccc9)

عطانا تلميح سريع

rotated or something!

معناته نجرب rot13 

و فعلاً طلع معي على طول و خلصنا منه و نجي عند الروت فلاق

كيف اجيبه ؟ لازم ارفع صلاحياتي عشان اقدر اجيبه,

عانيت قليلًا من التعليق بالـ المشين اللي داخله عليه و اضطريت اسويه داخل الموقع نفسه

وكذا كانت طريقتي برفع صلاحياتي

![11](https://github.com/Renat9s/tryhackme/assets/126417250/ec85ca84-d732-4575-8685-4b592ba4a124)

و قدرت اجيب الروت فلاق و تم بنجاح

happy hacking < 3
