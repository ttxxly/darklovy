RecyclerView官方地址：[戳我](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html) 

RecyclerView是比 ListView 更高级且更具灵活性的组件。 此组件是一个用于显示庞大数据集的容器，可通过保持有限数量的视图进行非常有效的滚动操作.

#### 使用 RecyclerView 的步骤：

```
1. 添加 RecyclerView 组件，设置对应的id
2. 设置布局管理器（控制其显示方式,3种可选方式）
	LinearLayoutManager：线性布局管理器（可垂直可水平，默认垂直）
   	StaggeredGridLayoutManager: 错列网格布局管理器
   	GridLayoutManager：网格布局管理器
3. 设置适配器
4. 设置item增加、移除动画（通过 ItemAnimator）
5. 添加分割线
```

#### 设置布局管理器

```
recyclerView.setLayoutManager(LayoutManager layoutManager);
例如：recyclerView.setLayoutManager(new LinearLayoutManager(this));

////////////////////////////////
LinearLayoutManager：线性布局管理器
	格式：
        格式一：
            //参数为上下文环境，实现的是默认的垂直布局
            new LinearLayoutManager(Context context) 
        格式二：
            //param 1:上下文环境 
            //param 2：布局显示方式（默认垂直）
            	垂直：LinearLayoutManager.VERTICAL（数据从上到下）
            	水平：LinearLayoutManager.HORIZONTAL （数据从左到右）
            //param 3：数据是否反转
            new LinearLayoutManager( Context context, int orientation, boolean reverseLayout)
	示例：
		垂直布局不反转
			recyclerView.setLayoutManager(new LinearLayoutManager(this));
			new LinearLayoutManager(this,LinearLayoutManager.VERTICAL,false);
		反转垂直布局
			new LinearLayoutManager(this,LinearLayoutManager.VERTICAL,true);
		水平布局不反转
			new LinearLayoutManager(this,LinearLayoutManager.HORIZONTAL,false);
			
////////////////////////////////
GridLayoutManager：网格布局管理器
	格式：
        格式一：
            //param 1: 上下文环境
            //param 2: 要显示的列数
            //默认显示垂直布局
            new GridLayoutManager(Context context, int spanCount)
        格式二：
            //param 1: 上下文环境
            //param 2: 要显示的列数
            //param 3: 方向
            //param 4: 是否反转
            new GridLayoutManager( Context context, 
            int spanCount, int orientation, boolean reverseLayout)
            
////////////////////////////////
StaggeredGridLayoutManager: 错列网格布局管理器
	//param 1: 要显示的列数
	//param 2: 显示的方向
		垂直: StaggeredGridLayoutManager.VERTICAL
		水平: StaggeredGridLayoutManager.HORIZONTAL
    new StaggeredGridLayoutManager(int spanCount,int orientation)
```

#### 添加点击事件

上一节中我们讲了如何使用RecyclerView的Adpater，其实我们会发现，Adapter是添加点击事件一个很好的地方，里面是构造布局等View的主要场所，也是数据和布局进行绑定的地方。首先我们在Adapter中创建一个实现点击接口，其中view是点击的Item，data是我们的数据，因为我们想知道我点击的区域部分的数据是什么，以便我下一步进行操作：

```
public static interface OnRecyclerViewItemClickListener {    void onItemClick(View view , DataModel data);}
```

定义完接口，添加接口和设置Adapter接口的方法：

```
private OnRecyclerViewItemClickListener mOnItemClickListener = null;    public void setOnItemClickListener(OnRecyclerViewItemClickListener listener) {    this.mOnItemClickListener = listener;}
```

那么这个接口用在什么地方呢？如下代码所示，我们为Adapter实现OnClickListener方法：

```
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.ViewHolder> implements View.OnClickListener{    @Override    public ViewHolder onCreateViewHolder(ViewGroup viewGroup, final int i) {        View view = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.item, viewGroup, false);        ViewHolder vh = new ViewHolder(view);        //将创建的View注册点击事件        view.setOnClickListener(this);        return vh;    }    @Override    public void onBindViewHolder(ViewHolder viewHolder, final int i) {        viewHolder.mTextView.setText(datas.get(i).title);        //将数据保存在itemView的Tag中，以便点击时进行获取        viewHolder.itemView.setTag(datas.get(i));    }    ...    @Override    public void onClick(View v) {        if (mOnItemClickListener != null) {            //注意这里使用getTag方法获取数据            mOnItemClickListener.onItemClick(v,(DataModel)v.getTag());        }    }    ...}
```

做完这些事情，我们就可以在Activity或其他地方为RecyclerView添加项目点击事件了，如在MainActivity中：

```
mAdapter = new MyAdapter(getDummyDatas());mRecyclerView.setAdapter(mAdapter);mAdapter.setOnItemClickListener(new MyAdapter.OnRecyclerViewItemClickListener() {    @Override    public void onItemClick(View view, DataModel data) {        //DO your fucking bussiness here!    }});
```

完成了以上代码就可以为RecyclerView添加项目点击事件了，下面我们来看看RecyclerView如何添加和删除数据并在界面上显示。

#### 添加删除数据

以前在ListView当中，我们只要修改后数据用Adapter的notifyDatasetChange一下就可以更新界面。然而在RecyclerView中还有一些更高级的用法：

添加数据：

```
public void addItem(DataModel content, int position) {    datas.add(position, content);    notifyItemInserted(position); //Attention!}
```

删除数据：

```
public void removeItem(DataModel model) {    int position = datas.indexOf(model);    datas.remove(position);    notifyItemRemoved(position);//Attention!}
```

值得注意的是RecyclerView的添加删除都是有默认的动画效果的，如果没有效果可以添加如下代码：

```
mRecyclerView.setItemAnimator(newDefaultItemAnimator());
```

当然啦你也可以自己定义你自己的Animator，等我研究明白了也来讲一讲如何自定义这些效果~