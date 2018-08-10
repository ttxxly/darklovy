我们知道如果是通过网络加载图像，那么根据用户所处的网络环境，有可能会花费很多时间，才能成功展示图片。一个预期的行为是一个APP先去显示一张占位图知道这样图片加载处理完成。

我们已经道Glide的基本使用方式：先with(context)，再load(资源),最后into(目标ImageView). 如果需要占位图那么我们还要加上placeHolder(resource)

#### 用法

```
Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .into(imageViewPlaceholder);
```

## 错误占位符：.error()

假设我们的 App 尝试从一个网站去加载一张图片。Glide 给我们一个选项去获取一个错误的回调并采取合适的行动。我们会在后面来讨论，对现在来说，可能太复杂了。在大多数情况下使用占位符，来指明图片不能被加载已经足够了。

调用 Glide 的流式接口和之前显示预加载占位符的例子是相同的，不同的是调用了名为 `error()` 的函数。

```
Glide
    .with(context)
    .load("http://futurestud.io/non_existing_image.png")
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .error(R.mipmap.future_studio_launcher) // will be displayed if the image cannot be loaded
    .into(imageViewError);


```

就这样。如果你定义的 `load()` 值的图片不能被加载出来，Glide 会显示 `R.mipmap.future_studio_launcher` 作为替换。再说一次，`error()`接受的参数只能是已经初始化的 drawable 对象或者指明它的资源(`R.drawable.<drawable-keyword>`)。