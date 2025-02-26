> ### جلسه اول: **آشنایی با Controller و ایجاد View**

1. **باز کردن قسمت Controller**

2. **ایجاد یک Controller با نام Home**

3. **استفاده از اکشن Resultها برای عملیات مختلف**
   - نام اولین اکشن باید *index* باشد.

4. **کلیک راست درون پرانتز return view**

5. **انتخاب گزینه Add View**

6. **انتخاب یک View هم نام با اکشن Result روی حالت بدون مدل**

7. **نوشتن اولین پیام در بین div های فایل View با نام index**

---

> ### جلسه دوم: **آغاز ساخت بازی سنگ کاغذ قیچی**

1. **ساخت کد Random ساز برای بازی سنگ کاغذ قیچی در ActionResult Index:**
   ```csharp
   Random num = new Random();
   int nums = num.Next(1, 4);
   if (nums == 1) {
       // ادامه کد
   }
   ```
   - `سورس مربوط به بازی و تولید متغیرهای آن عموماً باید در Index نوشته بشود. چون هر متغیری که فراخوانی می‌شود باید از قبل تولید شده باشد.`

2. **ساخت یک متغیر در Controller و استفاده در View متعلق به آن:**
   ```csharp
   ViewBag.<var-name> = "مقدار";
   ```

3. **استفاده از متغیر Controller در View:**
   ```html
   @ViewBag.<var-name>
   ```
   مثال:
   ```csharp
   if (b == 1) {
       ViewBag.rand = "سنگ";
   }
   ```
   ```html
   @ViewBag.rand
   ```

---

> ### جلسه سوم: **ساخت ساختار اولیه بازی سنگ کاغذ قیچی**

1. **ایجاد جدول در view و نمایش متغیرهای بازی درون یک جدول 2×2**

2. **استفاده از تگ marquee برای نمایش پیام متحرک در بالای صفحه**

3. **سایز دهی و مرکز کردن جدول**

---

> ### جلسه چهارم: **فراخوانی View درون View و ایجاد منو**

1. **باز کردن یک فرم در فرم دیگر:**
   - با استفاده از ساختار زیر می‌توان یک view را در یک view دیگر فراخوانی کرد:
     ```csharp
     @Html.ActionLink("نام ویو", "متن")
     ```
   - **سپس یک ویو اضافه می‌شود:**
     - ابتدا یک اکشن Result تعریف شود.
     - سپس یک ویو درون return view ایجاد گردد.

2. **نمایش عناوین:**
   - **ایجاد یک صفحه اصلی**
   - نمایش دو عنوان "صفحه اصلی" و "گالری عکس"
   - انتقال کاربر به view های دیگر.
   - توجه به وجود فایل برای نمایش در ویو گالری عکس مهم نیست.

---

> ### جلسه پنجم: **آشنایی با Entity Framework و نصب آن**

برای کار با پایگاه داده و توابع مربوط به ذخیره داده‌ها، از **Entity Framework** استفاده می‌شود.

- #### Entity Framework
  - **EF6**: مناسب برای مدل‌های کلاسیک و ساده‌تر.
  - **Core**: مناسب برای مدل‌های پیشرفته‌تر.

- #### نصب فریم ورک
1. **رفتن به مسیر زیر:**
   - `Tools` → `NuGet Package Manager` → `Manage NuGet Packages for Solution`

2. جستجوی عبارت "`Entity Framework`" در تب `Browse`.

3. انتخاب `Entity Framework`.

4. انتخاب پروژه مورد نظر و کلیک بر روی `Install`.

- #### ایجاد یک مدل نمونه در پروژه
برای ایجاد یک مدل جدید:
1. رفتن به پوشه **Models**.
2. کلیک بر روی گزینه **Add**.
3. انتخاب گزینه **New Item**.
4. ایجاد فایل با نام `file-name.cs` (از نام "class.cs" استفاده نشود).

---

> ### جلسه ششم: **استفاده از Session برای متغیرهای سراسری**

**ساخت متغیر قابل استفاده در تمام ویو های دیگر**
1. ابتدا درون index با استفاده از session یک متغیر سراسری تعریف می‌کنیم:
   ```csharp
   session.Add("نام متغیر", "مقدار")
   ```

2. سپس درون view هر ActionResult دیگری می‌توان با استفاده از session از این متغیر استفاده کرد:
   ```csharp
   @session["نام متغیر]
   ```

   مثال:
   - ساخت `Public ActionResult Game`
   - ساخت یک ویو برای کنترلر Game
   - با استفاده از `@session` از این متغیر استفاده می‌کنیم.

**`نکته`**: `اولویت بندی فرم ها اهمیت دارد. Session ها باید قبل از فراخوانی تعریف شده باشند در نتیجه بهتر است تمامی کد ها و تعاریف در ActionResult Index انجام شده سپس از متغیر ها در سایر ActionResult ها استفاده کنیم.`

---

