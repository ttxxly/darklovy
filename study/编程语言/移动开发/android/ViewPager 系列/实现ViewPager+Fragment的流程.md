# viewpager 作用

ViewPager（android.support.v4.view.ViewPager）是android扩展包v4包中的类，这个类可以让用户左右切换当前的view，实现滑动切换的效果。

# 使用场景

* 引导页
* 页卡滑动（微信页面、网易新闻）
 
# 使用步骤

1. 自定义 MyViewPager 类 继承 ViewPager

在 MyVIewPager 类可以利用 反射机制 来控制Fragment的切换速度

2. 在 要显示ViewPager的界面.java 中实现 ViewPageAdapter 类继承 PageAdapter

提供一个 适配器 将我们需要显示的视图页填充在 ViewPager 中。

实现以下方法：

* getCount()    获取组件的数量
* isViewFromObject()
* destroyItem()     //滑动时销毁的组件
    * container.removeView(viewContainter.get(position));
* instantiateItem() //滑动时生成的组件
    * container.addView(viewContainter.get(position));
    * return viewContainter.get(position);
* getItemPosition() 可选

3. 实现对应视图页面的 XML 。

```
View pagerview1 = LayoutInflater.from(MainActivity.this).inflate(R.layout.pager_table, null);
```

4. 将 三者关联起来

```
//Set a PagerAdapter that will supply views for this pager as needed
viewpager.setAdapter(mAdapter);
mAdpater = new ViewPagerAdapter();

//在 ViewPagerAdapter 中来操作添加或删除视图，视图通过 viewContainter 管理
((ViewPager) container).removeView(viewContainter.get(position));
((ViewPager) container).addView(viewContainter.get(position));


private ArrayList<View> viewContainter = new ArrayList<View>();
//Adds the specified object at the end of this ArrayList
viewContainter.add(pagerview1);
viewContainter.add(pagerview2);
viewContainter.add(pagerview3);
viewContainter.add(pagerview4);
        
// get a View     
View pagerview1 = LayoutInflater.from(MainActivity.this).inflate(R.layout.pager_table, null);
View pagerview2 = LayoutInflater.from(MainActivity.this).inflate(R.layout.pager_table, null);
View pagerview3 = LayoutInflater.from(MainActivity.this).inflate(R.layout.pager_table, null);
View pagerview4 = LayoutInflater.from(MainActivity.this).inflate(R.layout.pager_table, null);

```