[官方文档](https://developer.android.com/reference/android/view/View.html)

View 是用户接口的基础构件。View表示屏幕上的一块矩形区域，负责绘制这个区域和事件处理。


## View 的生命周期

![View-lifecycle.png](http://okyfoew6j.bkt.clouddn.com/View-lifecycle.png)

**自定义** View 周期中用到的方法

1. Creation(创建)：

使用View的构造函数进行创建，并处理有自定义的属性。
    
* onFinishInflate() 当View和他的子View全部从XML中inflate结束后


2. 布局(Layout)：

处理View的大小和位置相关的信息。

* onMesure()    计算每个控件在屏幕上的尺寸大小
* onLayout()    设置所有控件的大小和位置。
* onSizeChanged()   当View的大小改变会调用此方法。

3. 绘画（Drawing）：

* onDraw()  绘制 View

4. 事件处理（Event processing）：

* onKeyDown()   当设备的物理按键按下后会触发该方法
* onKeyUp()     当设备的物理按键弹起的时候就会触发该方法
* onTrackballEvent() 当轨迹球被触动的时候会触发该方法
* onTouchEvent()    当设备的屏幕有来自用户的触摸操作时会回调该法，比如某些滑动操作我们就可以在该方法中拦截处理，可以根据用户的不同滑动距离和滑动速度等用户操作，给出许多不同的反馈，提供更好的用户体验。

5. 焦点（Focus）

* onFocusChanged()  当控件的焦点发生改变，会触发该方法。

6. Attaching（附加）：

当View通过构造函数创建出来后，如果不挂载到Window上时，是无法显示出来的。

* onAttachedToWindow()  将 View 挂载到 Windows 上
* onDetachedFromWindow()    将 View 从 Windows 上移除
* onWindowVisibilityChanged() 当Window隐藏或者可见时会调用此方法

## Implementing a Custom View（实现一个自定义视图） 

1. 创建自定义View并复写构造方法
2. 自定义View的属性并使用
3. 在View的构造方法中获得我们自定义的属性 
4. 添加设置属性事件
5. 重写onMesure(可以不写) 
6. 重写onDraw
7. 与用户交互

### 创建自定义View并复写构造方法

继承View或继承View的派生子类

默认情况下会有三个构造函数：

```
public void CustomView(Context context) {}
public void CustomView(Context context, AttributeSet attrs) {}
public void CustomView(Context context, AttributeSet attrs, int defStyle) {}
```

第一种构造方法：用在代码中动态创建对象时使用的，如果只打算在代码中动态创建一个view而不使用布局文件xml，那么就直接实现这个构造方法就可以了(一般项目代码会比较庞大不推荐使用)

第二种构造方法：用于通过布局文件xml创建一个view时。因为XML标签中所有的属性都从资源包中读取出来并作为一个AttributeSet，然后传给构造方法。

第三种构造方法：相较于第二种多了一个参数defStyle，这个参数用来指定view的默认style，如果为0将不会应用任何默认的style。这个参数一般系统是不调用的，一般用于提供给第二个构造方法使用，在第二个构造方法中会传给第三个构造方法一个默认的style id。


### 自定义View的属性并使用

在 res/values/attrs.xml ：
在资源元素 `<declare-styleable>` 中为您的view定义自定义属性。

例子：

```
<declare-styleable name="PieChart">
       <attr name="showText" format="boolean" />
       <attr name="labelPosition" format="enum">
           <enum name="left" value="0"/>
           <enum name="right" value="1"/>
       </attr>
   </declare-styleable>
```
在 XML 文件中指定指定属性的值：

```
 <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:custom="http://schemas.android.com/apk/res/com.example.customviews">
 <com.example.customviews.charting.PieChart
     custom:showText="true"
     custom:labelPosition="left" />
</LinearLayout>
```

自定义属性可以像内建属性一样使用它们。唯一不同是自定义属性属于不同的命名空间。固定写法就是http://schemas.android.com/apk/res/你的包名。比如我的就是： `xmlns:custom="http://schemas.android.com/apk/res/com.example.customviews">`

### 获取自定义属性

当view从XML布局中创建了之后，XML标签中所有的属性都从资源包中读取出来并作为一个AttributeSet传递给view的构造函数.

固定的获取自定义属性代码:

```
public PieChart(Context context, AttributeSet attrs) {
   super(context, attrs);
   TypedArray a = context.getTheme().obtainStyledAttributes(
        attrs,
        R.styleable.PieChart,
        0, 0);

   try {
       mShowText = a.getBoolean(R.styleable.PieChart_showText, false);
       mTextPos = a.getInteger(R.styleable.PieChart_labelPosition, 0);
   } finally {
       a.recycle();
   }
}
```

通过调用Context的obtainStyledAttributes()方法返回一个TypedArray对象。然后直接用TypedArray对象获取自定义属性的值。 
由于TypedArray对象是共享的资源，所以在获取完值之后必须要调用recycle()方法来回收。

### 添加设置属性的方法

在xml中指定的自定义属性只有在view被初始化的时候能够获取到，有时候我们可能在运行时做一些操作，这种情况就需要我们为自定义属性设置getter和setter方法

```
public boolean isShowText() {
   return mShowText;
}

public void setShowText(boolean showText) {
   mShowText = showText;
   invalidate();
   requestLayout();
}
```

调用invalidate()方法让系统去调用view的onDraw()重新绘制.调用requestLayout()来请求测量获取一个新的布局位置.


### 重写onMesure

**系统帮我们测量的高度和宽度都是 `MATCH_PARNET`**  

* 设置明确的宽度和高度，系统测量结果就是我们设置的结果 
* 设置为 `WRAP_CONTENT` 或者 `MATCH_PARENT` 系统测量结果是 `MATCH_PARENT`

**我们需要自己测量的时候就需要重写 `onMeasure()` 方法**

重写之前先了解MeasureSpec的specMode,一共三种类型：

* EXACTLY：一般是设置了明确的值或者是MATCH_PARENT
* AT_MOST：表示子布局限制在一个最大值内，一般为WARP_CONTENT
* UNSPECIFIED：表示子布局想要多大就多大，很少使用

下面是重写 OnMesure() 代码：

```
@Override  
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec)  
{  
    int widthMode = MeasureSpec.getMode(widthMeasureSpec);  
    int widthSize = MeasureSpec.getSize(widthMeasureSpec);  
    int heightMode = MeasureSpec.getMode(heightMeasureSpec);  
    int heightSize = MeasureSpec.getSize(heightMeasureSpec);  
    int width;  
    int height ;  
    if (widthMode == MeasureSpec.EXACTLY)  
    {  
        width = widthSize;  
    } else  
    {  
        mPaint.setTextSize(mTitleTextSize);  
        mPaint.getTextBounds(mTitle, 0, mTitle.length(), mBounds);  
        float textWidth = mBounds.width();  
        int desired = (int) (getPaddingLeft() + textWidth + getPaddingRight());  
        width = desired;  
    }  
  
    if (heightMode == MeasureSpec.EXACTLY)  
    {  
        height = heightSize;  
    } else  
    {  
        mPaint.setTextSize(mTitleTextSize);  
        mPaint.getTextBounds(mTitle, 0, mTitle.length(), mBounds);  
        float textHeight = mBounds.height();  
        int desired = (int) (getPaddingTop() + textHeight + getPaddingBottom());  
        height = desired;  
    }  
      
      
  
    setMeasuredDimension(width, height);  
}  
```

### 重写OnDraw方法

一旦自定义控件被创建并且测量代码写好之后，接下来你就可以实现onDraw()来绘制View了。

原型：`void onDraw (Canvas canvas)`

简单的理解就是：
* Canvas处理画什么
* Paint处理怎么画

Canvas定义你可以在屏幕上画的形状,而Paint为你画的每个形状定义颜色、样式、字体等等.

### 与用户交互

我们需要记住这里是处理触摸事件的入口。

```
@Override
public boolean onTouchEvent(MotionEvent event) {
    return super.onTouchEvent(event);
}
```

这部分涉及知识还有很多， 我们会在之后的文章中讲解。

## 参考资料

* http://tedyin.me/2015/03/11/android-view-lifecycle/
* https://developer.android.com/reference/android/view/View.html
* https://hackernoon.com/android-draw-a-custom-view-ef79fe2ff54b
* http://www.jianshu.com/p/08e6dab7886e
* http://www.jianshu.com/p/7c1ed00989a9
* http://blog.csdn.net/lmj623565791/article/details/24252901
* http://tbfungeek.github.io/2016/04/24/Android-%E8%BF%9B%E9%98%B6%E4%B9%8B%E8%87%AA%E5%AE%9A%E4%B9%89View/
