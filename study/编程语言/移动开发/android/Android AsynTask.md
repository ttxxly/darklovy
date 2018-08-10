在Android中实现异步任务机制有两种方式，Handler和AsyncTask。

Handler模式需要为每一个任务创建一个新的线程，任务完成后通过Handler实例向UI线程发送消息，完成界面的更新，这种方式对于整个过程的控制比较精细，但也是有缺点的，例如代码相对臃肿，在多个任务同时执行时，不易对线程进行精确的控制。[关于Handler的相关知识](http://blog.csdn.net/liuhe688/archive/2011/05/09/6407225.aspx)，前面也有所介绍，不清楚的朋友们可以参照一下。

为了简化操作，Android1.5提供了工具类android.os.AsyncTask，它使创建异步任务变得更加简单，不再需要编写任务线程和Handler实例即可完成相同的任务。

先来看看AsyncTask的定义：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. public abstract class AsyncTask<Params, Progress, Result> {  

三种泛型类型分别代表“启动任务执行的输入参数”、“后台任务执行的进度”、“后台计算结果的类型”。在特定场合下，并不是所有类型都被使用，如果没有被使用，可以用java.lang.Void类型代替。

一个异步任务的执行一般包括以下几个步骤：

1.**execute(Params... params)**，执行一个异步任务，需要我们在代码中调用此方法，触发异步任务的执行。

2.**onPreExecute()**，在execute(Params... params)被调用后立即执行，一般用来在执行后台任务前对UI做一些标记。

3.**doInBackground(Params... params)**，在onPreExecute()完成后立即执行，用于执行较为费时的操作，此方法将接收输入参数和返回计算结果。在执行过程中可以调用publishProgress(Progress... values)来更新进度信息。

4.**onProgressUpdate(Progress... values)**，在调用publishProgress(Progress... values)时，此方法被执行，直接将进度信息更新到UI组件上。

5.**onPostExecute(Result result)**，当后台操作结束时，此方法将会被调用，计算结果将做为参数传递到此方法中，直接将结果显示到UI组件上。

在使用的时候，有几点需要格外注意：

1.异步任务的实例必须在UI线程中创建。

2.execute(Params... params)方法必须在UI线程中调用。

3.不要手动调用onPreExecute()，doInBackground(Params... params)，onProgressUpdate(Progress... values)，onPostExecute(Result result)这几个方法。

4.不能在doInBackground(Params... params)中更改UI组件的信息。

5.一个任务实例只能执行一次，如果执行第二次将会抛出异常。

接下来，我们来看看如何使用AsyncTask执行异步任务操作，我们先建立一个项目，结构如下：

![img](http://hi.csdn.net/attachment/201106/14/0_1308048004A27R.gif)

结构相对简单一些，让我们先看看MainActivity.java的代码：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. package com.scott.async;  
2.   
3. import java.io.ByteArrayOutputStream;  
4. import java.io.InputStream;  
5.   
6. import org.apache.http.HttpEntity;  
7. import org.apache.http.HttpResponse;  
8. import org.apache.http.HttpStatus;  
9. import org.apache.http.client.HttpClient;  
10. import org.apache.http.client.methods.HttpGet;  
11. import org.apache.http.impl.client.DefaultHttpClient;  
12.   
13. import android.app.Activity;  
14. import android.os.AsyncTask;  
15. import android.os.Bundle;  
16. import android.util.Log;  
17. import android.view.View;  
18. import android.widget.Button;  
19. import android.widget.ProgressBar;  
20. import android.widget.TextView;  
21.   
22. public class MainActivity extends Activity {  
23.   
24. ​    private static final String TAG = "ASYNC_TASK";  
25.   
26. ​    private Button execute;  
27. ​    private Button cancel;  
28. ​    private ProgressBar progressBar;  
29. ​    private TextView textView;  
30.   
31. ​    private MyTask mTask;  
32.   
33. ​    @Override  
34. ​    public void onCreate(Bundle savedInstanceState) {  
35. ​        super.onCreate(savedInstanceState);  
36. ​        setContentView(R.layout.main);  
37.   
38. ​        execute = (Button) findViewById(R.id.execute);  
39. ​        execute.setOnClickListener(new View.OnClickListener() {  
40. ​            @Override  
41. ​            public void onClick(View v) {  
42. ​                //注意每次需new一个实例,新建的任务只能执行一次,否则会出现异常  
43. ​                mTask = new MyTask();  
44. ​                mTask.execute("http://www.baidu.com");  
45.   
46. ​                execute.setEnabled(false);  
47. ​                cancel.setEnabled(true);  
48. ​            }  
49. ​        });  
50. ​        cancel = (Button) findViewById(R.id.cancel);  
51. ​        cancel.setOnClickListener(new View.OnClickListener() {  
52. ​            @Override  
53. ​            public void onClick(View v) {  
54. ​                //取消一个正在执行的任务,onCancelled方法将会被调用  
55. ​                mTask.cancel(true);  
56. ​            }  
57. ​        });  
58. ​        progressBar = (ProgressBar) findViewById(R.id.progress_bar);  
59. ​        textView = (TextView) findViewById(R.id.text_view);  
60.   
61. ​    }  
62.   
63. ​    private class MyTask extends AsyncTask<String, Integer, String> {  
64. ​        //onPreExecute方法用于在执行后台任务前做一些UI操作  
65. ​        @Override  
66. ​        protected void onPreExecute() {  
67. ​            Log.i(TAG, "onPreExecute() called");  
68. ​            textView.setText("loading...");  
69. ​        }  
70.   
71. ​        //doInBackground方法内部执行后台任务,不可在此方法内修改UI  
72. ​        @Override  
73. ​        protected String doInBackground(String... params) {  
74. ​            Log.i(TAG, "doInBackground(Params... params) called");  
75. ​            try {  
76. ​                HttpClient client = new DefaultHttpClient();  
77. ​                HttpGet get = new HttpGet(params[0]);  
78. ​                HttpResponse response = client.execute(get);  
79. ​                if (response.getStatusLine().getStatusCode() == HttpStatus.SC_OK) {  
80. ​                    HttpEntity entity = response.getEntity();  
81. ​                    InputStream is = entity.getContent();  
82. ​                    long total = entity.getContentLength();  
83. ​                    ByteArrayOutputStream baos = new ByteArrayOutputStream();  
84. ​                    byte[] buf = new byte[1024];  
85. ​                    int count = 0;  
86. ​                    int length = -1;  
87. ​                    while ((length = is.read(buf)) != -1) {  
88. ​                        baos.write(buf, 0, length);  
89. ​                        count += length;  
90. ​                        //调用publishProgress公布进度,最后onProgressUpdate方法将被执行  
91. ​                        publishProgress((int) ((count / (float) total) * 100));  
92. ​                        //为了演示进度,休眠500毫秒  
93. ​                        Thread.sleep(500);  
94. ​                    }  
95. ​                    return new String(baos.toByteArray(), "gb2312");  
96. ​                }  
97. ​            } catch (Exception e) {  
98. ​                Log.e(TAG, e.getMessage());  
99. ​            }  
100. ​            return null;  
101. ​        }  
102.   
103. ​        //onProgressUpdate方法用于更新进度信息  
104. ​        @Override  
105. ​        protected void onProgressUpdate(Integer... progresses) {  
106. ​            Log.i(TAG, "onProgressUpdate(Progress... progresses) called");  
107. ​            progressBar.setProgress(progresses[0]);  
108. ​            textView.setText("loading..." + progresses[0] + "%");  
109. ​        }  
110.   
111. ​        //onPostExecute方法用于在执行完后台任务后更新UI,显示结果  
112. ​        @Override  
113. ​        protected void onPostExecute(String result) {  
114. ​            Log.i(TAG, "onPostExecute(Result result) called");  
115. ​            textView.setText(result);  
116.   
117. ​            execute.setEnabled(true);  
118. ​            cancel.setEnabled(false);  
119. ​        }  
120.   
121. ​        //onCancelled方法用于在取消执行中的任务时更改UI  
122. ​        @Override  
123. ​        protected void onCancelled() {  
124. ​            Log.i(TAG, "onCancelled() called");  
125. ​            textView.setText("cancelled");  
126. ​            progressBar.setProgress(0);  
127.   
128. ​            execute.setEnabled(true);  
129. ​            cancel.setEnabled(false);  
130. ​        }  
131. ​    }  
132. }  

布局文件main.xml代码如下：

**[html]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. <?xml version="1.0" encoding="utf-8"?>  
2. <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
3. ​    android:orientation="vertical"  
4. ​    android:layout_width="fill_parent"  
5. ​    android:layout_height="fill_parent">  
6. ​    <Button  
7. ​        android:id="@+id/execute"  
8. ​        android:layout_width="fill_parent"  
9. ​        android:layout_height="wrap_content"  
10. ​        android:text="execute"/>  
11. ​    <Button  
12. ​        android:id="@+id/cancel"  
13. ​        android:layout_width="fill_parent"  
14. ​        android:layout_height="wrap_content"  
15. ​        android:enabled="false"  
16. ​        android:text="cancel"/>  
17. ​    <ProgressBar   
18. ​        android:id="@+id/progress_bar"   
19. ​        android:layout_width="fill_parent"   
20. ​        android:layout_height="wrap_content"   
21. ​        android:progress="0"  
22. ​        android:max="100"  
23. ​        style="?android:attr/progressBarStyleHorizontal"/>  
24. ​    <ScrollView  
25. ​        android:layout_width="fill_parent"   
26. ​        android:layout_height="wrap_content">  
27. ​        <TextView  
28. ​            android:id="@+id/text_view"  
29. ​            android:layout_width="fill_parent"   
30. ​            android:layout_height="wrap_content"/>  
31. ​    </ScrollView>  
32. </LinearLayout>  

因为需要访问网络，所以我们还需要在AndroidManifest.xml中加入访问网络的权限：

**[html]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. <uses-permission android:name="android.permission.INTERNET"/>  

我们来看一下运行时的界面：

![img](http://hi.csdn.net/attachment/201106/14/0_13080489541W1Z.gif)![img](http://hi.csdn.net/attachment/201106/14/0_13080489733363.gif)

![img](http://hi.csdn.net/attachment/201106/14/0_1308048991Z5Tt.gif)![img](http://hi.csdn.net/attachment/201106/14/0_1308049389SZzs.gif)

以上几个截图分别是初始界面、执行异步任务时界面、执行成功后界面、取消任务后界面。执行成功后，整个过程日志打印如下：

![img](http://hi.csdn.net/attachment/201106/14/0_1308049139BtIC.gif)

如果我们在执行任务时按下了“cancel”按钮，日志打印如下：

![img](http://hi.csdn.net/attachment/201106/14/0_1308049210lt0u.gif)

可以看到onCancelled()方法将会被调用，onPostExecute(Result result)方法将不再被调用。

上面介绍了AsyncTask的基本应用，有些朋友也许会有疑惑，AsyncTask内部是怎么执行的呢，它执行的过程跟我们使用Handler又有什么区别呢？答案是：AsyncTask是对Thread+Handler良好的封装，在android.os.AsyncTask代码里仍然可以看到Thread和Handler的踪迹。下面就向大家详细介绍一下AsyncTask的执行原理。

我们先看一下AsyncTask的大纲视图：

![img](http://hi.csdn.net/attachment/201106/13/0_13079649384Zjf.gif)

我们可以看到关键几个步骤的方法都在其中，doInBackground(Params... params)是一个抽象方法，我们继承AsyncTask时必须覆写此方法；onPreExecute()、onProgressUpdate(Progress... values)、onPostExecute(Result result)、onCancelled()这几个方法体都是空的，我们需要的时候可以选择性的覆写它们；publishProgress(Progress... values)是final修饰的，不能覆写，只能去调用，我们一般会在doInBackground(Params... params)中调用此方法；另外，我们可以看到有一个Status的枚举类和getStatus()方法，Status枚举类代码段如下：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. //初始状态  
2. private volatile Status mStatus = Status.PENDING;  
3.   
4. public enum Status {  
5. ​    /** 
6. ​     * Indicates that the task has not been executed yet. 
7. ​     */  
8. ​    PENDING,  
9. ​    /** 
10. ​     * Indicates that the task is running. 
11. ​     */  
12. ​    RUNNING,  
13. ​    /** 
14. ​     * Indicates that {@link AsyncTask#onPostExecute} has finished. 
15. ​     */  
16. ​    FINISHED,  
17. }  
18.   
19. /** 
20.  * Returns the current status of this task. 
21.  * 
22.  * @return The current status. 
23.  */  
24. public final Status getStatus() {  
25. ​    return mStatus;  
26. }  

可以看到，AsyncTask的初始状态为PENDING，代表待定状态，RUNNING代表执行状态，FINISHED代表结束状态，这几种状态在AsyncTask一次生命周期内的很多地方被使用，非常重要。

介绍完大纲视图相关内容之后，接下来，我们会从execute(Params... params)作为入口，重点分析一下AsyncTask的执行流程，我们来看一下execute(Params... params)方法的代码段：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. public final AsyncTask<Params, Progress, Result> execute(Params... params) {  
2. ​    if (mStatus != Status.PENDING) {  
3. ​        switch (mStatus) {  
4. ​            case RUNNING:  
5. ​                //如果该任务正在被执行则抛出异常  
6. ​                //值得一提的是,在调用cancel取消任务后,状态仍未RUNNING  
7. ​                throw new IllegalStateException("Cannot execute task:"  
8. ​                        + " the task is already running.");  
9. ​            case FINISHED:  
10. ​                //如果该任务已经执行完成则抛出异常  
11. ​                throw new IllegalStateException("Cannot execute task:"  
12. ​                        + " the task has already been executed "  
13. ​                        + "(a task can be executed only once)");  
14. ​        }  
15. ​    }  
16.   
17. ​    //改变状态为RUNNING  
18. ​    mStatus = Status.RUNNING;  
19.   
20. ​    //调用onPreExecute方法  
21. ​    onPreExecute();  
22.   
23. ​    mWorker.mParams = params;  
24. ​    sExecutor.execute(mFuture);  
25.   
26. ​    return this;  
27. }  

代码中涉及到三个陌生的变量：mWorker、sExecutor、mFuture，我们也会看一下他们的庐山真面目：

关于sExecutor，它是java.util.concurrent.ThreadPoolExecutor的实例，用于管理线程的执行。代码如下：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. private static final int CORE_POOL_SIZE = 5;  
2. private static final int MAXIMUM_POOL_SIZE = 128;  
3. private static final int KEEP_ALIVE = 10;  
4.   
5. //新建一个队列用来存放线程  
6. private static final BlockingQueue<Runnable> sWorkQueue =  
7. ​        new LinkedBlockingQueue<Runnable>(10);  
8. //新建一个线程工厂  
9. private static final ThreadFactory sThreadFactory = new ThreadFactory() {  
10. ​    private final AtomicInteger mCount = new AtomicInteger(1);  
11. ​    //新建一个线程  
12. ​    public Thread newThread(Runnable r) {  
13. ​        return new Thread(r, "AsyncTask #" + mCount.getAndIncrement());  
14. ​    }  
15. };  
16. //新建一个线程池执行器,用于管理线程的执行  
17. private static final ThreadPoolExecutor sExecutor = new ThreadPoolExecutor(CORE_POOL_SIZE,  
18. ​        MAXIMUM_POOL_SIZE, KEEP_ALIVE, TimeUnit.SECONDS, sWorkQueue, sThreadFactory);  

mWorker实际上是AsyncTask的一个的抽象内部类的实现对象实例，它实现了Callable<Result>接口中的call()方法，代码如下：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. private static abstract class WorkerRunnable<Params, Result> implements Callable<Result> {  
2. ​    Params[] mParams;  
3. }  

而mFuture实际上是java.util.concurrent.FutureTask的实例，下面是它的FutureTask类的相关信息：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. /** 
2.  * A cancellable asynchronous computation. 
3.  * ... 
4.  */  
5. public class FutureTask<V> implements RunnableFuture<V> {  

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. public interface RunnableFuture<V> extends Runnable, Future<V> {  
2. ​    /** 
3. ​     * Sets this Future to the result of its computation 
4. ​     * unless it has been cancelled. 
5. ​     */  
6. ​    void run();  
7. }  

可以看到FutureTask是一个可以中途取消的用于异步计算的类。

下面是mWorker和mFuture实例在AsyncTask中的体现：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. private final WorkerRunnable<Params, Result> mWorker;  
2. private final FutureTask<Result> mFuture;  
3.   
4. public AsyncTask() {  
5. ​    mWorker = new WorkerRunnable<Params, Result>() {  
6. ​        //call方法被调用后,将设置优先级为后台级别,然后调用AsyncTask的doInBackground方法  
7. ​        public Result call() throws Exception {  
8. ​            Process.setThreadPriority(Process.THREAD_PRIORITY_BACKGROUND);  
9. ​            return doInBackground(mParams);  
10. ​        }  
11. ​    };  
12.   
13. ​    //在mFuture实例中,将会调用mWorker做后台任务,完成后会调用done方法  
14. ​    mFuture = new FutureTask<Result>(mWorker) {  
15. ​        @Override  
16. ​        protected void done() {  
17. ​            Message message;  
18. ​            Result result = null;  
19.   
20. ​            try {  
21. ​                result = get();  
22. ​            } catch (InterruptedException e) {  
23. ​                android.util.Log.w(LOG_TAG, e);  
24. ​            } catch (ExecutionException e) {  
25. ​                throw new RuntimeException("An error occured while executing doInBackground()",  
26. ​                        e.getCause());  
27. ​            } catch (CancellationException e) {  
28. ​                //发送取消任务的消息  
29. ​                message = sHandler.obtainMessage(MESSAGE_POST_CANCEL,  
30. ​                        new AsyncTaskResult<Result>(AsyncTask.this, (Result[]) null));  
31. ​                message.sendToTarget();  
32. ​                return;  
33. ​            } catch (Throwable t) {  
34. ​                throw new RuntimeException("An error occured while executing "  
35. ​                        + "doInBackground()", t);  
36. ​            }  
37.   
38. ​            //发送显示结果的消息  
39. ​            message = sHandler.obtainMessage(MESSAGE_POST_RESULT,  
40. ​                    new AsyncTaskResult<Result>(AsyncTask.this, result));  
41. ​            message.sendToTarget();  
42. ​        }  
43. ​    };  
44. }  

我们看到上面的代码中，mFuture实例对象的done()方法中，如果捕捉到了CancellationException类型的异常，则发送一条“MESSAGE_POST_CANCEL”的消息；如果顺利执行，则发送一条“MESSAGE_POST_RESULT”的消息，而消息都与一个sHandler对象关联。这个sHandler实例实际上是AsyncTask内部类InternalHandler的实例，而InternalHandler正是继承了Handler，下面我们来分析一下它的代码：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. private static final int MESSAGE_POST_RESULT = 0x1; //显示结果  
2. private static final int MESSAGE_POST_PROGRESS = 0x2;   //更新进度  
3. private static final int MESSAGE_POST_CANCEL = 0x3; //取消任务  
4.   
5. private static final InternalHandler sHandler = new InternalHandler();  
6.   
7. private static class InternalHandler extends Handler {  
8. ​    @SuppressWarnings({"unchecked", "RawUseOfParameterizedType"})  
9. ​    @Override  
10. ​    public void handleMessage(Message msg) {  
11. ​        AsyncTaskResult result = (AsyncTaskResult) msg.obj;  
12. ​        switch (msg.what) {  
13. ​            case MESSAGE_POST_RESULT:  
14. ​                // There is only one result  
15. ​                //调用AsyncTask.finish方法  
16. ​                result.mTask.finish(result.mData[0]);  
17. ​                break;  
18. ​            case MESSAGE_POST_PROGRESS:  
19. ​                //调用AsyncTask.onProgressUpdate方法  
20. ​                result.mTask.onProgressUpdate(result.mData);  
21. ​                break;  
22. ​            case MESSAGE_POST_CANCEL:  
23. ​                //调用AsyncTask.onCancelled方法  
24. ​                result.mTask.onCancelled();  
25. ​                break;  
26. ​        }  
27. ​    }  
28. }  

我们看到，在处理消息时，遇到“MESSAGE_POST_RESULT”时，它会调用AsyncTask中的finish()方法，我们来看一下finish()方法的定义：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. private void finish(Result result) {  
2. ​    if (isCancelled()) result = null;  
3. ​    onPostExecute(result);  //调用onPostExecute显示结果  
4. ​    mStatus = Status.FINISHED;  //改变状态为FINISHED  
5. }  

原来finish()方法是负责调用onPostExecute(Result result)方法显示结果并改变任务状态的啊。

另外，在mFuture对象的done()方法里，构建一个消息时，这个消息包含了一个AsyncTaskResult类型的对象，然后在sHandler实例对象的handleMessage(Message msg)方法里，使用下面这种方式取得消息中附带的对象：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. AsyncTaskResult result = (AsyncTaskResult) msg.obj;  

这个AsyncTaskResult究竟是什么呢，它又包含什么内容呢？其实它也是AsyncTask的一个内部类，是用来包装执行结果的一个类，让我们来看一下它的代码结构：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. @SuppressWarnings({"RawUseOfParameterizedType"})  
2. private static class AsyncTaskResult<Data> {  
3. ​    final AsyncTask mTask;  
4. ​    final Data[] mData;  
5.   
6. ​    AsyncTaskResult(AsyncTask task, Data... data) {  
7. ​        mTask = task;  
8. ​        mData = data;  
9. ​    }  
10. }  

看以看到这个AsyncTaskResult封装了一个AsyncTask的实例和某种类型的数据集，我们再来看一下构建消息时的代码：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. //发送取消任务的消息  
2. message = sHandler.obtainMessage(MESSAGE_POST_CANCEL,  
3. ​        new AsyncTaskResult<Result>(AsyncTask.this, (Result[]) null));  
4. message.sendToTarget();  

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. //发送显示结果的消息  
2. message = sHandler.obtainMessage(MESSAGE_POST_RESULT,  
3. ​         new AsyncTaskResult<Result>(AsyncTask.this, result));  
4. message.sendToTarget();  

在处理消息时是如何使用这个对象呢，我们再来看一下：

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. result.mTask.finish(result.mData[0]);  

**[java]** [view plain](http://blog.csdn.net/liuhe688/article/details/6532519#) [copy](http://blog.csdn.net/liuhe688/article/details/6532519#)

1. result.mTask.onProgressUpdate(result.mData);  

概括来说，当我们调用execute(Params... params)方法后，execute方法会调用onPreExecute()方法，然后由ThreadPoolExecutor实例sExecutor执行一个FutureTask任务，这个过程中doInBackground(Params... params)将被调用，如果被开发者覆写的doInBackground(Params... params)方法中调用了publishProgress(Progress... values)方法，则通过InternalHandler实例sHandler发送一条MESSAGE_POST_PROGRESS消息，更新进度，sHandler处理消息时onProgressUpdate(Progress... values)方法将被调用；如果遇到异常，则发送一条MESSAGE_POST_CANCEL的消息，取消任务，sHandler处理消息时onCancelled()方法将被调用；如果执行成功，则发送一条MESSAGE_POST_RESULT的消息，显示结果，sHandler处理消息时onPostExecute(Result result)方法被调用。

经过上面的介绍，相信朋友们都已经认识到AsyncTask的本质了，它对Thread+Handler的良好封装，减少了开发者处理问题的复杂度，提高了开发效率，希望朋友们能多多体会一下。

#### 相关面试题

```
1. Android系统对下列哪些对象提供了资源池 (A C)
    A. Message
    B. Thread
    C. AsyncTask
    D. Looper
    解析：
    	A.Message提供了消息池，有静态方法Obtain从消息池中取对象；
    	B.Thread默认不提供资源池，除非使用线程池ThreadPool管理；
    	C.AsynTask是线程池改造的。
    		池里 默认提供（核数+1）个线程进行并发操作
    		最大支持（核数  * 2 + 1）个线程，超过后会丢弃其他任务
    	D.Looper，每个Looper创建时创建一个消息队列和线程对象，也不是资源池；
```

