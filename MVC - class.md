> ### جلسه اول: **آشنایی با Controller و ایجاد View**

1. **باز کردن قسمت Controller**

2. **ایجاد یک Controller با نام Home**

3. **استفاده از  ActionResualt ها برای عملیات مختلف**
    - نام اولین اکشن باید *`Index`* باشد.

4. **کلیک راست درون ActionResualt مورد نظر**

5. **انتخاب گزینه Add View**

6. **ایجاد در حالت empty(without model)**
---

> ### جلسه دوم: ** ساخت بازی سنگ کاغذ قیچی توسط کنترلر و نمایش بازی در view**

1. **ساخت کد Random ساز برای بازی سنگ کاغذ قیچی در ActionResult Index:**
   ```csharp
   Random num = new Random();
   int nums = num.Next(1, 4);
   if (nums == 1) {
       // ادامه کد
   }
   ```
   - `سورس مربوط به بازی و تولید متغیرهای آن عموماً باید در Index نوشته بشود. چون.`

2. **ساخت یک متغیر در Controller و استفاده در View متعلق به آن:**
   ```csharp
   ViewBag.< name > = "مقدار";
   ```
- `ویوبگ هر کنترلر فقط در ویو مربوط به خودش قابل استفادس و یبار مصرفه.`
‌
2. **استفاده از متغیر Controller در View:**
   ```html
   @ViewBag.< name >
   ```
   مثال:
   ```csharp
   if (nums == 1) {
       ViewBag.rand = "سنگ";
   }
   ```
`↓`
   ```html
   @ViewBag.rand
   ```

---

>#### توسعه بازی

---
> ### ایجاد صفحه های جدید و جابجایی بین ویو ها 

- یک ActionResualt با نام جدید ساخته و ویو مربوط به اونو ایجاد میکنیم.
با نوشتن عبارت زیر در view میشه یک لینک برای جابجایی بین view های مختلف ایجاد کرد:

```c#
 @Html.ActionLink("نام ویو", "متن")
 ```

---

> ### جلسه ششم: **استفاده از Session و متغیرهای سراسری**

`controller:`
   ```csharp
   session.Add("نام متغیر", "مقدار")
   ```
`or`
```c#
session[" name " ] = " value ";
```

- `برای استفاده در view:`
   ```csharp
   @session["نام متغیر]
   ```
- **`سشن ها در هر ویویی قابل استفاده هستن و تا مدت زیادی هم از بین نمیرن.`**
- `میشه از اونها برای نمایش نتایج بازی در سایر ویو ها استفاده کرد ولی نکته مهم اینه که ترتیب اجرای ویو ها مهمه و لازمه که سشن ها قبل اینکه صدا زده بشن از قبل تولید شده باشن؛ در نتیجه تو کنترلر هایی ایجاد میشن که اولویت اجرا دارن.`
---

> ### جلسه پنجم: **نصب Entity Framework**

برای کار با پایگاه داده و توابع مربوط به ذخیره داده‌ها، از **Entity Framework** استفاده میکنیم.

- #### Entity Framework
  - **EF6**: مناسب برای مدل‌های کلاسیک و ساده‌تر.
  - **Core**: مناسب برای مدل‌های پیشرفته‌تر.

- #### نصب فریم ورک
1. **رفتن به مسیر زیر:**
   - `Tools` → `NuGet Package Manager` → `Manage NuGet Packages for Solution`
1. جستجوی عبارت "`Entity Framework`" در تب `Browse`.
2. انتخاب `Entity Framework`.
3. انتخاب پروژه مورد نظر و کلیک روی `Install`.

- #### ایجاد یک مدل در پروژه
1. **`رفتن به پوشه Models.`**
2. **`کلیک راست، گزینه Add`**
3. **`انتخاب گزینه New Item.`**
4. ** `ایجاد فایل مدل با نام model-name.cs (از "class.cs" استفاده نشه بهتره.`**

---
> ### جلسه هفتم: **شروع کار با مدل

