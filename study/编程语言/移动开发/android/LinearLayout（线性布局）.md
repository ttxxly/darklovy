[官方文档](https://developer.android.com/reference/android/widget/LinearLayout.html)

[Linear Layout guide](https://developer.android.com/guide/topics/ui/layout/linear.html)


```
java.lang.Object
   ↳	android.view.View
 	   ↳	android.view.ViewGroup
 	 	   ↳	android.widget.LinearLayout
```

这个布局会将它所包含的组件在线性方向上依次排列。

### 常用属性

由于官方文档上包含了所有的属性，这里我只介绍几个常用的属性。

* `android:orientation` 设置布局管理器内组件的排列方式。
    *  horizontal： 设置水平排列
    *  vertical： 设置垂直排列（默认值）
    
* `android:gravity` 控制组件所包含的子元素的对齐方式可多个组合（left| top）

* `android:layout_gravity`  控制该组件在父容器那里的对其方式。
关于 `android:layout_gravity` 的官方文档： [戳我](https://developer.android.com/reference/android/widget/LinearLayout.LayoutParams.html#attr_android:layout_gravity)

* `android:layout_width` 控制布局的宽度，通常不写数字，有以下的参数
    * wrap_content  填充组件的实际大小，刚刚好包裹内容。
    * match_parent  填充满父容器
    
* `android:layout_height` 控制组件的高度，参数同上。

* `android:id` 为该组件设置唯一标识,可任意设置，比如 "bt_search" ，只有这样我们才能在java中通过 `findViewById(R.id.bt_search)` 找到该组件。

* `android:background` 设置背景，可以用图片，也可以直接用颜色。

* `android:weight`  权重，该属性是用来按比例划分区域的。


### Android 距离单位

*   px(像素): 每个 px 对应屏幕上的一个点
*   dip或dp(设备独立像素): 一种基于屏幕密度的抽象单位。在每英寸 160 点的显示器上, 1 dip = 1 px. 但随着屏幕密度的改变， dip 和 px 的对应关系会发生相应的改变。
*   sp(比例像素): 主要处理字体的大小， 可以根据用户的字体大小首选项进行缩放。
*   in(英寸): 标准长度单位
*   mm(毫米): 标准长度单位
*   pt(榜): 标准长度单位， 1/72 英寸

**大部分情况下：（组件长度： dp， 字体大小： sp）**

**当屏幕密度是160时： 160sp=160dip=1in=72pt**

### 注意事项

当 `android:orientation="vertical"` 时:

只有水平方向的设置才起作用，垂直方向的设置不起作用。  
即：`left，right，center_horizontal` 是生效的。 

当 `android:orientation="horizontal"` 时:

只有垂直方向的设置才起作用，水平方向的设置不起作用。  
即：`top，bottom，center_vertical` 是生效的。



