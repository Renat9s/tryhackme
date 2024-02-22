# [Brooklyn Nine Nine](https://tryhackme.com/room/brooklynninenine)

كالعادة نبدأ نفحص عن طريق nmap 
![image](https://github.com/Renat9s/tryhackme/assets/126417250/f187e4e8-ca3e-4ee1-85ff-e695657a7ebb)


و أرجع أشيك على الموقع و أشوف الـ page source 

وهنا به شيء شدني! نرجع له شويات 

![image](https://github.com/Renat9s/tryhackme/assets/126417250/0073cc53-c266-431a-b693-aa5b946d1941)


نرجع لبورت ftp بما إننا نقدر نسجل دخول عن طريق anonymous بدون كلمة سر

بعد ما دخلت أول شيء اشوفه الملف هذا 

![image](https://github.com/Renat9s/tryhackme/assets/126417250/2d7a2a12-4d50-4a0d-a3c3-347d12d7e00c)

يالله نحمله : get file


نطلع و نرجع للمشين حقنا و نقراه
![image](https://github.com/Renat9s/tryhackme/assets/126417250/0e3fb0f2-c4a3-446b-88fc-48401f8381eb)


حلو عرفنا ان به يوزر اسمه : jake & amy

ببدأ أسوي brute-force على الأول لأن مبين سهل تخمينه و لو ما نفع نشوف الثاني.

![image](https://github.com/Renat9s/tryhackme/assets/126417250/9edb25ef-c7f4-41ab-b48a-b6a71d32f687)

* و بكذا جبناه  وندخل عن طريق ssh
* نلقى بالـ home اليوزر فلاق

نحل أول سؤال  ونجي على موضوع الـ root

* التحدي به طريقتين إننا نرفع الصلاحيات و نوصل للروت

* حفظت الصورة من الموقع بما إنه طرى لنا Steganography
* قلت أستحدم هالأداة : [Stegcracker](https://github.com/Paradoxis/StegCracker) 
 


وهي للـ brute-force تستخرج الـ hidden data

استخدمتها لـ الصورة اللي حفظته وهذا طلع معي 
![image](https://github.com/Renat9s/tryhackme/assets/126417250/b6500eb4-20db-48d8-a23d-d0852f09e3ce)


ندخل بـ holt
عن طريق ssh

بعد ما نفر 
نشيّك على صلاحيات السودو : sudo -l 
ونلاحظ إن : ``` user holt may run the following commands on brookly_nine_nine : (all) NOPASSWD: /bin/nano ```

نقدر نستخدم سودو بالـ نانو كوماند بدون كلمة سر!

بحثت بهالموقع [GTFOBins](https://gtfobins.github.io) عن الكلام أكثر 
![image](https://github.com/Renat9s/tryhackme/assets/126417250/ad9cf315-0076-43f1-a498-9cc1b9af5a14)


بكذا سويت طريقة باليوزر holt

و طريقة أخرى عطوها فرصة وأبحثوا أكثر : )
happy hacking < 3 