توی مدل یک سری فیلد تعریف میکنیم که در آینده هر کدوم از اینها یک ستون مشخص رو در جدول اصلی دیتابیس تشکیل میدن.
```c#
Public int Id {get; set;}
Public string Names {get;set;}
Public string Emails {get;set;}
```
`Table in Database↓`

|       | Id  | Names | Emails |
| ----- | --- | ----- | ------ |
| Value |     |       |        |
| Value |     |       |        |
- `تنظیم get`: `دیتای قابل فراخوانی از سمت کاربر`
- `تنظیم set`: `دیتای قابل تنظیم از سمت کاربر`

---

> ### جلسه هشتم: **ساخت صفحه لاگین و فرم‌های ورودی**

> **ایجاد فرم برای ساخت صفحه لاگین و گرفتن داده ها از کاربر در view**
- **`نکته`**: **`این ویو ها باید روی حالت empty و با انتخاب مدل ایجاد بشن.`**
‌
`بعد از ایجاد ویو`:
 1. `اول مدل رو در ویو فراخوانی می‌کنیم.` 
```html
@model < proj-name >.Models.< model-name >
```
2. `یک فرم برای ارسال داده ها توسط ویو ایجاد میکنیم.`
```html
@using (@Html.BeginForm())
{
}
```
- **` هر نوع دیتایی که توی فرم ثبت بشه با هم در یک بسته قرار میگیره.` **

> #### - ساختار عناصر داخل فرم

- **`تکست‌باکس:`**
```html
<label> "text" </label> @html.TextBoxFor(x => x."field in model")
```
مثال:
```html
<label>ID: </label> @html.TextBoxFor(x=>x.Id)
```
- **`مقادیر این تکست باکس از طریق متغیر x به فیلد Id در مدل ریخته میشه.`**
‌
- **`دکمه‌ها:`**
```html
{
...
<input type="submit" value=" text ">
}
```

`↓`‌`↓`‌`↓`
‌مثال یه فرم ثبت نام:
```html
{
<label>ID: </label> @html.TextBoxFor(x=> x.Id)

<label>Name: </label> @html.TextBoxFor(x=> x.Names)

<label>Email:: </label> @html.TextBoxFor(x=> x.Emais)

<input type="submit" value=" text ">

}
```

3. `بعد از کلیک روی button بهتره که به یک ویو دیگه منتقل بشیم. میتونیم توی کنترلر این ویو، به صورت زیر مشخص کنیم که بعد از کلیک روی دکمه به چه ویویی منتقل بشیم`:
```c#
return view ("view-name")
```

---
---
> ### بهینه سازی فراخوانی ویو ها


- **`میشه بجای()return view در کنترلر، از ()return RedirectToAction استفاده کرد. در این صورت از ارسال درخواست های تکراری و خطای زمان اجرا جلوگیری میشه`**
    - `مثلا هنگام انتقال به سایر ویو ها در حین اجرا میشه از return RedirectToAction ("view-name") بجای return view ("view-name") استفاده کرد. در این صورت اکشنِ ویوی مربوطه هم به طور کامل فراخوانی میشه و تغییرات داده ها در همون زمان اجرا به صورت زنده ثبت شده و بروز میمونه و دیگه خطای درخواست تکراری یا مشکلات عدم ثبت تغییرات حین اجرا رو نداریم.`

---
---

> ### جلسه نهم: **ارسال و دریافت داده‌ها با استفاده از GET و POST**

**ارسال و دریافت get و post**
 - `به شکل زیر نوع عملکرد هر ActionResualt رو مشخص میکنیم`:
```csharp
[HttpGet] 
Public ActionResult register()
{
}

[HttpPost]
Public ActionResult register()
{
}
```
- `نوشتن Get الزامیه. در غیر این صورت ویو ها فراخوانی نمیشن.`
‌
**استفاده از مقادیر ارسال شده توسط فرم**
- `مثلا ریختن توی ویوبگ و سشن`
```csharp
[HttpPost]
Public ActionResult register
("model" formdata )
{
Session.Add("Id", formdata.Id)
Session.Add("Names",formdata.Names)
viewbag.Id = formdata.Id;
}
```

