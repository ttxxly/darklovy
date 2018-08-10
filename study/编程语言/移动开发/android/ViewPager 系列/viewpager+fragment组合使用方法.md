# 步骤

* xml 文件中定义
* 自定义 ViewPager（可选 ）
* 自定义 Adapter

## 1. 定义 xml 文件

## 2. 自定义 viewpager

```java

import android.content.Context;
import android.support.v4.view.ViewPager;
import android.util.AttributeSet;
import android.view.animation.AccelerateDecelerateInterpolator;
import android.view.animation.Interpolator;
import android.widget.Scroller;
import java.lang.reflect.Field;

public class MyViewPager extends ViewPager {

    public MyViewPager(Context context) {
        super(context);
        init(context);
    }

    public MyViewPager(Context context, AttributeSet attrs) {
        super(context, attrs);
        init(context);
    }

    private void init(Context context) {
        /**
         * ViewPager的惯性效果（滑到一定距离自动平滑到另一个pager，或者调用setCurrentItem）是通过scroller来实现的.
         * 其中有个变量为mScroller，为了修改这个滑动的速度，需要改变mScroller的一些值.
         * 但是mScroller是私有变量，所以在不直接修改ViewPager源码的情况下，只能用 反射 修改 mScroller。
         */
        try {
            Field field = ViewPager.class.getDeclaredField("mScroller");
            field.setAccessible(true);
            setSpeedScroller scroller = new setSpeedScroller(context,
                    new AccelerateDecelerateInterpolator());
            field.set(this, scroller);
            scroller.setmDuration(2000);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * 设置切换滑动速度
     */
    public class setSpeedScroller extends Scroller {
        private int mDuration = 20000;

        public setSpeedScroller(Context context) {
            super(context);
        }

        public setSpeedScroller(Context context, Interpolator interpolator) {
            super(context, interpolator);
        }

        @Override
        public void startScroll(int startX, int startY, int dx, int dy, int duration) {
            super.startScroll(startX, startY, dx, dy, mDuration);
        }

        @Override
        public void startScroll(int startX, int startY, int dx, int dy) {
            super.startScroll(startX, startY, dx, dy, mDuration);
        }

        public void setmDuration(int time) {
            mDuration = time;
        }

        public int getmDuration() {
            return mDuration;
        }
    }
}

```
## 3. 初始化数据，并将布局填充到 viewpag 中

## FragmentStatePagerAdapter 和 FragmentPagerAdapter 

PageAdapter 是 FragmentPagerAdapter 以及 FragmentStatePagerAdapter 的基类。

* FragmentPagerAdapter使用时，每一个生成的 Fragment 都将保存在内存之中。
* FragmentStatePagerAdapter只保留了当前显示的Fragment，其他划过的Fragment离开视线后，就会被销毁；而在页面需要显示时，再生成新的实例，当拥有大量的页面时，不必在内存中占用大量的内存。


## 关于普通 activity 是否可以内嵌 Fragment 问题

**普通Activity是可以内嵌Fragment的！！！！**

Fragment分为app包下和v4包下的。

* v4包是为了向下兼容（3.0之前没有Fragment），如果使用了v4包下的Fragemnt，则必须继承FragmentActivity,其他Fragment也要使用v4包下的，获取Fragment管理器的方法是 getSupportFragmentManager()。

* app包下的Fragment，则直接继承 Activity 即可，其他 Fragment 也用app包下的，获取 Fragment 管理器的方法是 getFragmentManager()。