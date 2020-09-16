# Android

#### 1. Android的四大组件

>Activity 活动，Service 服务，Content Provider 内容提供者，BroadcastReceiver 广播接收器

1. **Activity（活动）** ：提供窗口来和用户进行交互。

2. **Service （服务）**：它能够在后台执行一些耗时较长的操作，并且不提供用户界面。

3. **Content Provider （内容提供者）**：我们需要操作其他应用程序的一些数据，就会用到ContentProvider。

4. **BroadcastReceiver （广播接收器）**：广播是一种广泛运用的在应用程序之间传输信息的机制，主要用来监听系统或者应用发出的广播信息，然后根据广播信息作为相应的逻辑处理，也可以用来传输少量、频率低的数据。

#### 2. Android的五大布局

> LinearLayout（线性布局）FrameLayout（帧布局）RelativeLayout（相对布局）TableLayout（表格布局）AbsoluteLayout(绝对布局)

1. **LinearLayout（线性布局）**：在一个方向上（垂直或者水平）对齐所有子元素，一个垂直列表中每一行都只有一个子元素，一个水平列表只是一列高度。
2. **RelativeLayout（相对布局）**：根据布局中子控件会根据他们设置的参照控件和参数进行相对布局。参照控件可以是父控件，也可以是其他的子控件，但是被参照的空间必须在参照它的控件之前定义。
3. **AbsoluteLayout(绝对布局)**：此布局中的子控件需要指定其坐标的相对位置的横纵坐标，否则此布局会像FrameLayout布局一样被排在左上角。此布局不能自动适应屏幕尺寸，所以少用

4. **FrameLayout（帧布局）**：此布局是最简单的布局形式，所添加的组件都是层叠的方式显示，第一个控件在最底层，最后添加的控件在视图显示的最上层，有点类似堆栈的形式。

5. **TableLayout（表格布局）**：把子控件元素放置在行和列中，并且不显示行列和单元格边界线。每一行就是一个TableRow，也可以是一个View对象。

#### 3. Android常用控件

1. 文本标签: TextView

```objectivec
    <TextView
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/hello"
        android:id="@+id/abc" />
```

2. 编辑文本框: EditView

```objectivec
    <EditText 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/edit"
        android:inputType="text"
        android:hint="请在此输入用户名..."/>    //hint就是灰色的那些提示字
```

3. 按钮: Button

```objectivec
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button"
        android:text="click me"/>
```

4. 多选框: CheckBox

```objectivec
    <CheckBox 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/checkbox1"
        android:text="aaa"/>
    <CheckBox 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/checkbox2"
        android:text="bbb"/>
```

5. 单选按钮:RadioButton

要注意的是因为单选按钮需要分组，也就是你得分好哪几个单选按钮之间只能选一个，然后用`RadioGroup`标签来圈起来，比如：

```xml
    <RadioGroup
        android:id="@+id/group1"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <RadioButton
            android:id="@+id/a1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="aaa"/>    //单标签，后面有/
        <RadioButton
            android:id="@+id/a2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="bbb"/>
    </RadioGroup>
```

6.  图片: ImageView

要注意的是其一般是通过`src`属性引用`res-drawable`对应分辨率的文件夹、`assets`或网络等地方的图片，比如引用安卓程序默认有的一个图片（就是那个绿色机器人）：

```objectivec
    <ImageButton 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/image"
        android:src="@drawable/ic_launcher"/>
```

当然在`class`文件当中也能设置图片，比如：



```undefined
    imageView = (ImageView) findViewById(R.id.image);
    imageView.setImageResource(R.drawable.ic_launcher);
```

7.  进度条: ProgressBar

有各种风格，垂直风格（一个圈圈），水平风格（一条线的，用的比较多的），`SeekBar`（可拖拽的，比如调音量的），`RatingBar`（评分几星的那种），设置方式通过`style`（前面没有android:），然后值有6种（`Horizontal`/`Small`/`Large`/`Inverse`/`Small.Inverse`/`Large.Inverse`），值的形式是`"?android:attr/progressBarStyle"+"类型"`，比如下面是个水平进度条：

```objectivec
    <ProgressBar 
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:id="@+id/progress"
        style="?android:attr/progressBarStyleHorizontal"/>
```

此时如果要设置其初始值、第二进度（两个进度都在一条线上，但颜色不同等）、加减可以在`class`中设置：

```cpp
progressBar.setMax(100);    //设置这条进度条总数值
progressBar.setProgress(20);    //设置第一进度初始数值
progressBar.setSecondaryProgress(30);   //设置第二进度初始数值
```

监听器控制加减进度：

```java
    class ButtonListener implements OnClickListener{
        public void onClick(View v){
            progressBar.incrementProgressBy(10);    //监听器中每次点击第一进度增加10，如果要减10就-10
            progressBar.incrementSecondaryProgressBy(10);   //每次点击第二进度就加10
        }
    }
```

#### 4. Android五大存储方式

①　使用SharedPreferences存储数据　

②　文件存储数据

③　 SQLite数据库存储数据

④　使用ContentProvider存储数据

⑤　网络存储数据

#### 5. hadler机制

#### 6. view的绘制流程

#### 7. View事件分发机制 

#### 8. MVC&MVP&MVVM

#### 9. intentService

#### 10. 内存泄露

#### 11. binder机制 

#### 12.