---

> ### جلسه دهم: **کار با مدل‌های بزرگ و اتصال به دیتابیس با یکپارچه کردن مدل ها**

- بعد از ساخت مدل ها:
    - `برای یکپارچه کردن مدل ها و ارسال به سمت دیتابیس یک فایل class جدید ساخته و موارد زیر رو وارد می‌کنیم`:
    ‌
- ‌`استفاده از "db" تو نامگذاری این مدل توصیه میشه.`
```csharp
using System.data.Entity;
using System.ComponentModel. Dataannotation;
using System.ComponentModel. Dataannotation.schema;
using < project-name >.Models;
```
‌
**` این مدل رو از نوع dBcountext تعریف میکنیم:`**
```csharp
Public class datadb
```
↓
```csharp
Public class < dbmodel-name > : dBcountext 
```
‌
- `در نهایت یکی‌یکی مدل ها رو برای ارسال به سمت دیتابیس توی این مدل صدا می‌زنیم`:
‌`↓`
```C#
Public Dbset < model > name_model {get; set;}

Public Dbset < model2 > name_model2 {get; set;}

```
- `با استفاده از Dbset ، ارتباط بین مدل ها و جداول دیتابیس رو توسط نامی فرضی *name_model" برقرار می‌کنیم.`
---

> ### جلسه یازدهم: `code first` 
>  **شش مرحله برای فعال‌سازی مهاجرت و به‌روزرسانی دیتابیس**

- **ایجاد دیتابیس**:
1. نصب SQL server و ایجاد سرور محلی
2. نصب SSMS و اتصال به سرور محلی

- **اتصال به دیتابیس:**
1. ایجاد کلاس ها در پروژه 
2. ایجاد dBmodel و صدا زدن کلاس‌ها
3. ایجاد Connection String تو فایل web.config
4. فعالسازی مهاجرت 
    - دستور `Enable-Migrations`
5. اضافه کردن مهاجرت 
    - دستور `Add-Migration`
6. بروزرسانی دیتابیس بعد از هر تغییری در مدل ها و کلاس ها
    - دستور `Update-Database`

---
جلسه دوازدهم 
> ### صفحه ثبت نام و ذخیره تغییرات 

1. ایجاد متغیر سراسری برای دسترسی 
```c#
private "dbmodel" db = new "dbmodel"();
```
2. ارسال و ذخیره داده ها
```c#
db.name_model.Add(formdata);
db.Savechanges();
```
- **`دیتای ارسال شده از سمت فرم توسط اسم اختصاصی هر مدل:"name_model" و توسط dbmodel به سمت جداول دیتابیس فرستاده و ثبت میشه.`**
`↓`
```c#
File: HomeControler

private "dbmodel" db = new "dbmodel"();

[HttpGet]

public ActionResult register()
   {
   return View();
   }
   
[HttpPost]

public ActionResult register ("model" formdata)
   {
db.name_model.Add(formdata);
db.Savechanges();
return RedirectToAction ("Index);
}
```
- `به کمک RedirectToAction ، بعد از ثبت، به صفحه اول برگشته و ویو-کنترلر مجدداً بارگذاری میشه تا از ارسال درخواست تکراری و خطای زمان اجرا جلوگیری بشه.`
- `به علت استفاده از RedirectToAction سشن های گزارش‌دهندۀ وضعیت فرصت نمایش تو این ویو رو ندارن؛ به همین علت بعد از حذف و انتقال خودکار، پیام وضعیت رو در همون صفحه Index نمایش می‌دیدم و سشن هارو همونجا استفاده میکنیم.`
---
---
جلسه 
> ### جستجو در دیتابیس 