> ### جلسه هفتم: **شروع کار با دیتابیس و تعریف مدل‌ها**

**استفاده از دیتابیس**
چارت اولیه تعریف مقادیر در دیتابیس:
درون return view یک ویو empty ساخته و مدل را انتخاب می‌کنیم.

|       | Id  | Names | Emails |
| ----- | --- | ----- | ------ |
| Value |     |       |        |
| Value |     |       |        |

- تنظیم:
   ```csharp
   Public int Id {get; set;}
   Public string Names {get;set;}
   Public string Emails {get;set;}
   ```
   - تنظیم get: دیتای قابل فراخوانی از سمت کاربر
   - تنظیم set: دیتای قابل تنظیم از سمت کاربر

---

> ### جلسه هشتم: **ساخت صفحه لاگین و فرم‌های ورودی**

**ساختار صفحه لاگین گرفتن داده ها از کاربر در ویو**

بعد از ساخت view در حالت empty به همراه مدل، درون ویو یک صفحه برای وارد کردن اطلاعات به وسیله text box ها ایجاد می‌کنیم.
```html
@Html.Begin.Form()
{
}
```
- تمام عناصر درون فرم با یکدیگر مرتبط هستند.

#### - ساختار تکست باکس
> Label : (textbox)
```html
<label> "text" </label> @html.TextBoxFor("var" => "var"."field in database")
```
مثال:
```html
<label>ID: </label> @html.TextBoxFor(x=>x.Id)
```
- مقادیر تکست باکس از طریق متغیر x به فیلد `Id` در دیتابیس ریخته می‌شود.

#### - ساختار button
```html
{
...
<input type="" value="">
}
```
نوع type هر چیزی می‌تواند باشد اما برای ساخت button که اکشنی را روی فرم اعمال می‌کند از `"type="submit"` استفاده می‌کنیم.

بعد از طراحی جدول، تمام عناصر را وارد یک سطر جدول می‌کنیم تا کادربندی شود.
```html
<center>
<table border="1">
    <tr>
        <td>
            @html.BeginForm()
            {
            }
        </td>
    </tr>
</table>
</center>
```

---

> ### جلسه نهم: **ارسال و دریافت داده‌ها با استفاده از GET و POST**

**ارسال و دریافت get و post**
با استفاده از `[HttpGet]` و `[HttpPost]` نوع کار با داده را مشخص می‌کنیم.
```csharp
[HttpGet] 
Public ActionResult registers()
{
}

[HttpPost]
Public ActionResult registers()
{
}
```

سپس داده های فرم را در action ای که post است، از طریق session به دیتابیس منتقل می‌کنیم تا در سایر ویو ها قابل استفاده باشد.
```csharp
[HttpPost]
Public ActionResult registers("Model" formdata)
{
    Session.Add("id", formdata.id)
    Session.Add("Emails", formdata.Emails)
    Session.Add("Names", formdata.Names)
}
```

- **برای تعریف viewBag:**
```csharp
ViewBag."var" = formdata."Model";
```

- برای استفاده از متغیر سشن در ویوی دیگر، مثلاً پایین همان فرم رجیستر:
```csharp
<center>
<table border="1">
    <tr>
        <td>
            @html.BeginForm()
            {
            }
        </td>
    </tr>
</table>
</center>

@Session["id"]
```

> - رفتن به فرم بعد بعد از زدن button:
   ```csharp
   return view ("game")
   ```

---

> ### جلسه دهم: **کار با مدل‌های بزرگ و اتصال به دیتابیس**

**کد فرست**
بعد از ساخت table ها یک مدل بزرگ می‌سازیم که همه ی table ها را در بر بگیرد.

برای شروع ابتدا موارد زیر را در مدل using می‌کنیم:
```csharp
Using System.data.Entity;
Using System.ComponentModel. Dataannotation;
System.ComponentModel. Dataannotation.schema;
```

- یک فایل مدل جدید و یک class از نوع dBcountext تعریف می‌کنیم:
```csharp
Public class datadb: dBcountext 
```
  - اگر در ساخت کلاس به مشکل خورد فایل entity framework نصب شود.

سپس برای تعریف یک جدول (فیلد نه):
```csharp
Public Dbset <مدل> name {get; set;}
```
در کد بالا اگر ارور داد برای استفاده از پروژه در فایل database، پروژه را صدا می‌زنیم:
```csharp
Using project-1.Models;
```

---

> ### جلسه یازدهم: **فعال‌سازی مهاجرت و به‌روزرسانی دیتابیس**

**کار با بانک اطلاعاتی**

|
|-- `Create Model`
|   |
|   |-- `dbconnect (اتصال به پایگاه داده)`
|   |   |
|   |   |-- `Connection String (رشته اتصال)`
|
|-- `Enable Migration (فعال کردن مهاجرت)`
|
|-- `Add Migration (اضافه کردن مهاجرت)`
|
|-- `Update Database (به‌روزرسانی پایگاه داده)`
