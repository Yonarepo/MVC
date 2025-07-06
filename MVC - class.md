> ### جلسه اول: **آشنایی با Controller و ایجاد View**

1. **باز کردن قسمت Controller**

2. **ایجاد یک Controller با نام Home**

3. **استفاده از  ActionResualt ها برای عملیات مختلف**
    - نام اولین اکشن باید *`Index`* باشد.

4. **کلیک راست درون ActionResualt مورد نظر**

5. **انتخاب گزینه Add View**

6. **ایجاد در حالت empty(without model)**
---
> > #### متغیر های مشترک بین کنترلر و ویو
##### ‌• ایجاد viewbag
`متغیر یکبار مصرف که بعد از نمایش از بین میره.`
###### `ایجاد در controler: `
```c#
ViewBag.name = "مقدار";
```
###### `استفاده در view:`
```d
@ViewBag.name
```
‌
##### • ایجاد session 
`متغیر غیرموقت که تا زمان بسته نشدن مرورگر معتبره.`
###### `ایجاد در controler:`
```sh
session["نام‌متغیر"] = "مقدار";
```
```sh
session.Add("نام‌متغیر", "مقدار")
```
###### `استفاده در view:`
```d
@session["نام متغیر"]
```
---

---
> > #### ایجاد صفحات جدید و جابجایی بین صفحات


##### • ایجاد صفحه جدید 
1. ‌اضافه‌کردن `ActionResault` جدید با نام مشخص در فایل `controler`
2. ایجاد یک ویو سفارشی (کلیک راست در خطوط `ActionResault` و `add view` یا ایجاد یک فایل `view` همنام با `ActionResault` جدید)
##### • جابجایی بین صفحات و فراخوانی صفحه‌ها با لینک درون‌صفحه‌ای
```html
<!-- view -->
 @Html.ActionLink("نام ویو", "متن")
 ```

---

---

>> #### : **نصب Entity Framework**
###### • برای کار با پایگاه داده و توابع مربوط به ذخیره داده‌ها، از **Entity Framework** استفاده میکنیم.
###### • نصب فریم ورک
   • نوار بالایی
   `Tools` →‌ `NuGet Package Manager` → `Manage NuGet Packages for Solution`
• جستجوی عبارت "`Entity Framework`" در تب `Browse`.
• انتخاب `Entity Framework`.
• انتخاب پروژه مورد نظر و کلیک روی `Install`.

- #### ایجاد یک مدل در پروژه
1. **`رفتن به پوشه Models.`**
2. **`کلیک راست، گزینه Add`**
3. **`انتخاب گزینه New Item.`**
4. ** `ایجاد فایل مدل با نام model-name.cs (از "class.cs" استفاده نشه بهتره.`**

---
>> #### کار با مدل پروژه

###### `فایل مدل یک سری فیلد داره که با هربار ارسال داده به دیتابیس، فیلد هایی که با هم ارسال میشن رو در قالب یک رکورد (یک ردیف) به جدول اطلاعات دیتابیس می‌فرسته و اونجا ذخیره می‌کنه.`
###### 1. ایجاد یک فایل cs. در پوشه Models
###### 2. حالا فیلد هارو اضافه می‌کنیم:
```c#
//ساختار کلی فیلد
public [DataType] [name] {..;..}

//مثال
[key]
Public int x {get; set;}
Public int Id {get; set;}
Public string Names {get;set;}
Public string Emails {get;set;}
```
• مدل بالا با هربار ارسال داده ردیفی به شکل زیر در جدول دیتابیس اضافه می‌کنه:

| Model | `Id` | `Names` | `Emails` |
| ----- | ---- | ------- | -------- |
| ‌     | ‌    | ‌       | ‌        |

==در بالای اولین فیلد باید عبارت [Key] رو بذاریم. این فیلد معمولا کلید رکوردهاست که خودکار مقداردهی میشه و اگه تکراری باشه خطا میگیریم. پس بهتره فیلدی که قراره کاربر بهشون مقدار بده رو به عنوان کلید انتخاب نکنیم.==
• `تنظیم get`: `دیتای قابل فراخوانی از سمت کاربر`
• `تنظیم set`: `دیتای قابل تنظیم از سمت کاربر`

---

> > #### فرم های ارسال داده در view 