```c#
"model" < name > = db.name_model.FirstorDefault(u=> u.Id==Id);
```
- `یک متغیر از نوع مدل موردنظر تعریف شده و درون جدول دیتابیس بر اساس فیلد مربوط به Id ، رکوردها رو جستجو می‌کنه.`
- 
‌`↓`
```c#
[HttpPost]

public ActionResult finder(int id)

{

"model" < name > = db.name_model.FirstorDefault(u=> u.Id==Id);
  
if( < name > != null)
{
viewBag.Name= < name >.Name; viewBag.Lastname= < name >.Last_name;
return view();

}
else
{
session["find-status"] = "Not found";
return RedirectToAction ("finder");
}
```
- `رکورد ها بر اساس یک فیلد خاص، مثلا Id جستجو میشن. کاربر یک Id رو برا جستجو می‌فرسته و در صورت مطابقت، تمام محتویات رکورد مربوط به اون Id فراخوانی و در متغیر ها ذخیره میشن.`
- `در صورت پیدا نشدن رکوردی با عنوان موردنظر، به کمک RedirectToAction همین ویو مجددا به صورت اولیه بارگذاری میشه تا از ارسال فرم تکراری جلوگیری بشه.`

---
---
جلسه 
> ### حذف اطلاعات از دیتابیس

```c#
"model" < name > = db.name_model.FirstorDefault(u=> u.Id==Id);
```

```C#
if (Id != null)
{

   if (< name > != null)
   {
db.name_model.Remove(< name >);
db.Savechanges();
session["delet-status"] = "successful.";
   }
   else
   {
session["delet-status"] = "Not Found.";
   }

}

else
{
session["delet-status"] = "Please enter valid ID.";
}

return RedirectToAction("Index");
}
```
- `به کمک یک نام فرضی < name > و توسط فیلد Id، رکورد مربوطه ی ذخیره شده در model جستجو شده و در صورت وجود حذف میشود.`
- `به کمک RedirectToAction ، بعد از حذف، به صفحه اول برگشته و ویو-کنترلر مجدداً بارگذاری میشه تا از ارسال درخواست تکراری و خطای زمان اجرا جلوگیری بشه.`
- `به علت استفاده از RedirectToAction سشن های گزارش‌دهنده وضعیت فرصت نمایش تو این ویو رو ندارن؛ به همین علت بعد از حذف و انتقال خودکار، پیام وضعیت رو در همون صفحه Index نمایش می‌دیدم و سشن هارو همونجا استفاده میکنیم.`

---
---
> ### نمایش پیام های گزارش وضعیت حذف و ثبت، بعد از انتقال خودکار به Index

- دلیل انجام اینکار اینه که ویوبگ ها به علت ریکوئست مجدد منقضی میشن.
- به این شکل با هر بار اجرای Index بررسی می‌کنیم که آیا session ها مقدار گرفتن یا نه. اگه مقدار داشتن اونارو به کمک ویوبگ های یبار مصرف نمایش داده و مقادیر session رو پاک میکنیم.
```c#
```

---
---
> ### استایل های مانا و اسکلت ثابت سایت (Layout)
‌
‌

- ‌ `قسمت‌هایی مثل نوار کناری ، نوار بالایی ، استایل کلی، صفحه کامنت‌ها و غیره در فایل` `layout.cshtml_` `نوشته شده و توی مابقی ویوها اونو صدا می‌زنیم.` 
```html
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
}
```
- `یعنی دیگه از این به‌بعد فقط محتواگذاری می‌کنیم و استایل سایت پیش‌فرض همه جا استفاده میشه.`

> ### فراخوانی یک اکشن غیر مرتبط با ویو در یک view
> ‌

```html
<h2>صفحه داشبورد</h2>
<!-- دکمه لاگ‌اوت -->
<form action="@Url.Action("Logout")" method="post">
    <button type="submit">خروج از حساب</button>
</form>
```
- `این دکمه‌ی خروج از حساب در پنل داشبورد(یا حتی فایل Layout)، اکشن مربوط به LogOut رو صدا میزنه تا شروع به اجرا کنه.`

---
---

> ### ایجاد فرایند کامنت گذاری 
‌
‌
‌
---
---

> ### سیستم LogIn و LogOut

‌
- **ایجاد مدل**
```c#
public class User
{
    public int Id { get; set; }
    public string name { get; set; }
    public string username { get; set; }
    public string password { get; set; }
}
```

