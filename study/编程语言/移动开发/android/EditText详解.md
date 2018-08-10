[官方文档](https://developer.android.com/reference/android/widget/EditText.html)

```
java.lang.Object
   ↳	android.view.View
 	   ↳	android.widget.TextView
 	 	   ↳	android.widget.EditText
```

EditTex是Android中比较常用的一个控件,它是用户和Android应用进行数据传递的通道.

## 常用属性

```
android:hint 设置hint提示文本

android:textColorHint 设置hint提示文字颜色

android:textColor 设置文字颜色

android:textSize 设置文本字体大小

android:textStyle 
设置文本字体样式,bold(加粗),italic(倾斜),normal(默认是正常字体).

android:numeric 控制EditText输入数字的类型 decimal(浮点数),integer(正整数),signed(带+ -号的整数).
注意:该属性在使用时提示已过时,建议使用android:inputType属性替代.

android:singleLine 
设置是否单行输入
true(单行输入),false(会自动换行).
注意:盖属性在使用时提示已过时,建议使用android:maxLines="1"属性替代.

android:password="true" 
以密文的形式显示输入的文本.
注意:该属性在使用时提示已过时,建议使用android:inputType属性替代.


android:textColorHighlight 
设置被选中字体的颜色.
默认为 Theme 主题中的 “colorAccent”的颜色.

textCursorDrawable 
设置被光标的颜色.默认为 Theme 主题中的 “colorAccent”的颜色.

android:textScaleX 设置文本的水平缩放系数.

android:typeface 设置hint提示文本的字体.
normal(默认),monospace,sans,serif.

android:background 设置EditText背景.
"@null"设置背景为透明.当我们设置背景后,EditText的那条线就会消失.

android:textAppearance //设置文本的颜色,字体,大小和样式.

android:digits 设置只接收指定的文本内容.

android:phoneNumber="true" 设置输入电话号码.
注意:该属性在使用时提示已过时,建议使用android:inputType属性替代.

android:editable 设置EditText是否可以编辑.
当你设置为true,会提示你该EditText已经是可编辑的.
设置为false时会提示使用inputType替代.

android:inputType 设置文本的类型，用于帮助输入法显示合适的键盘类型.

android:maxLength 设置EditText最多接受的文本的个数.

android:lines 
设置EditText显示的行数,设置两行就显示两行，即使第二行没有数据.

android:lineSpacingExtra 设置行间距.

android:lineSpacingMultiplier 设置行间距的倍数. 如设置成1.5倍

android:imeOptions 
设置右下角IME动作与编辑框相关的动作
如actionDone右下角将显示一个“完成”，而不设置默认是一个回车符号.
```

## 小例子

### 登录界面

![EditTextDemo.png](http://okyfoew6j.bkt.clouddn.com/EditTextDemo.png)

在 activity_main.xml 中

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="top.ttxxly.com.edittextdemo.MainActivity"
    android:orientation="vertical">

    <EditText
        android:layout_marginTop="140dp"
        android:layout_marginLeft="100dp"
        android:layout_marginRight="100dp"
        android:layout_marginBottom="10dp"
        android:id="@+id/et_user_name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="请输入用户名..."
        android:imeOptions="actionNext"
        android:inputType="text"
         />

    <EditText
        android:layout_marginTop="30dp"
        android:layout_marginLeft="100dp"
        android:layout_marginRight="100dp"
        android:layout_marginBottom="10dp"
        android:id="@+id/et_password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="请输入密码..."
        android:imeOptions="actionDone"
        android:inputType="textPassword"
        />
    <RelativeLayout
        android:layout_marginTop="30dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">
        <Button
            android:id="@+id/btn_login"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="100dp"
            android:text="登录"
            android:textSize="21sp"/>
        <Button
            android:id="@+id/btn_register"
            android:layout_marginRight="100dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:text="注册"
            android:textSize="21sp"/>
    </RelativeLayout>

</LinearLayout>

```

*注：inputType和imeOptions结合使用弹出输入法*

### 参考

* http://www.jianshu.com/p/5fe19793dd82