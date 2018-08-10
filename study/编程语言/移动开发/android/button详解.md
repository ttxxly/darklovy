[官方文档](https://developer.android.com/reference/android/widget/Button.html)

```
java.lang.Object
   ↳	android.view.View
 	   ↳	android.widget.TextView
 	 	   ↳	android.widget.Button
```

在 Android 开发中， Button是常用的控件，用起来也比较简单的。


### 1.在 Android 中 定义 Button 

* 在 xml 文件中定义
* 通过代码创建然后加入到界面中

两种实现的效果是一样的，大部分的时候我们一般在 xml 中定义， 简单方便， 层次分明。

### 2. Button 常见的属性以及相关的方法

(1) 设置是否允许点击

* xml 属性： `android:clickable`
* 相关方法：`setClickable(boolean clickable)`

(2) 设置背景色

* xml 属性： `android:background`
* 相关方法： `setBackgroundResource(int resid)`

通过资源文件设置背景色。

resid:资源xml文件ID 

按钮默认背景为android.R.drawable.btn_default
    
(3) 设置文字

* xml 属性： `android:text`	
* 相关方法： `setText(CharSequence text)`

(4) 设置文字颜色

* xml 属性： `android:textColor`
* 相关方法： `setTextColor(int color)`

(5) 设置点击事件

* xml 属性： `android:onClick`
* 相关方法： `setOnClickListener(OnClickListener l)`


### 3. button 点击事件

### 4. 小 Demo

在 activity_main.xml 中

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginLeft="10dp"
    android:orientation="vertical">

    <Button
        android:id="@+id/btn_click_one"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button点击事件写法1：使用内部类" />

    <Button
        android:id="@+id/btn_click_two"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="click"
        android:text="Button点击事件写法2:在XML文件中声明onClick属性" />

    <Button
        android:id="@+id/btn_click_three"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="click"
        android:text="Button点击事件写法3:匿名内部类" />

    <Button
        android:id="@+id/btn_click_four"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="click"
        android:text="Button点击事件写法4：Activity实现View.OnClickListener接口" />


    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:background="#000000"
        android:padding="10dp"
        android:text="Button设置背景：background"
        android:textColor="#ffffff" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:background="@drawable/shape_button_test"
        android:padding="10dp"
        android:text="Button设置shape" />


</LinearLayout>
```

在 MainActivity 中

```
package top.ttxxly.com.buttondemo;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        /**
         * 点击事件：使用内部类（很少用）
         * 步骤：
         *      1. findViewById 获取按钮
         *      2. 设置点击事件
         */
        Button btn_click_one = (Button) findViewById(R.id.btn_click_one);
        btn_click_one.setOnClickListener(new MyClickListener());

        /**
         * 点击事件： 匿名内部类
         * 适合场景：测试、或者只有单个button的时候。使用较多
         */
        Button btn_click_three = (Button) findViewById(R.id.btn_click_three);
        btn_click_three.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

            }
        });
    }

    /**
     * 点击事件：在XML文件中声明onClick属性（很少用）
     * @param view
     */
    public void click(View view) {
        switch (view.getId()) {
            case R.id.btn_click_two:
                Toast.makeText(this, "在XML文件中声明onClick属性", Toast.LENGTH_SHORT).show();
                break;
        }
    }

    private class MyClickListener implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            Toast.makeText(getApplicationContext(), "用内部类", Toast.LENGTH_SHORT).show();
        }
    }
}

```

在 res/drawable 中 设置 按钮的形状以及背景色

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">

    <!--     默认背景色 -->
    <solid android:color="#ffffff" />

    <!-- 边框 -->
    <stroke
        android:width="1dp"
        android:color="@android:color/black" />

    <!--     设置弧度 -->
    <corners android:radius="20dp" />
</shape>
```



### Button 开发中的一些注意事项

* Button 的 `setOnClickListener` 优先级比 xml 中 `android:onClick` 高，如果同时设置点击事件，只有 `setOnClickListener` 有效。