- **‌ویو مربوط به لاگین** 

```html
@model YourProject.Models.User

@using (Html.BeginForm())
{
    <label>Email:</label>
    @Html.TextBoxFor(x => x.Email)
    
    <label>Password:</label>
    @Html.PasswordFor(x => x.Password)
    
    <input type="submit" value="Login" />
}
```

- ‌ **کنترلر لاگین**
```c#
var "name" =
db.name_model.FirstOrDefault(x => x.Email == formData.Email && x.Password == formData.Password);
```
- ** `این یک شرط لامبداعه که دو عمل مختلف رو انجام میده؛ اول بررسی می‌کنه آیا دو داده ارسال شده از سمت formdata با مقادیر دو فیلد مشخص از دیتابیس مطابقت داره یا نه. در صورت تطابقِ هر دو، این مقادیر رو در یک متغیر ذخیره می‌کنه.` **
‌`+`
```c#
if ("name" != null)
    {
        Session["LogIn-status"] = "true" ;
        return RedirectToAction("Index", "Home");
    }
```
- ‌`مقدارگیریِ متغیر رو بررسی می‌کنیم(مطابقت رمز) و در صورت تأیید  یک سشن رو به عنوان کلیدِ اعتبارسنجی مقداردهی می‌کنیم.`
‌
- ‌**اعتبار سنجی کاربران در کنترلر**
```c#
public ActionResult UserDashboard()
{
    if (Session["LogIn-status"] == null)
    {
        return RedirectToAction("Login");
    }
    return View();
}
```
- `حالا در هر ویویی که مخصوص کاربران لاگین شده هست، با این شرط اعتبار کاربر رو بررسی می‌کنیم و در صورت عدم تایید، اون رو به صفحه لاگین هدایت می‌کنیم.`
‌
- **اعتبارسنجی کاربران در ویو**
```html
@if (Session["LogIn-status"] != null)
{
    <p>Welcome, @Session["LogIn-status"]</p>
    @Html.ActionLink("Logout", "Logout")
}
else
{
    @Html.ActionLink("Login", "Login")
}
```
‌
‌
- **کنترلر لاگ‌اوت**
```c#
public ActionResult Logout()
{
    Session.Clear();
    return RedirectToAction("Index");
}
```
مثال:
```c#
private dbmodel db = new dbmodel();

[HttpGet]
public ActionResult Login()
{
    return View();
}

[HttpPost]
public ActionResult Login(User  formData)
{
    var < name > = db.name_model.FirstOrDefault(x => x.Email == formData.Email && x.Password == formData.Password);

    if (user != null)
    {
        Session["user"] = user.Name;
        return RedirectToAction("Index", "Home");
    }
    else
    {
        ViewBag.Error = "Invalid email or password.";
        return View();
    }
    
public ActionResult Logout()
{
    Session.Clear();
    return RedirectToAction("Index");
}
}
```

---
---
> ### سیستم `LogIn` و `LogOut` پیشرفته با `cookie`
‌

‌
- ** *کنترلر لاگین* **

```c#
var "loginuser" =
db.model_name.FirstOrDefault(x => x.username == formData.username && x.Password == formData.Password);
```
- `با همون رویه قبلی`

```c#
if ("loginuser" != null)
    {
HttpCookie cookie = new HttpCookie("user", loginuser.username);

cookie.Expires = DateTime.Now.AddDays(5);

Response.Cookies.Add(cookie);
    }
```
- ‌`در قسمت اول یک متغیر از نوع کوکی با نام LogIn-status مقداردهی میشه.`
- `در بخش دوم یک مدت‌زمان برای منقضی شدن اعتبار لاگین مشخص می‌کنیم - در غیر این صورت موقتیه.`
- `در بخش سوم کوکی رو همراه با مقدارش به مرورگر کاربر می‌فرستیم تا اونجا ذخیره بشه.`


