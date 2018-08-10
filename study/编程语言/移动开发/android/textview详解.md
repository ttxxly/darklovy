[官方文档](https://developer.android.com/reference/android/widget/TextView.html)

```
java.lang.Object
   ↳	android.view.View
 	   ↳	android.widget.TextView
```

TextView直接继承了View， 它还是 EditText、 Button 两个UI组件类的父类。TextView的作用就是在界面上显示文本。

## 属性


```

android:autoLink    设置是否当文本为URL链接/email/电话号码/map时，文本显示为可点击的链接。
可选值(none/web/email/phone/map/all)  

android:autoText    
如果设置，将自动执行输入值的拼写纠正。
此处无效果，在显示输入法并输入的时候起作用。  

android:background：
控件的背景颜色，可以理解为填充整个控件的颜色，可以是图片哦

android:bufferType  
指定getText()方式取得的文本类别。
选项editable 类似于StringBuilder可追加字符，  
也就是说getText后可调用append方法设置文本内容。spannable 则可在给定的字符区域使用样式

android:capitalize  
设置英文字母大写类型。
此处无效果，需要弹出输入法才能看得到，参见EditView此属性说明。 

android:cursorVisible   设定光标为显示/隐藏，默认显示。  

android:digits  设置允许输入哪些字符。如“1234567890.+-*/%\n()” 

android:drawableBottom  
在text的下方输出一个drawable，如图片。
如果指定一个颜色的话会把text的背景设为该颜色，并且同时和background使用时覆盖后者。  

android:drawableLeft    在text的左边输出一个drawable，如图片。

android:drawablePadding 
设置text与drawable(图片)的间隔
与drawableLeft、drawableRight、drawableTop、drawableBottom一起使用.
可设置为负数，单独使用没有效果。 

android:drawableRight   在text的右边输出一个drawable，如图片。  

android:drawableTop 在text的正上方输出一个drawable，如图片。  

android:editable    设置是否可编辑。这里无效果，参见EditView。

android:editorExtras    设置文本的额外的输入数据。在EditView再讨论。 

android:ellipsize   
设置当文字过长时,该控件该如何显示。
有如下值设置：
”start”—–省略号显示在开头；
”end”——省略号显示在结尾；
”middle”—-省略号显示在中间；
”marquee” ——以跑马灯的方式显示(动画横向移动)  

android:freezesText 设置保存文本的内容以及光标的位置。参见：这里。  

android:gravity 设置文本位置，如设置成“center”，文本将居中显示。  

android:hint    
Text为空时显示的文字提示信息，可通过textColorHint设置提示信息的颜色。
此属性在EditView中使用，但是这里也可以用。  

android:id  
为该视图提供一个标识符名称
允许您稍后使用findViewById(r.idid)检索视图.

android:includeFontPadding  设置文本是否包含顶部和底部额外空白，默认为true。  

android:inputMethod 
为文本指定输入法，需要完全限定名（完整的包名）。
例如：com.google.android.inputmethod.pinyin，但是这里报错找不到。  

android:inputType   
设置文本的类型，用于帮助输入法显示合适的键盘类型。
在EditView中再详细说明，这里无效果。  

android:marqueeRepeatLimit  在ellipsize指定marquee的情况下，设置重复滚动的次数，当设置为marquee_forever时表示无限次。  

android:ems 设置TextView的宽度为N个字符的宽度。这里测试为一个汉字字符宽度

android:maxEms  设置TextView的宽度为最长为N个字符的宽度。与ems同时使用时覆盖ems选项。  

android:minEms  设置TextView的宽度为最短为N个字符的宽度。与ems同时使用时覆盖ems选项。  

android:maxLength   限制显示的文本长度，超出部分不显示。  

android:lines   设置文本的行数，设置两行就显示两行，即使第二行没有数据。  
android:maxLines    设置文本的最大显示行数，与width或者layout_width结合使用
超出部分自动换行，超出行数将不显示。  

android:minLines    设置文本的最小行数，与lines类似。

android:layout_width：
组件的宽度，一般写：wrap_content或者match_parent(fill_parent)
前者是控件显示的内容多大，控件就多大
后者会填满该控件所在的父容器；
当然也可以设置成特定的大小，比如 `20dp`

android:linksClickable  设置链接是否点击连接，即使设置了autoLink。 

android:lineSpacingExtra    设置行间距。  

android:lineSpacingMultiplier   设置行间距的倍数。如”1.2”  

android:password    以小点”.”显示文本  

android:phoneNumber 设置为电话号码的输入方式。  


android:scrollHorizontally  设置文本超出TextView的宽度的情况下，是否出现横拉条。

android:selectAllOnFocus    如果文本是可选择的，让他获取焦点而不是将光标移动为文本的开始位置或者末尾位置。TextView中设置后无效果。  

android:shadowColor 指定文本阴影的颜色，需要与shadowRadius一起使用。

android:shadowDx    设置阴影横向坐标开始位置。  

android:shadowDy    设置阴影纵向坐标开始位置。  

android:shadowRadius    设置阴影的半径。设置为0.1就变成字体的颜色了，一般设置为3.0的效果比较好。  
android:singleLine  设置单行显示。
如果和layout_width一起使用，当文本不能全部显示时，后面用“…”来表示。
如android:text="test_ singleLine " android:singleLine="true" android:layout_width="20dp"将只显示“t…”。
如果不设置singleLine或者设置为false，文本将自动换行  

android:text    
设置显示文本.  
一般我们是把字符串写到string.xml文件中，然后通过@String/xxx取得对应的字符串内容的

android:textColor   设置文本颜色 

android:textColorHighlight  被选中文字的底色，默认为蓝色  

android:textColorHint   设置提示信息文字的颜色，默认为灰色。与hint一起使用。  

android:textColorLink   文字链接的颜色.  

android:textScaleX 
设置文字之间间隔，默认为1.0f。分别设置0.5f/1.0f/1.5f/2.0f效果如下：  

android:textSize    设置文字大小，推荐度量单位”sp”，如”15sp”  

android:textStyle   
设置字形[bold(粗体) 0, italic(斜体) 1,
bolditalic(又粗又斜) 2] 可以设置一个或多个，用“|”隔开  

android:typeface    设置文本字体，必须是以下常量值之一：normal 0, sans 1, serif 2, monospace(等宽字体) 3]   

android:height  设置文本区域的高度，支持度量单位：px(像素)/dp/sp/in/mm(毫米)  

android:maxHeight   设置文本区域的最大高度  

android:minHeight   设置文本区域的最小高度  

android:width   
设置文本区域的宽度
支持度量单位：px(像素)/dp/sp/in/mm(毫米)，与layout_width的区别看这里。  

android:maxWidth    设置文本区域的最大宽度 

android:minWidth    设置文本区域的最小宽度
```

### 插入图片

```
android:drawableLeft
android:drawableTop
android:drawableRight
android:drawableBottom
```

### 阴影

```
android:shadowColor //指定文本阴影的颜色
android:shadowDx //设置阴影横向坐标开始位置
android:shadowDy //设置阴影纵向坐标开始位置
android:shadowRadius //设置阴影的半径。设置为0.1会变成字体的颜色
```

## 几个关于 textview 的小例子

写在一起的

![textViewDemo.png](http://okyfoew6j.bkt.clouddn.com/textViewDemo.png)

### 带阴影的TextView

在 activity_main.xml 中

```
<TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:shadowColor="#008844"
        android:shadowDx="8"
        android:shadowDy="8"
        android:shadowRadius="2"
        android:text="带阴影的TextView"
        android:textColor="#008844"
        android:textSize="30sp" />
```

### 圆角边框、渐变背景的 TextView

新建 txt_circleborder.xml 文件(圆形边框的样式)

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- 设置透明背景色 -->
    <solid android:color="#87CEEB" />

    <!-- 设置一个黑色边框 -->
    <stroke
        android:width="2px"
        android:color="#000000" />
    <!-- 设置四个圆角的半径 -->
    <corners
        android:bottomLeftRadius="10px"
        android:bottomRightRadius="10px"
        android:topLeftRadius="10px"
        android:topRightRadius="10px" />
    <!-- 设置一下边距,让空间大一点 -->
    <padding
        android:bottom="5dp"
        android:left="5dp"
        android:right="5dp"
        android:top="5dp" />

</shape>
```

新建 txt_rectborder.xml 文件（矩形边框的样式）

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >

    <!-- 设置一个黑色边框 -->
    <stroke android:width="2px" android:color="#000000"/>
    <!-- 渐变 -->
    <gradient
        android:angle="270"
        android:endColor="#C0C0C0"
        android:startColor="#FCD209" />
    <!-- 设置一下边距,让空间大一点 -->
    <padding
        android:left="5dp"
        android:top="5dp"
        android:right="5dp"
        android:bottom="5dp"/>

</shape>
```

在 activity_main.xml 中

```
<TextView
        android:id="@+id/txtOne"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:textSize="18sp"
        android:gravity="center"
        android:background="@drawable/txt_rectborder"
        android:text="矩形边框的TextView" />

    <TextView
        android:id="@+id/txtTwo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:textSize="18sp"
        android:gravity="center"
        android:layout_gravity="center_horizontal"
        android:background="@drawable/txt_circleborder"
        android:text="圆角边框的TextView" />
```

###  带图片(drawableXxx)的TextView：

在 activity_main.xml 中

```
<TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_marginTop="100dp"
        android:drawableTop="@mipmap/ic_launcher"
        android:drawableBottom="@mipmap/ic_launcher"
        android:drawableLeft="@mipmap/ic_launcher"
        android:drawableRight="@mipmap/ic_launcher"
        android:text="么么哒"
        android:gravity="center"
        />
```

*注：在xml文件中不能直接设置大小，可以使用代码修改*

### 参考

* http://www.runoob.com/w3cnote/android-tutorial-textview.html
* http://android.jobbole.com/83961/