فرم‌ها راهی برای ارسال داده ها به مدل هستن.
###### `با استفاده از قطعه زیر، داده وارد شده در فرم توسط متغیر x به فیلد Id در مدل ارسال میشه.`
```html
(x=>x.Id)
```
> ##### • ایجاد فرم 
```d
@using (@Html.BeginForm())
{
‌
}
```
##### • ساختار عناصر داخل فرم
 `لیبل:`
```html
<label> "text" </label> 
```
`تکست‌باکس:`
```html
@html.TextBoxFor(x=>x.Id)
```
`دکمه‌ها:`
```html
<input type="submit" value="text">

```

##### • ساختار نهایی فرم ثبت‌نام:
```html
{
<label>ID: </label> @html.TextBoxFor(x=> x.Id)

<label>Name: </label> @html.TextBoxFor(x=> x.Names)

<label>Email:: </label> @html.TextBoxFor(x=> x.Emais)

<input type="submit" value="Ok">
}
```
```d
ID:    [        ]
Name:  [        ]
Email: [        ]
```
###### `در فرم بالا مقادیر تکست‌باکس‌ها به فیلد های Id  Names و Emails ارسال شده و یک دکمه با عبارت Ok هنگام کلیک شدن مقادیر فرم رو از view به ActionResault مربوطه ارسال میکنه.`
‌

> ##### • استفاده از مقادیر فرم

یک ActionResault همنام با فعلی می‌سازیم و به شکل زیر تغییرشون می‌دیم:
در اکشنی که از نوع postعه به شکل زیر فرم دیتا و اسم مدل رو فراخوانی میکنیم؛ حالا مقادیر ارسال شده از سمت فرم در این اکشن قابل استفاده است.
```c#
//
[HttpGet] 
Public ActionResult mypage1()
{
}
//
[HttpPost]
Public ActionResult mypage1(model formdata)
{
//برای مثال اونو توی یک سشن میریزیم:
Session[Id] = formdata.Id;
}
```
---
---
>> #### فراخوانی صفحه‌ها بعد از کلیک روی دکمه

در بین کد های ActionResault کنترلر مربوط به هر ویو عبارت`()return view` دیده میشه که موقع زدن روی دکمه Ok این خط کد مقادیر تولید شده اون ویو رو صادر میکنه.
==در داخل پرانتز این خط ، اسم هر ویویی رو که بذاریم بعد از زدن روی Ok به اون صفحه منتقل میشیم==.
برای مثال:
```c#
return view("home")
```
`بعد از کلیک به‌صورت خودکار مارو به صفحه‌ای با نام home منتقل میکنه.`

==بهتره بجای این از== 
```
return RedirectToAction ()
```
==استفاده کنیم. در این صورت از ارسال درخواست ها و مقادیر تکراری توسط فرم و خطای زمان اجرا جلوگیری میشه.==
نکته: در استفاده از این مورد ، نمیشه از ویوبگ ها استفاده کرد. چون در این حالت کل اکشن به صورت کامل فراخوانی میشه و مقدار ویوبگ میسوزه. بهتره از session استفاده کنیم.

---
---

>> #### آماده‌سازی مدل اتصال به دیتابیس اصلی

حالا تمام مدل های پروژه در یک مدل نهایی جمع میشه تا یکجا به دیتابیس فرستاده بشه.

##### • ابتدا ایجاد یک فایل مدل جدید 
`اصولا بهتره در نام این مدل از db استفاده کنیم تا از بقیه متمایز و راحت تشخیص داده بشه. ما نام فرضی dbmodel رو انتخاب میکنیم`
##### • اضافه کردن موارد زیر به namespace 
```csharp
using System.data.Entity;
using System.ComponentModel. Dataannotation;
using System.ComponentModel. Dataannotation.schema;
//جایگزین کردن نام پروژه شخصی
using project-name.Models;
```
##### • تبدیل مدل به dbContext(نوع مدل ارسال کننده) با تغییر خط زیر
```csharp
Public class dbmodel
↓
Public class dbmodel : dBcountext 
```
##### ‌•  اضافه کردن تک‌تک مدلها برای ارسال
```C#
//در پرانتز نام مدل و بعد از اون یه نام فرضی و مستعار برای مدل در دیتابیس
Public Dbset < model1 > name_model1 {get; set;}

Public Dbset < model2 > name_model2 {get; set;}
```
###### `با استفاده از Dbset ابتدا نام مدل و سپس یک نام برای ثبت‌شدن در دیتابیس انتخاب میشه.`
`برای مثال از حالا به بعد مدلی با نام model2 با عنوان name_modle2 در دیتابیس شناخته میشه`

