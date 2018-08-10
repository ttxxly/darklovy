作用：显示任意图片。可自定义显示尺寸，显示颜色等。

官方文档：http://developer.android.com/reference/android/widget/ImageView.html

### XML 属性

```
- android:adjustViewBounds 是否保持宽高比。需要与maxWidth、MaxHeight一起使用，单独使用没有效果。
- android:cropToPadding 是否截取指定区域用空白代替。单独设置无效果，需要与scrollY一起使用 
- android:maxHeight 定义View的最大高度，需要与AdjustViewBounds一起使用，单独使用没效果
- android:scaleType 决定了图片在View上的显示的样式，比如如何对图片进行缩放，显示图片整体还是部分，还是根据自己的需求进行相关显示。
```

#### ScaleType 属性

```
- martrix 不对图片进行缩放，对原图从 View 的左上角绘制图片（图片不变形）
- fitXY 将图片全部绘制到 View 中，但是图片会变形
- fitStart、fitCenter、fitEnd 三个属性会选择图片的较长边为基准对图片进行缩放处理（图片不变形，不能充满  View）
- center 不对图片进行缩放处理，选取 View 以及图片的中心点进行绘制。
- centerCrop 保证图片充满 View， 因此选取图片中较短的边为基准做缩放处理（图片不变形，做缩放处理）
- centerInside 保证图片显示在 View 中间，当图片大于 View 时，选取图片较长的边为基准对图片进行缩小，当图片宽高小于 View 时，直接将图片显示到 View 中间。（图片不变形）
```

#### 动态设置 ImageView 的图片源

```
来源1：drawable 文件夹
	setImageResource(R.drawable.xxx)
来源2：网址 url
	
```