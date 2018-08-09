**本章描述 <input> 元素的输入类型。**

## 输入类型：text

*<input type="text">* 定义供*文本输入*的单行输入字段：

### 实例

```
<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_text)

以上 HTML 代码在浏览器中看上去是这样的：

First name:
Last name:

## 输入类型：password

*<input type="password">* 定义*密码字段*：

### 实例

```
<form>
 User name:<br>
<input type="text" name="username">
<br>
 User password:<br>
<input type="password" name="psw">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_password)

以上 HTML 代码在浏览器中看上去是这样的：

User name:
User password:

注释：password 字段中的字符会被做掩码处理（显示为星号或实心圆）。

## 输入类型：submit

*<input type="submit">* 定义*提交*表单数据至*表单处理程序*的按钮。

表单处理程序（form-handler）通常是包含处理输入数据的脚本的服务器页面。

在表单的 action 属性中规定表单处理程序（form-handler）：

### 实例

```
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_submit)

以上 HTML 代码在浏览器中看上去是这样的：

First name:
Last name:

如果您省略了提交按钮的 value 属性，那么该按钮将获得默认文本：

### 实例

```
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_submit_nn)

## Input Type: radio

<input type="radio"> 定义单选按钮。

Radio buttons let a user select ONLY ONE of a limited number of choices:

### 实例

```
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_radio)

以上 HTML 代码在浏览器中看上去是这样的：

Male 
Female

## Input Type: checkbox

<input type="checkbox"> 定义复选框。

复选框允许用户在有限数量的选项中选择零个或多个选项。

### 实例

```
<form>
<input type="checkbox" name="vehicle" value="Bike">I have a bike
<br>
<input type="checkbox" name="vehicle" value="Car">I have a car 
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_checkbox)

以上 HTML 代码在浏览器中看上去是这样的：

I have a bike 
I have a car

## Input Type: button

*<input type="button>* 定义*按钮*。

### 实例

```
<input type="button" onclick="alert('Hello World!')" value="Click Me!">

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_button)

以上 HTML 代码在浏览器中看上去是这样的：

## HTML5 输入类型

HTML5 增加了多个新的输入类型：

- color
- date
- datetime
- datetime-local
- email
- month
- number
- range
- search
- tel
- time
- url
- week

注释：老式 web 浏览器不支持的输入类型，会被视为输入类型 text。

## 输入类型：number

*<input type="number">* 用于应该包含数字值的输入字段。

您能够对数字做出限制。

根据浏览器支持，限制可应用到输入字段。

### 实例

```
<form>
  Quantity (between 1 and 5):
  <input type="number" name="quantity" min="1" max="5">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_number)

## 输入限制

这里列出了一些常用的输入限制（其中一些是 HTML5 中新增的）：

| 属性        | 描述                |
| --------- | ----------------- |
| disabled  | 规定输入字段应该被禁用。      |
| max       | 规定输入字段的最大值。       |
| maxlength | 规定输入字段的最大字符数。     |
| min       | 规定输入字段的最小值。       |
| pattern   | 规定通过其检查输入值的正则表达式。 |
| readonly  | 规定输入字段为只读（无法修改）。  |
| required  | 规定输入字段是必需的（必需填写）。 |
| size      | 规定输入字段的宽度（以字符计）。  |
| step      | 规定输入字段的合法数字间隔。    |
| value     | 规定输入字段的默认值。       |

您将在下一章学到更多有关输入限制的知识。

### 实例

```
<form>
  Quantity:
  <input type="number" name="points" min="0" max="100" step="10" value="30">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_number_step)

## 输入类型：date

*<input type="date">* 用于应该包含日期的输入字段。

根据浏览器支持，日期选择器会出现输入字段中。

### 实例

```
<form>
  Birthday:
  <input type="date" name="bday">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_date)

您可以向输入添加限制：

### 实例

```
<form>
  Enter a date before 1980-01-01:
  <input type="date" name="bday" max="1979-12-31"><br>
  Enter a date after 2000-01-01:
  <input type="date" name="bday" min="2000-01-02"><br>
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_date_max_min)

## 输入类型：color

*<input type="color">* 用于应该包含颜色的输入字段。

根据浏览器支持，颜色选择器会出现输入字段中。

### 实例

```
<form>
  Select your favorite color:
  <input type="color" name="favcolor">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_color)

## 输入类型：range

*<input type="range">* 用于应该包含一定范围内的值的输入字段。

根据浏览器支持，输入字段能够显示为滑块控件。

### 实例

```
<form>
  <input type="range" name="points" min="0" max="10">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_range)

您能够使用如下属性来规定限制：min、max、step、value。

## 输入类型：month

*<input type="month">* 允许用户选择月份和年份。

根据浏览器支持，日期选择器会出现输入字段中。

### 实例

```
<form>
  Birthday (month and year):
  <input type="month" name="bdaymonth">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_month)

## 输入类型：week

*<input type="week">* 允许用户选择周和年。

根据浏览器支持，日期选择器会出现输入字段中。

### 实例

```
<form>
  Select a week:
  <input type="week" name="week_year">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_week)

## 输入类型：time

*<input type="time">* 允许用户选择时间（无时区）。

根据浏览器支持，时间选择器会出现输入字段中。

### 实例

```
<form>
  Select a time:
  <input type="time" name="usr_time">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_time)

## 输入类型：datetime

*<input type="datetime">* 允许用户选择日期和时间（有时区）。

根据浏览器支持，日期选择器会出现输入字段中。

### 实例

```
<form>
  Birthday (date and time):
  <input type="datetime" name="bdaytime">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_datetime)

## 输入类型：datetime-local

*<input type="datetime-local">* 允许用户选择日期和时间（无时区）。

根据浏览器支持，日期选择器会出现输入字段中。

### 实例

```
<form>
  Birthday (date and time):
  <input type="datetime-local" name="bdaytime">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_datetime-local)

## 输入类型：email

*<input type="email">* 用于应该包含电子邮件地址的输入字段。

根据浏览器支持，能够在被提交时自动对电子邮件地址进行验证。

某些智能手机会识别 email 类型，并在键盘增加 ".com" 以匹配电子邮件输入。

### 实例

```
<form>
  E-mail:
  <input type="email" name="email">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_email)

## 输入类型：search

*<input type="search">* 用于搜索字段（搜索字段的表现类似常规文本字段）。

### 实例

```
<form>
  Search Google:
  <input type="search" name="googlesearch">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_search)

## 输入类型：tel

*<input type="tel">* 用于应该包含电话号码的输入字段。

目前只有 Safari 8 支持 tel 类型。

### 实例

```
<form>
  Telephone:
  <input type="tel" name="usrtel">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_tel)

## 输入类型：url

*<input type="url">* 用于应该包含 URL 地址的输入字段。

根据浏览器支持，在提交时能够自动验证 url 字段。

某些智能手机识别 url 类型，并向键盘添加 ".com" 以匹配 url 输入。

### 实例

```
<form>
  Add your homepage:
  <input type="url" name="homepage">
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_url)