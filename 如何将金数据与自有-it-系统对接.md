#如何将金数据与自有 IT 系统对接

当一款产品需要与其他产品集成时，往往意味着漫长的对接流程，从零开始了解对方的系统架构、低效的沟通，开发 API 等等，其中耗费的时间与精力，拖慢了很多公司的工作效率。

金数据目前已经拥有完整的 API ，可以让你免去很多对接工作，也有附带参数跳转的功能，方便你将数据写入自己的系统内。

##开启 API

金数据API为具备编程能力的用户提供了极强的扩展功能。开发者可以通过表单API获取表单定义、通过数据API追加数据或通过数据推送API将新提交的数据推送到自己的平台。

前往 **个人中心** —— **API** 来开启你的API支持及[获取API Key\/Secret](https://help.jinshuju.net/articles/api-auth.html)。

API访问规则

* 所有的数据格式为JSON
* 所有的数据传输编码为UTF-8
* 目前，API访问的地址来源为[https:\/\/jinshuju.net\/api\/v1\/](https://jinshuju.net/api/v1/)
* 除了数据推送API外，所有的API都需要恰当的API访问权限。目前我们仅支持HTTP Basic验证的方式。

## 目前提供的API

1. 数据推送API：开启数据推送API的表单收到新数据时，金数据会将该数据通过HTTP POST推送到指定的URL。

2. 表单API：您可以通过该API获取表单定义，然后你可以在任意你熟知的平台上重绘这个表单。通过结合[数据API](https://help.jinshuju.net/articles/entry-api.html)，您可以脱离金数据界面绘制和添加数据。

3. 数据API：您可以通过这个API添加数据。您能够将所有的数据通过JSON格式以HTTP POST的方式发送到对应的表单。

##设置跳转的附带参数

你可以设置填表者点击提交后，附带当前表单的部分内容跳转到指定网址。

目前可供选择的附带参数包括表单中的单\/多行文本、单选、多选、数字、邮箱、电话、日期以及网址等字段。如果表单中包含商品字段，则还可以附带序号和总价。您最多可以选择3个附带参数。

![](https://o1cqumdwn.qnssl.com/assets/file/408/redirect-with-params.png)

在表单的 **设置** —— **数据提交** 页面的 **填写者填写完表单后** 选择“自动打开其他网页”，填写您要跳转的网址，并勾选需要附加的参数。

当用户填写了该表单并提交后，将会附带勾选的参数跳转到网页。 例如：[http:\/\/success.test.com\/?field\_1=xxx&field\_2=xxx&jamr\_h=xxx&serial\_number=xxx](http://success.test.com/?field_1=xxx&field_2=xxx&jamr_h=xxx&serial_number=xxx)

跳转的网址包含4个参数：serial\_number、field\_1、field\_2和jamr\_h。 前3个是你勾选的字段，字段的API Code可以点击上图所示的“字段对照表”查看得到。jamr\_h是系统自动生成的验证码。您可以通过发送一个GET请求至 [https:\/\/jinshuju.net\/api\/v1\/jamr\_v](https://jinshuju.net/api/v1/jamr_v) 来验证跳转参数的有效性。

###验证跳转参数的有效性

您可以对跳转附带的参数进行验证，以保证该参数有效或者没有被恶意篡改。

您需要在提交成功转向后的 **10分钟内** 发送GET请求至 [https:\/\/jinshuju.net\/api\/v1\/jamr\_v进行验证](https://jinshuju.net/api/v1/jamr_v%E8%BF%9B%E8%A1%8C%E9%AA%8C%E8%AF%81)。

例如： [https:\/\/jinshuju.net\/api\/v1\/jamr\_v?field\_1=xxx&field\_2=xxx&jamr\_h=xxx&serial\_number=xxx](https://jinshuju.net/api/v1/jamr_v?field_1=xxx&field_2=xxx&jamr_h=xxx&serial_number=xxx)

如果返回200则表示验证通过，如果返回400则表示验证失败，失败信息可以查看response JSON中的message。