---
>> #### اتصال مدل به دیتابیس 

###### • ایجاد یک دیتابیس محلی:
 1- نصب SQL server و ایجاد سرور محلی
 
2- نصب SSMS و اتصال به سرور محلی

###### • اتصال به دیتابیس:
 بعد از ساخت مدلها و اضافه کردن اونا به مدل نهایی
با رفتن به بخش `tools` ، باز کردن `nugget Console` و زدن دستور زیر مهاجرت رو فعال میکنیم:
```d
Enable-Migrations
```
با دستور زیر یک فایل مهاجرت ایجاد میشه:
`یک اسم انتخابی از ما میخواد`
```d
Add-Migration
```
و با دستور زیر اتصال کامل میشه:
```d
Update-Database
```
`حالا در جلسات بعدی هر داده ارسالی از طرف فرم رو میشه در دیتابیس اصلی ذخیره کرد.`

---

> >#### ذخیره یک داده واقعی و ساخت فرم ثبت نام 

##### • ابتدا ایجاد متغیر سراسری 
`در مثال زیر عبارت "db" به نمایندگی از اجتماع مدل های پروژه یا همون dbmodel با داده های ارسالی در کنترلر کار می‌کنه.`
```c#
private [dbmodel] [name] = new [dbmodel]();
//مثال
private dbmodel db = new dbmodel();
```

###### •اکشن زیر که یک فرم در ویوی خودش داشت و مقادیر فرم رو دریافت میکرد به کمک قطعه زیر هر داده ارسال شده رو به عنوان یک رکورد در دیتابیس ثبت و ذخیره می‌کنه:
```c#
//
[HttpPost]
Public ActionResult mypage1(model formdata)
{
//////////////ثبت یک رکورد توسط فرم 
db.name_model.Add(formdata);
db.Savechanges();
//////////////
}

```
`در اینجا db به نمایندگی از مدل جمع‌کننده حضور داره و داده رو دریافت می‌کنه؛ همچنین بعد از db به name_model اشاره کردیم که نام‌مستعار مدلی با نام model1 در دیتابیس بود تا داده ها به این مدل ارسال بشن.`

##### • کد نهایی اکشن ثبت نام:
```c#
//متغیر سراسری از نوع dbmodel
private dbmodel db = new dbmodel();

[HttpGet]
public ActionResult register()
   {
   return View();
   }
   
[HttpPost]
//فرم‌دیتا و مدل رو داخل این اکشن صدا زدیم
public ActionResult register (model formdata)
   {
   
//ذخیره داده‌ها
db.name_model.Add(formdata);
db.Savechanges();

//انتقال به یک ویو دیگه با نام ایندکس بعد از کلیک روی دکمه
return RedirectToAction ("Index);
}
```
`به کمک RedirectToAction ، بعد از ثبت، به صفحه اول برگشته و ویو-کنترلر مجدداً بارگذاری میشن تا از ارسال درخواست تکراری و خطای زمان اجرا جلوگیری بشه.`

---
---
>> #### جستجو در دیتابیس 
>> `کاربران رو بر اساس Id جستجو میکنیم.`

