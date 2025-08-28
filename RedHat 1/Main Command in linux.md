**Day 1**
 -  pwd
to retrieve the current location.

 - mkdir dir1"
علشان اعمل ديريكتورى جديد


- mkdir   -p   d10/d9
-p علشان لو ملقاش الديريكتورى يعملو هو

- rmdir   d9 
علشان امسح ديريكتورى

-  mkdir {1.. 100}
- عشان اعمل 100 مره وحده

- touch  file 
- بعمل file جديد

- nano file 
- علشان افتحه و اعدل فيه

- cat file 
- اظهر الكلام الموجود فى الfile

- rm -r  dir1 
- علشان امسح dir حتى لو جواه حاجه 

- mv     newfile1     dir1/mvfile
علشان انقل الداتا و اغير اسم file

- cp  
- اعمل كوبى


- 

```bash
ls -l
```


```bash

```


#Day_3_RedHat
max days (password)   >  password will be expired
min days (password)   > user cannot change the password before
inactivity   >  no.  of days  user can login usering the password after password expiration warning days

```bash
chage -M 30  -I 2  -m 3  -W 2  -E 2025-10-14 user2
```
"M" max days 
"m" min days
"W"   warndays WARN_DAYS
"I"  -inactive INACTIVE
 
### 🔐 أولاً: التشفير (Encryption)

- **الهدف**: حماية سرية البيانات ومنع أي شخص غير مصرح له من قراءتها.
    
- **هل يمكن عكسه؟** ✅ نعم، يمكن **فك التشفير** باستخدام مفتاح.
    
- **الاستخدام**: عند إرسال بيانات حساسة مثل رسائل البريد الإلكتروني أو عند تصفح الإنترنت (HTTPS).
    
- **أمثلة**: AES – RSA – DES
    
- **كيف يعمل؟**  
    تشفير(النص، مفتاح) → بيانات مشفرة  
    فك التشفير(البيانات المشفرة، نفس المفتاح) → النص الأصلي
    

---

### 🔒 ثانياً: الهاش (Hashing)

- **الهدف**: التأكد من **سلامة البيانات** أو تخزين كلمات المرور بطريقة آمنة.
    
- **هل يمكن عكسه؟** ❌ لا، هو **اتجاه واحد فقط**.
    
- **الاستخدام**: تخزين كلمات المرور، التحقق من الملفات، التوقيعات الرقمية.
    
- **أمثلة**: SHA-256 – MD5 – SHA-1
    
- **كيف يعمل؟**  
    هاش(البيانات) → سلسلة ثابتة من الأحرف  
    أي تغيير صغير في البيانات = نتيجة مختلفة تمامًا
    

---

### 📦 ثالثاً: الترميز (Encoding)

- **الهدف**: تحويل البيانات لصيغة مناسبة للنقل أو التخزين، وليس للحماية.
    
- **هل يمكن عكسه؟** ✅ نعم، **سهل الفك**.
    
- **الاستخدام**: نقل البيانات عبر الإنترنت، مثل تحويل الصور لنص Base64.
    
- **أمثلة**: Base64 – ASCII – UTF-8 – ترميز الروابط (URL Encoding)
    
- **كيف يعمل؟**  
    ترميز(البيانات) → شكل مختلف  
    فك الترميز(الشكل) → البيانات الأصلية
    

---

### 🔁 جدول المقارنة السريع:

|الميزة|**التشفير**|**الهاش**|**الترميز**|
|---|---|---|---|
|**الهدف**|الحفاظ على السرية|التحقق وسلامة البيانات|تسهيل النقل/التخزين|
|**يمكن عكسه؟**|نعم (بالمفتاح)|لا|نعم|
|**هل يستخدم مفتاح؟**|نعم|لا|لا|
|**أمثلة**|AES، RSA|SHA-256، MD5|Base64، UTF-8|
|**يُستخدم في؟**|حماية البيانات|كلمات المرور، التحقق|إرسال البيانات عبر الشبكة|


```bash
nano /etc/sudoers
visudo
```

cmnd_Alies  GROUPMANG =/sbin/useradd  , /sbin/userdel ,  



#Day_5

Symbolic  :
chmod 

owner > u
group > g
other >  o

Read > r
write > w
execute > x


Numeric permissions  :

rad = 4
write = 2
execute = 1




لتجربت البيرمشن

```bash
umask 621
```

def (dir )  621  >  777 - 621  = 156   d --x r-x rw-
156 -xxx = 046   - --- r-- rw-

```bash
mkdir dir4 ; touch file4
ls -ld dir4 file4
```



```bash
chown zeko:shanggroup   
```
shared directory problems :
1 - files are not shard by defolte



