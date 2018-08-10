在 dimens.xml 中我们可以保存各种在 UI 布局中用到的尺寸，常用于做屏幕适配。

例子：

dimens.xml

```
<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="nav_header_vertical_spacing">16dp</dimen>
    <dimen name="nav_header_height">160dp</dimen>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    <dimen name="fab_margin">16dp</dimen>
</resources>
```

然后在布局文件中

```
android:paddingTop="@dimen/nav_header_vertical_spacing"
```

类似于 strings.xml 