##### • در قطعه زیر ابتدا یک متغیر از نوع مدلی که قصد جستجو در اون رو داریم می‌سازیم. 
در نهایت قسمت`u=>u.Id == Id`بررسی میکنه که مقدار Id که از سمت فرم اومده با مقدار Id خاصی در داخل دیتابیس یکی هست یا نه. اگر بود تمام اون رکورد رو (شامل Name Id Email) در متغیر میریزه.
```c#
[model] [نام انتخابی] = db.name_model.FirstorDefault(u=> u.Id==Id);
```
‌
‌
```c#
[HttpPost]
public ActionResult search(int Id)
{

model1 user = db.name_model.FirstorDefault(u=> u.Id==Id);

//شرط که چیزی پیدا شده و متغیر مقدار گرفته باشه؛ یعنی خالی نباشه
   if(user != null)
 {

//مقادیر پیدا شده رو در ویوبگ می‌ریزیم واسه نمایش یا غیره
viewBag.Name=.user.Name viewBag.Lastname= user.Emails;

//در صورت پیدا شدن نتیجه
return view();

 }
   else
 {
session["find-status"] = "Not found";

//در صورت پیدا نشدن نتیجه بارگزاری مجدد همین اکشن فعلی رو انجام میده تا درخواست تکراری و خطا نداشته باشیم.
return RedirectToAction ("search");
 }
‌
 }
```
• `رکورد ها بر اساس یک فیلد خاص، مثلا Id جستجو میشن. کاربر یک Id رو برا جستجو می‌فرسته و در صورت مطابقت، تمام محتویات رکورد مربوط به اون Id فراخوانی و در متغیر ها ذخیره میشن.`

---
---
جلسه 
> ### حذف اطلاعات از دیتابیس

##### • در این قطعه مجددا متغیری از نوع مدل مورد نظر می‌سازیم و کل مقادیر یک رکورد رو بر حسب یک فیلد در اون می‌ریزیم.
```c#
model < name > = db.name_model.FirstorDefault(u=> u.Id==Id);
//ما اینجا از فیلد آیدی برای جستجو استفاده کردیم. میشه از هر فیلدی مثل یوزرنیم ایمیل و غیره هم استفاده کرد‌.
```
##### • همچنان در صورت خالی نبودن و مقدار گرفتن متغیر(پیدا شدن رکورد در دیتابیس):
```C#
   if (< name > != null)
   {
//رکورد با محتوای پیدا شده از دیتابیس حذف و تغییرات ثبت میشه.
db.name_model.Remove(< name >);
db.Savechanges();
//ایجاد پیام موفقیت 
session["delet-status"] = "successful.";

//انتقال به صفحه اصلی بعد از اتمام حذف
return RedirectToAction("Index");
   }
   
   else
   {
   //پیام عدم موفقیت 
session["delet-status"] = "Not Found.";

//بارگزاری دوباره ویو و جلوگیری از درخواست مجدد
return RedirectToAction("delete");
   }


}
```
•`به کمک یک متغیر از نوع مدل و توسط فیلد Id، تمام محتوای رکورد پیدا شده در این متغیر ریخته میشه.`
• `به علت استفاده از RedirectToAction سشن های گزارش‌دهنده وضعیت فرصت نمایش تو این ویو رو ندارن؛ به همین علت بعد از حذف و انتقال خودکار، پیام وضعیت رو در صفحه ای که بهش منتقل شدیم نمایش می‌دیم. مثلا در اینجا Index.`

---
---

>> ##### استفاده از سایر اکشن ها در ویو( اکشن هایی بجز اکشن خود ویو)


‌
#### • ارسال فرم به سایر اکشن ها 
 • `برای مثال یک فرم در صفحه اصلی که درخواستی به  اکشن جستجو میفرسته و کد اون اکشن اجرا میشه بدون اینکه لازم باشه به صفحه جستجو بریم`
```cs
‌@using (Html.BeginForm("actio-name", "controller-name", FormMethod.Post/Get))
{
//نوشتن ادامه عناصر فرم
}
```


##### • دکمه 
`با کلیک روی این دکمه اکشن موردنظر شروع به اجرا می‌کنه. برای مثال یک اکشن تولید مقادیر تصادفی، رمزنگاری و غیره کار خودشو انجام میده و مقدارش رو میفرسته بدون اینکه لازم باشه به صفحه ویو مربوط به اون اکشن بریم.`
```html
<h2>صفحه داشبورد</h2>
<!-- دکمه  -->
<!-- وارد‌میشه action-name نام‌اکشن در -->
<form action="@Url.Action("action-name")" method="post">
    <button type="submit"> Ok </button>
</form>
```
---
---
---
>> #### سیستم LogIn و LogOut
> ##### لاگین موقت و یکبار مصرف

‌
##### ‌• مدل و فیلد های مورد نیاز
```c#
public class users
{
    [key]
    public int Id { get; set; }
    public string name { get; set; }
    public string username { get; set; }
    public string password { get; set; }
}
```