- **اعتبارسنجی کاربران در هر کنترلر***
```c#
if (Request.Cookies["LogIn-status"] == null)
{
    return RedirectToAction("login");
}
return view();
```
-  `متغیر مربوط به اعتبارسنجیِ ذخیره‌شده در کش مرورگر کاربر رو بررسی می‌کنیم تا ببینیم معتبره یا نه. اگه نبود به صفحه لاگین هدایت میشه.`
‌
- **`کنترلر مربوط به لاگ‌اوت`**
```c#
public ActionResult Logout()
{
    HttpCookie cookie = new HttpCookie("LogIn-status");
    
    cookie.Expires = DateTime.Now.AddDays(-1);
    
    Response.Cookies.Add(cookie);

 return RedirectToAction("Index");
}
```
- `دستور مستقیمی برای حذف کوکی وجود نداره. پس ما دوباره همون کوکی رو این بار بدون مقدار تعریف و مدت زمان اون رو یک روز قبل تعیین می‌کنیم. "مرورگر به طور خودکار کوکی‌های تاریخ گذشته رو حذف می‌کنه" در نتیجه بعد از ارسال این کوکی به مرورگر از بین میره.`

- **فرایند LogOut در ویو***
```html
<h2>صفحه داشبورد</h2>
<!-- دکمه لاگ‌اوت -->
<form action="@Url.Action("Logout")" method="post">
    <button type="submit">خروج از حساب</button>
</form>
```
`این دکمه در هر ویویی که باشه اکشن مربوط به لاگ‌اوت رو فراخوانی می‌کنه.`

---
---


> ### استفاده از دو فرم در یک ویو 
> - ارسال به اکشن‌های متفاوت 
‌

```html
‌@using (Html.BeginForm("actio-name", "controller-name", FormMethod.Post/Get))
{
}
```
- **`داخل فرم مشخص میکنیم که محتوای فرم به کدوم اکشن از چه کنترلری بره.`**
    - `نوع متد رو میشه مشخص کرد.`
---
---

> ### استفاده از یک فرم برای انجام دو عمل مختلف
> - ** `با دو تا دکمه اختصاصی در یک ویو، اکشن حذف و جستجو رو یکی کردیم.` **
‌
‌
- **ویو**
```html
‌
@model YourNamespace.Models.students

@using (Html.BeginForm("", "Home", FormMethod.Post))
{
    @Html.TextBoxFor(x => x.Id, new { placeholder = "Enter ID" })

    <button type="submit" name="actionType" value="finder">Search</button>
    <button type="submit" name="actionType" value="delete">Delete</button>
}
```
- **`تایپ دکمه ها به شکلیه که بعد از کلیک، هر کدوم مقدار خاصی میگیرن.`**
‌
‌
- **کنترلر dashboard**
```c#
public ActionResualt
finder(int? Id, string actionType)
{

 if (actionType == "finder")
 {
 //searching code..
 return RedirectToAction("dashboard")
 }


 else if (actionType == "delet")
 {
 //deleting code..
 return RedirectToAction("dashboard")
 }
}
```
- `بهتره نکات مربوط به ریدایرکشن رو در نظر بگیریم از جمله عدم امکان استفاده از ویوبگ.`

- **`نکته مهم`**: `ممکنه به دلیل ساختار ویو ، بعد پیدا شدن Id ، دیگه مقداری به فرآیند delete نرسه.`
    - **برای حل این مشکل**:
1. داخل شرط `finder` بعد از اینکه مقدار Id جستجو شده null نبود یک session تعریف میکنیم.
```c#
//"model" student = db.tbl_model...
//if (student != null){
session["stdId"] = student.Id;
```
‌
2. سپس داخل شرط `delete` به این شکل از این مقادیر استفاده میکنیم:
```c#
//مقدار سشن رو به صورت عددی به یک متغیر می‌ریزیم.
int? studentId = Session[stdId] as int?;

//با همون رویه قبلی مقادیر ارسال شده از سمت فرم‌دیتا رو مطابقت میدیم.
"model" student = db.tbl_model.FirstOrDfault(x => x.Id == stdId)

//تطابق و حذف 
if (student!= null){
db.tbl_model.Remove(student);
db.SaveChange();
}

```

