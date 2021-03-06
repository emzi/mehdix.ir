---
title: تولید فرمولهای زیبای ریاضی در وب
category: پروژه
tags: react mathjax ریاضی فرمول
uuid: 335ef169-0331-4ae5-a1f0-bc775412e798
---

از چندی پیش تصمیم گرفته‌ام همینطور که مشغول برنامه‌نویسی هستم قطعات کوچک کارهای خودم را به صورت پکیج قابل استفاده مجدد منتشر کنم. امروز یک کامپوننت کوچک React نوشتم.

چند وقتی است درگیر نمایش فرمولهای ریاضی در یک پروژه React هستم. [React][ریکت] یک پروژه اوپن سورس از طرف شرکت فیسبوک است. وبسایتها یا اپ‌هایی که با این تکنولوژی ساخته می‌شوند از قسمت‌های کوچکی بنام Component تشکیل می‌شوند. هر کامپوننت State خودش را دارد و بخش مجزایی از برنامه را به اصطلاح «رِندر» می‌کند. React هم همواره گوش به زنگ تغییر State است و با هر تغییر از همه کامپوننت‌ها می‌خواهد که خودشان را بروز کنند. البته هر کامپوننت خودش تصمیم می‌گیرد که بروز بشود یا نه.

به همین معرفی کوتاه از React بسنده می‌کنم و می‌روم سراغ کامپوننت خودم. در میان محققان سه روش رایج برای مکتوب کردن فرمولهای ریاضی وجود دارد. TeX و ASCIImath و MathML. در این میان TeX از همه معروف‌تر و پرکاربردتر است. MathML هم یک استاندارد مبتنی بر XML است که برای تایپ توسط آدمها ساخته نشده و بیشتر برای هضم توسط برنامه‌ها و مرورگرها بوجود آمده است. ولی مرورگرها به درستی از آن پشتیبانی نمی‌کنند. در اینترنت پروژه اوپن سورس خوب دیگری وجود دارد بنام MathJax. این پروژه که با جاوااسکریپت نوشته شده می‌تواند هر سه فرمتهای بالا را بپذیرد و خروجی زیبا و قابل نمایش در مرورگر اینترنت بازدید کننده تولید بکند. اهمیت این پروژه در اینست که می‌تواند بسته به نوع و نسخه مرورگر بازدید کننده خروجی مناسب تولید کند. حالا یا با تولید کد MathML یا توسط استایل‌گذاری با CSS و HTML خالص. لازم به ذکر است که هیچ مرورگری قادر به نمایش ASCIImath و TeX نیست. در پشتیبانی از MathML هم بین علما اختلاف است!

حالا کامپوننت ما این وسط چکاره است؟ مشکل من این بود که نمی‌توان [MathJax][جکس] را به صورت خام در یک پروژه React بکار برد و باید برایش یک کامپوننت نوشت که با توجه به Life Cycle کامپوننت React در زمان مناسب عمل رِندر کردن خروجی را انجام بدهد. (از توضیح Life Cylce می‌گذریم!) من هم بجای اینکه در لابلای کد پروژه خودم اینکار را انجام بدهم برایش یک کامپوننت بنام `react-mathjax-preview` نوشتم و روی npmjs [منتشر][پکیج] کرده‌ام. در یک پروژه جاوااسکریپت می‌توان آنرا به شیوه زیر نصب کرد:


    $ npm install react-mathjax-preview

برای استفاده از هم کافی است پکیج را ایمپورت کنید و رشته حاوی کدهای ریاضی را به آن بدهید:

```js
import React, {Component} from 'react'
import {render} from 'react-dom'
import MathJax from 'react-mathjax-preview'

const math = String.raw`

  $$\lim_{x \to \infty} \exp(-x) = 0$$`

class Demo extends Component {
  constructor(props) {
    super(props);
    this.state = {
      math: tex
    }
  render() {
    return <MathJax math={this.state.math} />
  }
}
```

همراه سورس برنامه یک دموی کوچک هم هست که به روش زیر می‌توانید اجرا کنید:

    git clone https://github.com/mehdisadeghi/react-mathjax-preview && cd react-mathjax-preview
    npm install
    npm run start

اگر با مرورگر لوکال‌هاست پورت ۳۰۰۰ را باز کنید خروجی باید چیزی شبیه عکس زیر باشد:

{: .center}
![](assets/pimg/mathjax-preview.png)


طبق روال همیشه ‬[سورس][سورس] برنامه روی گیت‌هاب است.

[ریکت]: https://facebook.github.io/react/
[جکس]: https://www.mathjax.org/
[پکیج]: https://www.npmjs.com/package/react-mathjax-preview
[سورس]: https://github.com/mehdisadeghi/react-mathjax-preview