---
> ### لاگین 
##### • ‌‌ویو و صفحه لاگین 
```html
@model YourProject.Models.users

@using (Html.BeginForm())
{
    <label>Name: </label>
    @Html.TextBoxFor(x => x.name)
    
    <label>Username: </label>
    @Html.(x => x.Username)
    
    <label>Password: </label>
    @Html.(x => x.password)
    
    <input type="submit" value="Login" />
}
```
##### • کنترلر لاگین
```c#
var "name" =
db.name_model.FirstOrDefault(x => x.username == formData.Username && x.password == formData.Password);
```
• `این یک شرط لامبداعه که دو عمل مختلف رو انجام میده؛ اول بررسی می‌کنه آیا دو داده ارسال شده از سمت formdata همزمان با مقادیر دو فیلد خاصی از دیتابیس مطابقت دارن یا نه. در صورت تطابقِ هر دو، این مقادیر رو در یک متغیر ذخیره می‌کنه.`
‌
```c#
if ("name" != null)
    {
        Session["LogIn-status"] = "true" ;
        return RedirectToAction("Index", "Home");
    }
```
- ‌`مقدارگیریِ متغیر رو بررسی می‌کنیم(تایید شرط لامبدا و مطابقت رمز) و در صورت تأیید  یک سشن رو به عنوان کلیدِ اعتبارسنجی مقداردهی می‌کنیم.`
‌
##### • اعتبار سنجی‌
 ==حالا در هر اکشنی که دیدن محتوای ویوش به لاگین نیاز داره با یک شرط مقدار سشن رو چک میکنیم. اگه خالی بود(لاگین نبود یا از بین رفته بود) اونو به کمک `RedirectToAction` به صفحه لاگین می‌فرستیم تا لاگین کنه بیاد:==
```c#
public ActionResult home()
{
\
//چک کردن کلید لاگین
    if (Session["LogIn-status"] == null)
    {
        return RedirectToAction("Login");
    }

//ادامه کد ها
}
```
###### • میشه در ویو هم اعتبارسنجی کرد(توصیه نمیشه)
```d
@if (Session["LogIn-status"] != null)
{
    <p>Welcome, @Session["LogIn-status"]</p>
}

else
{
    @Html.ActionLink("Login", "Login")
}
```

---

> ### لاگ‌اوت
##### • کنترلر لاگ‌اوت 
`یک کنترلر مجزا مقادیر session رو از بین میبره`

==میشه از روش دکمه هایی که سایر اکشن هارو صدا میزنن استفاده کرد تا تنها با زدن یک دکمه ، این اکشن کلید رو از بین ببره==
```c#
public ActionResult Logout()
{
    Session.Clear();
    return view ("Index");
}
```
---
ساختار کامل یک سیستم لاگین-لاگ‌اوت
```c#
private dbmodel db = new dbmodel();

[HttpGet]
public ActionResult login()
{
    return View();
}

//ورود
[HttpPost]
public ActionResult Login(User  formData)
{
//شرط بررسی کننده‌ی یوزر و پسورد
    var name =
db.name_model.FirstOrDefault(x => x.username == formData.Username && x.password == formData.Password);

    if (user != null)
    {
//اینجا به کلید مقدار نام‌کاربری شخص رو دادیم تا بعداً کنار پروفایل نمایش بدیم؛ اختیاری و طبق کاربرد
        Session["user"] = user.Name;
   return RedirectToAction("home");
    }
    
    else
    {
    //کاربر پیدا نشد و بارگزاری مجدد صفحه 
        ViewBag.Error = "Invalid email or password.";
  return RedirectToAction("login");
    }

//خروج
public ActionResult logout()
{
    Session.Clear();
    return RedirectToAction("Index");
}
}
```

---
---
>> #### سیستم `Login-LogOut` ==دائمی== با `cookie`


##### • کنترلر لاگین

```c#
var user =
db.name_model.FirstOrDefault(x => x.username == formData.Username && x.password == formData.Password);
```
##### • اخبار سنجی‌ 
==اینبار بجای کلید سشن موقتی، یک کوکی در مرورگر کاربر ذخیره میکنیم که یکبار مصرف نیست==
```c#
if (user != null)
    {
HttpCookie cookie = new HttpCookie("user", loginuser.username);

cookie.Expires = DateTime.Now.AddDays(5);

Response.Cookies.Add(cookie);
    }
```
• `در قسمت‌اول یک متغیر از نوع کوکی با نام 
user-login مقداردهی میشه.`
• `در بخش دوم مدت‌زمان منقضی شدن کوکی رو مشخص می‌کنیم - در غیر این صورت موقتیه.`
• `در بخش سوم کوکی رو همراه با مقدارش به مرورگر کاربر می‌فرستیم تا اونجا ذخیره بشه.`


