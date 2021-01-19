<div dir="rtl">
  
# پایان ترم برنامه نویسی وب

## معین کاملی ۹۹۰۱۱۰۵۳


سوال۱:


سوال۲:

</div>
<div dir="rtl">

xss به نوعی از حمله گفته میشه که یک اسکریئت در کد تزریق (inject) میشه و اون کد میتونه مخرب باشه و اهداف مهاجم رو انجام بده هدف ما جلوگیری از اجرا شدن اون اسکریپته


کد زیر رو در نظر بگیرید

</div>
```

// request data
const body={
    name: "<script>alert('xss attack')</script>"
};
// vulnerable code
get('/', function (req, res) {
    req.body.name;
});

```
<div dir="rtl">
در این کد یک ریکوئست گت نام کاربر را فرضا میگیرد و در یک جایی نگه میدارد، اگر مهاجم به جای نام کاربری اسکریپتی را بفرستد در هنگام فرضا فراخوانی یا نمایش نام این اسکریپت اجرا میشود، برای جلوگیری از اجرای آن میتوانیم این اسکریپت را به عنوان فرضا تایپ استرینگ  میگیریم تا قابل اجرا نباشد به صورت زید
</div>
```

// use sanitizer package
get('/', function (req, res) {
    //Sanitize user input
    req.body.sanitize('name').xss();
});

```

<div dir="rtl">
  
ما در اینجا از پکیج sanitize استفاده کردیم تا نام گرفته شده از کاربر قابلیت اجرا شدن نداشته باشد.


سوال۳:

دو ورژن ای پی آی یک و دو وجود داره هر کدوم سه تا یو آر ال به صورت زیر

v1:

"/v1/login"

"/v1/submit"

"/v1/read"

v2:

"/v2/login"

"/v2/submit"

"/v2/read"

سوال۴:


</div>
