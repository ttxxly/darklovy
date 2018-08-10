[官网文档](https://developer.android.com/reference/android/widget/ListView.html) 

ListView是一个能使数据集合以动态滚动的方式展示到用户的界面上的View.它专门用于处理那种内容元素很多，手机屏幕无法展示出所有的内容的情况。它使用列表的形式来展示内容，超出屏幕部分就通过手指滑动就可以移动到屏幕内了。

### Adapter

我们应该明白的是控件就是为了交互和展示数据的，而ListView只是为了展示很多很多的数据而设计的。由于它的数据源（数组、集合、数据库表的游标）多样性，我们不能为了每一种数据源去进行适配工作，所以ListView被设计成交互和展示用，而数据源则由 Adapter（适配器）承担，负责适配多种多样的数据源。Adapter是一个接口（interface），可以去实现各种各样的子类，子类通过自己的逻辑去完成特定的适配工作。

* ArrayAdapter：用于数组和List类型的数据源适配。
* SimpleCursorAdapter：用于游标类型的数据源适配。
* SimpleAdapter：用于绑定在XML中定义的控件对应数据
* BaseAdapter：通用的基础适配器

工作原理图：

![](http://img.blog.csdn.net/20150719202924532?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### ListView 使用 ArrayAdapter

在 activity_main.xml 中：

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="top.ttxxly.listview_arrayadapter_demo.MainActivity">

    <ListView
        android:id="@+id/main_lv"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</android.support.constraint.ConstraintLayout>
```

在 MainActivity.java 中：

```
public class MainActivity extends AppCompatActivity {

    private ListView lv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        lv = (ListView) findViewById(R.id.main_lv);

        //设置数据源
        List<String> s = new ArrayList<>();
        s.add("语文");
        s.add("数学");
        s.add("化学");
        s.add("英语");
        s.add("生物");
        s.add("历史");
        s.add("政治");

        //设置适配器
        /**
         * ArrayAdapter参数：
         *      1：context（上下文）
         *      2：用于填充ListView每行的layout资源ID
         *          * android.R.layout.simple_list_item_1 包含 TextView控件
         *          * android.R.layout.simple_list_item_checked 带选择框（需要设置单选或多选模式）
         *          * android.R.layout.simple_list_item_multiple_choice 带CheckBox (需要设置单选或多选模式）
         *          * android.R.layout.simple_list_item_single_choice 带RadioButton (需要设置单选或多选模式）
         *      3: 数据源
         */
        lv.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_single_choice, s));
        lv.setChoiceMode(ListView.CHOICE_MODE_SINGLE);//设置单选或者多选模式，否则没有选择效果
    }
}

```

小结：

（1）设置数据源

（2）实现ArrayAdapter的构造函数来创建一个ArrayAdapter的对象。

（3）通过 ListView 的 setAdapter() 方法来绑定ArrayAdapter。



### ListView 优化



### 参考链接

* http://blog.csdn.net/guolin_blog/article/details/44996879
* http://www.cnblogs.com/zhengbeibei/archive/2013/05/14/3078805.html