##### • اعتبارسنجی 
```c#
if (Request.Cookies["user"] == null)
{
    return RedirectToAction("login");
}
return view();
```
•  ` تو هر اکشنی که دیدن محتواش لاگین لازم داره ، با یک شرط متغیر اعتبارسنجیِ ذخیره‌شده در مرورگر کاربر به عنوان کلید بررسی میشه تا ببینیم معتبره یا نه. اگه نبود به صفحه لاگین هدایت میشه تا نتونه به اون صحفه وارد بشه.`
‌
---
>> ##### کنترلر لاگ‌اوت
```c#
public ActionResult Logout()
{
HttpCookie user-login = new HttpCookie("user", loginuser.username);

    cookie.Expires = DateTime.Now.AddDays(-1);
    
    Response.Cookies.Add(cookie);

 return RedirectToAction("Index");
}
```
•`دستور مستقیمی برای حذف کوکی وجود نداره. پس دوباره همون کوکی با مدت‌زمان اعتبار منفی یک روز (دیروز) بروزرسانی می‌کنیم.`==مرورگر به طور خودکار کوکی‌های تاریخ گذشته رو حذف می‌کنه==`در نتیجه بعد از ارسال به مرورگر این کوکی از بین میره.`

##### • دکمه لاگ‌اوت در ویو 
```html
<h2>صفحه داشبورد</h2>
<!-- دکمه لاگ‌اوت -->
<form action="@Url.Action("logout")" method="post">
    <button type="submit">خروج از حساب</button>
</form>
```
`این دکمه در هر ویویی که باشه اکشن مربوط به لاگ‌اوت رو فراخوانی می‌کنه تا عملیات منقضی سازی کوکی رو انجام بده.`

---
---
---

>> #### استفاده از یک فرم برای انجام دو عمل مختلف


` ایجاد دو دکمه مختلف که هرکدوم مقادیر یک فرم رو به اکشن های مختلف می‌فرستن`

##### • ایجاد فرم با دو دکمه
```d html
@model YourNamespace.Models.students

//ایجاد فرم
@using (Html.BeginForm())
{
//یه تکست‌باکس فرضی
    @Html.TextBoxFor(x => x.username, new { placeholder = "Enter Username" })

    <button type="submit" name="actionType" value="search">Search</button>
    <button type="submit" name="actionType" value="delete">Delete</button>
}
```

‌
##### • کنترلر dashboard
`به این شکل میشه کنترلر حذف و جستجو رو یکی کرد:`
```c#
public ActionResualt search(int? Id, string actionType)
{
 if (actionType == "search")
 {
 //ادامه کدهای جستجو 
 return RedirectToAction("dashboard")
 }
‌
‌
 else if (actionType == "delete")
 {
 //ادامه کدهای حذف
 return RedirectToAction("dashboard")
 }
}
```
‌

• `نکته مهم`: `ممکنه به دلیل ساختار ویو ، بعد پیدا شدن Id ، دیگه مقداری به فرآیند delete نرسه.`
###### • برای حل این مشکل:
 داخل شرط `finder` بعد از اینکه مقدار Id جستجو شده null نبود یک session تعریف میکنیم:
```c#
//model1 student = db.tbl_model...
//if (student != null){

session["stdId"] = student.Id;
```
 سپس داخل شرط `delete` به این شکل از این مقادیر استفاده میکنیم:
```c#
//مقدار سشن رو به صورت عددی به یک متغیر می‌ریزیم.
int? studentId = Session[stdId] as int?;

//با همون رویه قبلی مقادیر ارسال شده از سمت فرم‌دیتا رو مطابقت میدیم.
model1 student = db.tbl_model.FirstOrDfault(x => x.Id == stdId)

//تطابق و حذف 
if (student!= null){
db.tbl_model.Remove(student);
db.SaveChange();
}
```
