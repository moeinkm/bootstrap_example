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
  
در این کد یک ریکوئست گت نام کاربر را فرضا میگیرد و در یک جایی نگه میدارد، اگر مهاجم به جای نام کاربری اسکریپتی را بفرستد در هنگام فرضا فراخوانی یا نمایش نام این اسکریپت اجرا میشود، برای جلوگیری از اجرای آن میتوانیم این اسکریپت را به عنوان فرضا تایپ استرینگ  میگیریم تا قابل اجرا نباشد به صورت زیر


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

روی پورت 8080

سوال۴:

هوک ها توابعی ساده اند که به ما اجازه می دهند از قابلیت های  state و lifecycle در react بدون استفاده از ساختار class در کامپوننت هایی که به صورت تابع هستند استفاده کنیم

این یک هوک کاستوم است که با تغییر استیت صفحه و تغییر عرض آن به کمتر از ۶۰۰ پیکسل استیت isSmall ترو میشود 

</div>


```
import { useState, useEffect } from "react";
const useWindowsWidth = () => {
    const [isSmall, setIsSmall] = useState(false);
    let checkScreenSize = () => {
        setIsSmall(window.innerWidth < 600); // result is boolean
    };
    useEffect(() => {
        checkScreenSize();
        window.addEventListener("resize", checkScreenSize); // call when the window size changes
        return () => window.removeEventListener("resize", checkScreenSize);
    }, []);
    return isSmall;
};
export default useWindowsWidth;
```

<div dir="rtl>
در فانکشن زیر هنگام تغییر استیت فرضاً رندر جدید برگرداده میشود         

</div>

```
import React from 'react'
import useWindowWidth from './useWindowWidth.js'
const MyComponent = () => {
  const onSmallScreen = useWindowWidth();
  return (
    // Return some elements
  )
}
```

<div dir="rtl">

سوال۵:

الف) در session کاربر ذخیره میکنیم

برای داده هایی که میتوان در سمت کلاینت ذخیره کرد

تا گرفتار تاخیر هارد نشویم و چون نمیخواهیم توزیع شده این کار را انجام دهیم پس مصرف س پی یو تغییری در حالت های مختلف نمیکند با ذخیره در ردیس میتوانیم مثلا عدد بزرگی که در نظر میگیریم را در ردیس ذخیره کنیم چون به کاربر ارتباطی ندارد ولی در هارد آن را ذخیره نمیکنیم چون با منقضی شدن نشست (درصورتی که نشست را برای مدت طولانی ای میخواهیم استفاده کنیم میتوان آن را در هارد ذخیره کرد چون با درصورت ذخیره در ردیس این داده را از دست میدهیم) 

ب) در نشست ذخیره میکنیم و از load balancer و sticky session استفاده میکنیم 



ج) در اینجا چون از حالت قبل ریت استفاده از شبکه کمتر است میتوان در ردیس توزیع شده استفاده کرد.

</div>
