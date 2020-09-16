# Android

#### 1. Android的四大组件

>Activity 活动，Service 服务，Content Provider 内容提供者，BroadcastReceiver 广播接收器

##### [1] 活动：Activity

提供窗口来和用户进行交互。

##### [2] 服务：Service

它能够在后台执行一些耗时较长的操作，并且不提供用户界面。

##### [3] 内容提供者：Content Provider 

我们需要操作其他应用程序的一些数据，就会用到ContentProvider。

##### [4] **广播接收器：BroadcastReceiver **

广播是一种广泛运用的在应用程序之间传输信息的机制，主要用来监听系统或者应用发出的广播信息，然后根据广播信息作为相应的逻辑处理，也可以用来传输少量、频率低的数据。

#### 2. Android的五大布局

> LinearLayout（线性布局）FrameLayout（帧布局）RelativeLayout（相对布局）TableLayout（表格布局）AbsoluteLayout(绝对布局)

##### [1] 线性布局：**LinearLayout**

在一个方向上（垂直或者水平）对齐所有子元素，一个垂直列表中每一行都只有一个子元素，一个水平列表只是一列高度。

##### [2] 相对布局：RelativeLayout

根据布局中子控件会根据他们设置的参照控件和参数进行相对布局。参照控件可以是父控件，也可以是其他的子控件，但是被参照的空间必须在参照它的控件之前定义。

##### [3] **绝对布局：AbsoluteLayout**

此布局中的子控件需要指定其坐标的相对位置的横纵坐标，否则此布局会像FrameLayout布局一样被排在左上角。此布局不能自动适应屏幕尺寸，所以少用

##### [4] **帧布局：FrameLayout**

此布局是最简单的布局形式，所添加的组件都是层叠的方式显示，第一个控件在最底层，最后添加的控件在视图显示的最上层，有点类似堆栈的形式。

##### [5] **表格布局：TableLayout**

把子控件元素放置在行和列中，并且不显示行列和单元格边界线。每一行就是一个TableRow，也可以是一个View对象。

#### 3. Android常用控件

##### [1] 文本标签: TextView

```objectivec
    <TextView
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/hello"
        android:id="@+id/abc" />
```

##### [2] 编辑文本框: EditView

```objectivec
    <EditText 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/edit"
        android:inputType="text"
        android:hint="请在此输入用户名..."/>    //hint就是灰色的那些提示字
```

##### [3] 按钮: Button

```objectivec
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button"
        android:text="click me"/>
```

##### [4] 多选框: CheckBox

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

##### [5] 单选按钮:RadioButton

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

##### [6] 图片: ImageView

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

##### [7] 进度条: ProgressBar

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

##### [1] SharedPreferences

SharedPreference类提供了一个总体框架，使您可以保存和检索的任何基本数据类型（ boolean, float, int, long, string）的持久键-值对（基于XML文件存储的“key-value”键值对数据）。

##### [2] **文件**

当文件被保存在内部存储中时，默认情况下，文件是应用程序私有的，其他应用不能访问。当用户卸载应用程序时这些文件也跟着被删除。

##### [3] **SQLite**

**SQLite**是一款轻量级的关系型数据库，它的运算速度非常快，占用资源很少，通常只需要几百K的内存就足够了，因而特别适合在移动设备上使用。

##### [4] **ContentProvider**

是数据调用者，ContentProvider将数据发布出来，通过ContentResolver对象结合Uri进行调用通过ContentResolver对象可以调用ContentProvider的增删改查。

>Uri（通用资源标识符 Universal Resource Identifer），代表数据操作的地址，每一个ContentProvider发布数据时都会有唯一的地址。

##### [5] **网络**

HttpUrlConnection和HttpClient。

#### 5. hadler机制

> https://www.jianshu.com/p/ba46bad5af67
>
> https://www.cnblogs.com/dendai-05/p/6945159.html
>
> https://www.jianshu.com/p/b63cdff5e661

**什么是Handler机制？**

Handler机制是AndroidSDK提供的一个非常重要的处理异步消息的机制，主要是由Handler、Looper、Message和MessageQueue组成，Handler只是消息处理机制的一部分。

- Message：消息（分为硬件产生的消息和软件产生的消息）。
- MessageQueue：消息队列，主要是向消息池投递消息（MessageQueue.enqueueMessage）和取走消息池中的消息(MessageQueue.next)。
- Handler：主要功能是向消息池发送消息（Handler.sendMessage）和处理消息（Handler.handleMessage）。
- Looper：不停的循环执行（Looper.loop），从MessageQueue中取出Message并发送给Handler。

**分析上述各部分：**

##### [1] Message

什么是硬件消息和软件消息呢？硬件消息就是我们滑动触摸点击按钮等等，软件消息就是我们主动new Message发送出去的。Message实现了Parcelable接口封装消息数据，所以他是存在于内存中的。一个实体（类）如果需要封装到消息中去就必须实现这一接口。

##### [2] MessageQueue

相当于一个容器，消息池。上述看到了.next应该猜到是链表形式，实际上确实是单链表维护，在插入和删除上有优势。在其next()中会无限循环，不断的判断是否有消息，有就返回这条消息并移除。

#####  [3] Looper

Looper创建的时候会创建一个MessageQueue，它们两个是一一对应的关系。调用Looper.loop()的时候消息循环开始，不断地调用MessageQueue的next()方法，当有消息就处理，否则就堵塞在next()方法中。loop()跟MessageQueue的next()一样都是死循环（源码可见for(;;)）。退出时调用Looper.quit()，它会调用MessageQueue的quit()方法，此时next会返回null，然后loop()方法也跟着退出。

##### [4] **Handler**

在主线程构造Handler，new Handler()里调用了Looper.myLooper()这个方法，这个方法是获取当前线程的Looper的。在其他线程调用sendMessage()时主线程的MessageQueue会插入一条Message，然后被Looper使用，在Looper的loop()中通过回调 msg.target.dispatchMessage(msg);发送给Handler。Handler跟Looper的关系是多对一。

一段Looper的源码片段：

![img](https:////upload-images.jianshu.io/upload_images/1427878-726ae596b9e7337f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1013/format/webp)

**解释完各部分的分工那来总结一下他们之间的关系：**Handler负责发送消息（Message）到MessageQueue中，Looper负责循环的接收MessageQueue中的消息通过回调方法返还给Handler自己本身。

![img](https:////upload-images.jianshu.io/upload_images/1427878-6df2837aaa26b267.png?imageMogr2/auto-orient/strip|imageView2/2/w/600/format/webp)

#### 6. view的绘制流程

>https://blog.csdn.net/sinat_27154507/article/details/79748010
>
>https://www.jianshu.com/p/5a71014e7b1b

##### [1] Measure过程

------

对于测量我们来说几个知识点,了解这几个知识点，之后的实例分析你才看得懂。
 **1、MeasureSpec 的理解**
 对于View的测量，肯定会和MeasureSpec接触，MeasureSpec是两个单词组成，翻译过来“测量规格”或者“测量参数”，很多博客包括官方文档对他的说明基本都是“一个MeasureSpec封装了从父容器传递给子容器的布局要求”,这个MeasureSpec 封装的是**父容器传递给子容器的布局要求**，而不是父容器对子容器的布局要求，“传递” 两个字很重要，更精确的说法应该这个MeasureSpec是由父View的MeasureSpec和子View的LayoutParams通过简单的计算得出一个针对子View的测量要求，这个测量要求就是MeasureSpec。

- 大家都知道一个MeasureSpec是一个大小跟模式的组合值,MeasureSpec中的值是一个整型（32位）将size和mode打包成一个Int型，其中高两位是mode，后面30位存的是size，是为了减少对象的分配开支。MeasureSpec 类似于下图，只不过这边用的是十进制的数，而MeasureSpec 是二进制存储的。

  ![img](https:////upload-images.jianshu.io/upload_images/966283-c330852c971b02a8.png?imageMogr2/auto-orient/strip|imageView2/2/w/405/format/webp)

  注：-1 代表的是EXACTLY，-2 是AT_MOST

- MeasureSpec一共有三种模式

> **UPSPECIFIED** : 父容器对于子容器没有任何限制,子容器想要多大就多大
>  **EXACTLY**: 父容器已经为子容器设置了尺寸,子容器应当服从这些边界,不论子容器想要多大的空间。
>  **AT_MOST**：子容器可以是声明大小内的任意大小

>1. **UNSPECIFIED (unspecified-不明确的) 父容器不对 View 有任何的限制**，要多大给多大，这种情况下一般用于系统内部，表示一种测量的状态。
>2. **EXACTLY (exactly-精确地)父容器已经检测出 View 所需要的精确大小**，这个时候 View 的最终大小就是 SpecSize 所指定的值，它对应于LayoutParams 中的 **match_parent** 和具体的数值这两种模式。
>3. **AT_MOST (at_most-最大) 父容器指定了一个可用大小即 SpecSize**，View 的大小不能大于这个值，具体是什么值要看不同 View 的具体实现。它对应于 LayoutParams 中的 **wrap_content**。

很多文章都会把这三个模式说成这样，当然其实包括官方文档也是这样表达的，但是这样并不好理解。特别是如果把这三种模式又和MATCH_PARENT和WRAP_CONTENT 联系到一起，很多人就懵逼了。如果从代码上来看view.measure(int widthMeasureSpec, int heightMeasureSpec) 的两个MeasureSpec是父类传递过来的，但并不是完全是父View的要求，而是父View的MeasureSpec和子View自己的LayoutParams共同决定的，而子View的LayoutParams其实就是我们在xml写的时候设置的layout_width和layout_height 转化而来的。我们先来看代码会清晰一些：

父View的measure的过程会先测量子View，等子View测量结果出来后，再来测量自己，上面的measureChildWithMargins就是用来测量某个子View的，我们来分析是怎样测量的，具体看注释：

```java
protected void measureChildWithMargins(View child, int parentWidthMeasureSpec, int widthUsed, int parentHeightMeasureSpec, int heightUsed) { 

// 子View的LayoutParams，你在xml的layout_width和layout_height,
// layout_xxx的值最后都会封装到这个个LayoutParams。
final MarginLayoutParams lp = (MarginLayoutParams) child.getLayoutParams();   

//根据父View的测量规格和父View自己的Padding，
//还有子View的Margin和已经用掉的空间大小（widthUsed），就能算出子View的MeasureSpec,具体计算过程看getChildMeasureSpec方法。
final int childWidthMeasureSpec = getChildMeasureSpec(parentWidthMeasureSpec,            
mPaddingLeft + mPaddingRight + lp.leftMargin + lp.rightMargin + widthUsed, lp.width);    

final int childHeightMeasureSpec = getChildMeasureSpec(parentHeightMeasureSpec,           
mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin  + heightUsed, lp.height);  

//通过父View的MeasureSpec和子View的自己LayoutParams的计算，算出子View的MeasureSpec，然后父容器传递给子容器的
// 然后让子View用这个MeasureSpec（一个测量要求，比如不能超过多大）去测量自己，如果子View是ViewGroup 那还会递归往下测量。
child.measure(childWidthMeasureSpec, childHeightMeasureSpec);

}

// spec参数   表示父View的MeasureSpec 
// padding参数    父View的Padding+子View的Margin，父View的大小减去这些边距，才能精确算出
//               子View的MeasureSpec的size
// childDimension参数  表示该子View内部LayoutParams属性的值（lp.width或者lp.height）
//                    可以是wrap_content、match_parent、一个精确指(an exactly size),  
public static int getChildMeasureSpec(int spec, int padding, int childDimension) {  
    int specMode = MeasureSpec.getMode(spec);  //获得父View的mode  
    int specSize = MeasureSpec.getSize(spec);  //获得父View的大小  

   //父View的大小-自己的Padding+子View的Margin，得到值才是子View的大小。
    int size = Math.max(0, specSize - padding);   
  
    int resultSize = 0;    //初始化值，最后通过这个两个值生成子View的MeasureSpec
    int resultMode = 0;    //初始化值，最后通过这个两个值生成子View的MeasureSpec
  
    switch (specMode) {  
    // Parent has imposed an exact size on us  
    //1、父View是EXACTLY的 ！  
    case MeasureSpec.EXACTLY:   
        //1.1、子View的width或height是个精确值 (an exactly size)  
        if (childDimension >= 0) {            
            resultSize = childDimension;         //size为精确值  
            resultMode = MeasureSpec.EXACTLY;    //mode为 EXACTLY 。  
        }   
        //1.2、子View的width或height为 MATCH_PARENT/FILL_PARENT   
        else if (childDimension == LayoutParams.MATCH_PARENT) {  
            // Child wants to be our size. So be it.  
            resultSize = size;                   //size为父视图大小  
            resultMode = MeasureSpec.EXACTLY;    //mode为 EXACTLY 。  
        }   
        //1.3、子View的width或height为 WRAP_CONTENT  
        else if (childDimension == LayoutParams.WRAP_CONTENT) {  
            // Child wants to determine its own size. It can't be  
            // bigger than us.  
            resultSize = size;                   //size为父视图大小  
            resultMode = MeasureSpec.AT_MOST;    //mode为AT_MOST 。  
        }  
        break;  
  
    // Parent has imposed a maximum size on us  
    //2、父View是AT_MOST的 ！      
    case MeasureSpec.AT_MOST:  
        //2.1、子View的width或height是个精确值 (an exactly size)  
        if (childDimension >= 0) {  
            // Child wants a specific size... so be it  
            resultSize = childDimension;        //size为精确值  
            resultMode = MeasureSpec.EXACTLY;   //mode为 EXACTLY 。  
        }  
        //2.2、子View的width或height为 MATCH_PARENT/FILL_PARENT  
        else if (childDimension == LayoutParams.MATCH_PARENT) {  
            // Child wants to be our size, but our size is not fixed.  
            // Constrain child to not be bigger than us.  
            resultSize = size;                  //size为父视图大小  
            resultMode = MeasureSpec.AT_MOST;   //mode为AT_MOST  
        }  
        //2.3、子View的width或height为 WRAP_CONTENT  
        else if (childDimension == LayoutParams.WRAP_CONTENT) {  
            // Child wants to determine its own size. It can't be  
            // bigger than us.  
            resultSize = size;                  //size为父视图大小  
            resultMode = MeasureSpec.AT_MOST;   //mode为AT_MOST  
        }  
        break;  
  
    // Parent asked to see how big we want to be  
    //3、父View是UNSPECIFIED的 ！  
    case MeasureSpec.UNSPECIFIED:  
        //3.1、子View的width或height是个精确值 (an exactly size)  
        if (childDimension >= 0) {  
            // Child wants a specific size... let him have it  
            resultSize = childDimension;        //size为精确值  
            resultMode = MeasureSpec.EXACTLY;   //mode为 EXACTLY  
        }  
        //3.2、子View的width或height为 MATCH_PARENT/FILL_PARENT  
        else if (childDimension == LayoutParams.MATCH_PARENT) {  
            // Child wants to be our size... find out how big it should  
            // be  
            resultSize = 0;                        //size为0！ ,其值未定  
            resultMode = MeasureSpec.UNSPECIFIED;  //mode为 UNSPECIFIED  
        }   
        //3.3、子View的width或height为 WRAP_CONTENT  
        else if (childDimension == LayoutParams.WRAP_CONTENT) {  
            // Child wants to determine its own size.... find out how  
            // big it should be  
            resultSize = 0;                        //size为0! ，其值未定  
            resultMode = MeasureSpec.UNSPECIFIED;  //mode为 UNSPECIFIED  
        }  
        break;  
    }  
    //根据上面逻辑条件获取的mode和size构建MeasureSpec对象。  
    return MeasureSpec.makeMeasureSpec(resultSize, resultMode);  
}    
```

上面的代码有点多，希望你仔细看一些注释，代码写得很多，其实计算原理很简单：
 1、如果我们在xml 的layout_width或者layout_height 把值都写死，那么上述的测量完全就不需要了，之所以要上面的这步测量，是因为 **match_parent 就是充满父容器，wrap_content 就是自己多大就多大**， 我们写代码的时候特别爽，我们编码方便的时候，google就要帮我们计算你match_parent的时候是多大，wrap_content的是多大，这个计算过程，就是计算出来的父View的MeasureSpec不断往子View传递，结合子View的LayoutParams 一起再算出子View的MeasureSpec，然后继续传给子View，不断计算每个View的MeasureSpec，子View有了MeasureSpec才能更测量自己和自己的子View。

2、上述代码如果这么来理解就简单了

- **如果父View的MeasureSpec 是EXACTLY，说明父View的大小是确切的，（确切的意思很好理解，如果一个View的MeasureSpec 是EXACTLY，那么它的size 是多大，最后展示到屏幕就一定是那么大）。**

1、如果子View 的layout_xxxx是MATCH_PARENT，父View的大小是确切，子View的大小又MATCH_PARENT（充满整个父View），那么子View的大小肯定是确切的，而且大小值就是父View的size。所以子View的size=父View的size，mode=EXACTLY

2、如果子View 的layout_xxxx是WRAP_CONTENT，也就是子View的大小是根据自己的content 来决定的，但是子View的毕竟是子View，大小不能超过父View的大小，但是子View的是WRAP_CONTENT，我们还不知道具体子View的大小是多少，要等到child.measure(childWidthMeasureSpec, childHeightMeasureSpec) 调用的时候才去真正测量子View 自己content的大小（比如TextView wrap_content 的时候你要测量TextView content 的大小，也就是字符占用的大小，这个测量就是在child.measure(childWidthMeasureSpec, childHeightMeasureSpec)的时候，才能测出字符的大小，MeasureSpec 的意思就是假设你字符100px，但是MeasureSpec 要求最大的只能50px，这时候就要截掉了）。通过上述描述，子View MeasureSpec mode的应该是AT_MOST，而size 暂定父View的 size，表示的意思就是子View的大小没有不确切的值，子View的大小最大为父View的大小，不能超过父View的大小（这就是AT_MOST 的意思），然后这个MeasureSpec 做为子View measure方法 的参数，做为子View的大小的约束或者说是要求，有了这个MeasureSpec子View再实现自己的测量。

3、如果如果子View 的layout_xxxx是确定的值（200dp），那么就更简单了，不管你父View的mode和size是什么，我都写死了就是200dp，那么控件最后展示就是就是200dp，不管我的父View有多大，也不管我自己的content 有多大，反正我就是这么大，所以这种情况MeasureSpec 的mode = EXACTLY 大小size=你在layout_xxxx 填的那个值。

- **如果父View的MeasureSpec 是AT_MOST，说明父View的大小是不确定，最大的大小是MeasureSpec 的size值，不能超过这个值。**

1、如果子View 的layout_xxxx是MATCH_PARENT，父View的大小是不确定（只知道最大只能多大），子View的大小MATCH_PARENT（充满整个父View），那么子View你即使充满父容器，你的大小也是不确定的，父View自己都确定不了自己的大小，你MATCH_PARENT你的大小肯定也不能确定的，所以子View的mode=AT_MOST，size=父View的size，也就是你在布局虽然写的是MATCH_PARENT，但是由于你的父容器自己的大小不确定，导致子View的大小也不确定，只知道最大就是父View的大小。

2、如果子View 的layout_xxxx是WRAP_CONTENT，父View的大小是不确定（只知道最大只能多大），子View又是WRAP_CONTENT，那么在子View的Content没算出大小之前，子View的大小最大就是父View的大小，所以子View MeasureSpec mode的就是AT_MOST，而size 暂定父View的 size。

3、如果如果子View 的layout_xxxx是确定的值（200dp），同上，写多少就是多少，改变不了的。

- **如果父View的MeasureSpec 是UNSPECIFIED(未指定),表示没有任何束缚和约束，不像AT_MOST表示最大只能多大，不也像EXACTLY表示父View确定的大小，子View可以得到任意想要的大小，不受约束**

1、如果子View 的layout_xxxx是MATCH_PARENT，因为父View的MeasureSpec是UNSPECIFIED，父View自己的大小并没有任何约束和要求，
 那么对于子View来说无论是WRAP_CONTENT还是MATCH_PARENT，子View也是没有任何束缚的，想多大就多大，没有不能超过多少的要求，一旦没有任何要求和约束，size的值就没有任何意义了，所以一般都直接设置成0

2、同上...

3、如果如果子View 的layout_xxxx是确定的值（200dp），同上，写多少就是多少，改变不了的（记住，只有设置的确切的值，那么无论怎么测量，大小都是不变的，都是你写的那个值）

到此为止，你是否对MeasureSpec 和三种模式、还有WRAP_CONTENT和MATCH_PARENT有一定的了解了，如果还有任何问题，欢迎在我简书（用户名：Kelin）评论里留言。

**2、View的测量过程主要是在onMeasure()方法**
 打开View的源码，找到measure方法，这个方法代码不少，但是测量工作都是在onMeasure()做的，measure方法是final的所以这个方法也不可重写，如果想自定义View的测量，你应该去重写onMeasure()方法

```java
public final void measure(int widthMeasureSpec, int heightMeasureSpec) {
  ......
  onMeasure(widthMeasureSpec,heightMeasureSpec);
  .....
}
```

**3、View的onMeasure 的默认实现**
 打开View.java 的源码来看下onMeasure的实现

```java
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {    
  setMeasuredDimension(
  getDefaultSize(getSuggestedMinimumWidth(), widthMeasureSpec),            
  getDefaultSize(getSuggestedMinimumHeight(), heightMeasureSpec));
}
```

View的onMeasure方法默认实现很简单，就是调用setMeasuredDimension()，setMeasuredDimension()可以简单理解就是给mMeasuredWidth和mMeasuredHeight设值，如果这两个值一旦设置了，那么意味着对于这个View的测量结束了，这个View的宽高已经有测量的结果出来了。如果我们想设定某个View的高宽，完全可以直接通过setMeasuredDimension（100，200）来设置死它的高宽（不建议），但是setMeasuredDimension方法必须在onMeasure方法中调用，不然会抛异常。我们来看下对于View来说它的默认高宽是怎么获取的。



```java
//获取的是android:minHeight属性的值或者View背景图片的大小值
protected int getSuggestedMinimumWidth() { 
   return (mBackground == null) ? mMinWidth : max(mMinWidth, mBackground.getMinimumWidth()); 
} 
//@param size参数一般表示设置了android:minHeight属性或者该View背景图片的大小值  
public static int getDefaultSize(int size, int measureSpec) {    
   int result = size;    
   int specMode = MeasureSpec.getMode(measureSpec);    
   int specSize = MeasureSpec.getSize(measureSpec);    
   switch (specMode) {    
   case MeasureSpec.UNSPECIFIED:        //表示该View的大小父视图未定，设置为默认值 
     result = size;  
     break;    
   case MeasureSpec.AT_MOST:    
   case MeasureSpec.EXACTLY:        
     result = specSize;  
     break;   
 }    
return result;
}
```

getDefaultSize的第一个参数size等于getSuggestedMinimumXXXX返回的的值（建议的最小宽度和高度），而建议的最小宽度和高度都是由View的Background尺寸与通过设置View的minXXX属性共同决定的，这个size可以理解为View的默认长度，而第二个参数measureSpec，是父View传给自己的MeasureSpec,这个measureSpec是通过测量计算出来的，具体的计算测量过程前面在讲解MeasureSpec已经讲得比较清楚了（是有父View的MeasureSpec和子View自己的LayoutParams 共同决定的）只要这个测试的mode不是UNSPECIFIED（未确定的），那么默认的就会用这个测量的数值当做View的高度。

对于View默认是测量很简单，大部分情况就是拿计算出来的MeasureSpec的size 当做最终测量的大小。而对于其他的一些View的派生类，如TextView、Button、ImageView等，它们的onMeasure方法系统了都做了重写，不会这么简单直接拿 MeasureSpec 的size来当大小，而去会先去测量字符或者图片的高度等，然后拿到View本身content这个高度（字符高度等），如果MeasureSpec是AT_MOST，而且View本身content的高度不超出MeasureSpec的size，那么可以直接用View本身content的高度（字符高度等），而不是像View.java 直接用MeasureSpec的size做为View的大小。

**4、ViewGroup的Measure过程**
 ViewGroup 类并没有实现onMeasure，我们知道测量过程其实都是在onMeasure方法里面做的，我们来看下FrameLayout 的onMeasure 方法,具体分析看注释哦。



```java
//FrameLayout 的测量
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {  
....
int maxHeight = 0;
int maxWidth = 0;
int childState = 0;
for (int i = 0; i < count; i++) {    
   final View child = getChildAt(i);    
   if (mMeasureAllChildren || child.getVisibility() != GONE) {   
    // 遍历自己的子View，只要不是GONE的都会参与测量，measureChildWithMargins方法在最上面
    // 的源码已经讲过了，如果忘了回头去看看，基本思想就是父View把自己的MeasureSpec 
    // 传给子View结合子View自己的LayoutParams 算出子View 的MeasureSpec，然后继续往下传，
    // 传递叶子节点，叶子节点没有子View，根据传下来的这个MeasureSpec测量自己就好了。
     measureChildWithMargins(child, widthMeasureSpec, 0, heightMeasureSpec, 0);       
     final LayoutParams lp = (LayoutParams) child.getLayoutParams(); 
     maxWidth = Math.max(maxWidth, child.getMeasuredWidth() +  lp.leftMargin + lp.rightMargin);        
     maxHeight = Math.max(maxHeight, child.getMeasuredHeight() + lp.topMargin + lp.bottomMargin);  
     ....
     ....
   }
}
.....
.....
//所有的孩子测量之后，经过一系类的计算之后通过setMeasuredDimension设置自己的宽高，
//对于FrameLayout 可能用最大的字View的大小，对于LinearLayout，可能是高度的累加，
//具体测量的原理去看看源码。总的来说，父View是等所有的子View测量结束之后，再来测量自己。
setMeasuredDimension(resolveSizeAndState(maxWidth, widthMeasureSpec, childState),        
resolveSizeAndState(maxHeight, heightMeasureSpec, childState << MEASURED_HEIGHT_STATE_SHIFT));
....
}  
```

到目前为止，基本把Measure 主要原理都过了一遍，接下来我们会结合实例来讲解整个match的过程，首先看下面的代码：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout  xmlns:android="http://schemas.android.com/apk/res/android"    
   android:id="@+id/linear"
   android:layout_width="match_parent"    
   android:layout_height="wrap_content"    
   android:layout_marginTop="50dp"    
   android:background="@android:color/holo_blue_dark"    
   android:paddingBottom="70dp"    
   android:orientation="vertical">    
   <TextView        
    android:id="@+id/text"       
    android:layout_width="match_parent"     
    android:layout_height="wrap_content"  
    android:background="@color/material_blue_grey_800"       
    android:text="TextView"        
    android:textColor="@android:color/white"        
    android:textSize="20sp" />    
   <View       
      android:id="@+id/view"       
     android:layout_width="match_parent" 
     android:layout_height="150dp"    
     android:background="@android:color/holo_green_dark" />
</LinearLayout>
```

上面的代码对于出来的布局是下面的一张图

![img](https:////upload-images.jianshu.io/upload_images/966283-4a11f92ac8c5e224.png?imageMogr2/auto-orient/strip|imageView2/2/w/1042/format/webp)

对于上面图可能有些不懂，这边做下说明:

> 整个图是一个DecorView,DecorView可以理解成整个页面的根View,DecorView是一个FrameLayout,包含两个子View，一个id=statusBarBackground的View和一个是LineaLayout，id=statusBarBackground的View，我们可以先不管（我也不是特别懂这个View,应该就是statusBar的设置背景的一个控件，方便设置statusBar的背景)，而这个LinearLayout比较重要，它包含一个title和一个content，title很好理解其实就是TitleBar或者ActionBar,content 就更简单了，setContentView()方法你应该用过吧，android.R.id.content 你应该听过吧，没错就是它,content是一个FrameLayout，你写的页面布局通过setContentView加进来就成了content的直接子View。

整个View的布局图如下：

![img](https:////upload-images.jianshu.io/upload_images/966283-4096801e91e2eccc.png?imageMogr2/auto-orient/strip|imageView2/2/w/810/format/webp)



这张图在下面分析measure，会经常用到，主要用于了解递归的时候view 的measure顺序

> 注:
>  1、 header的是个ViewStub,用来惰性加载ActionBar，为了便于分析整个测量过程，我把Theme设成NoActionBar，避免ActionBar 相关的measure干扰整个过程，这样可以忽略掉ActionBar 的测量，在调试代码更清晰。
>  2、包含Header(ActionBar）和id/content 的那个父View，我不知道叫什么名字好，我们姑且叫它ViewRoot（看上图）,它是垂直的LinearLayout，放着整个页面除statusBar 的之外所有的东西，叫它ViewRoot 应该还ok，一个代号而已。

既然我们知道整个View的Root是DecorView，那么View的绘制是从哪里开始的呢，我们知道每个Activity 均会创建一个 PhoneWindow对象，是Activity和整个View系统交互的接口，每个Window都对应着一个View和一个ViewRootImpl，Window和View通过ViewRootImpl来建立联系,对于Activity来说，ViewRootImpl是连接WindowManager和DecorView的纽带,绘制的入口是由ViewRootImpl的performTraversals方法来发起Measure，Layout，Draw等流程的。

我们来看下ViewRootImpl的performTraversals 方法：



```java
private void performTraversals() { 
...... 
int childWidthMeasureSpec = getRootMeasureSpec(mWidth, lp.width); 
int childHeightMeasureSpec = getRootMeasureSpec(mHeight, lp.height); 
...... 
mView.measure(childWidthMeasureSpec, childHeightMeasureSpec); 
......
mView.layout(0, 0, mView.getMeasuredWidth(), mView.getMeasuredHeight());
...... 
mView.draw(canvas); 
......
}

private static int getRootMeasureSpec(int windowSize, int rootDimension) { 
   int measureSpec; 
   switch (rootDimension) { 
   case ViewGroup.LayoutParams.MATCH_PARENT: 
   // Window can't resize. Force root view to be windowSize.   
   measureSpec = MeasureSpec.makeMeasureSpec(windowSize,MeasureSpec.EXACTLY);
   break; 
   ...... 
  } 
 return measureSpec; 
}
```

performTraversals 中我们看到的mView其实就是DecorView,View的绘制从DecorView开始， 在mView.measure()的时候调用getRootMeasureSpec获得两个MeasureSpec做为参数，getRootMeasureSpec的两个参数（mWidth, lp.width）mWith和mHeight 是屏幕的宽度和高度， lp是WindowManager.LayoutParams，它的lp.width和lp.height的默认值是MATCH_PARENT,所以通过getRootMeasureSpec 生成的测量规格MeasureSpec 的mode是MATCH_PARENT ，size是屏幕的高宽。
 因为DecorView 是一个FrameLayout 那么接下来会进入FrameLayout 的measure方法，measure的两个参数就是刚才getRootMeasureSpec的生成的两个MeasureSpec，DecorView的测量开始了。
 首先是DecorView 的 MeasureSpec ，根据上面的分析DecorView 的 MeasureSpec是Windows传过来的，我们画出DecorView 的MeasureSpec 图：



![img](https:////upload-images.jianshu.io/upload_images/966283-c330852c971b02a8.png?imageMogr2/auto-orient/strip|imageView2/2/w/405/format/webp)

> 注：
>  1、-1 代表的是EXACTLY，-2 是AT_MOST
>  2、由于屏幕的像素是1440x2560,所以DecorView 的MeasureSpec的size 对应于这两个值

那么接下来在FrameLayout 的onMeasure()方法DecorView开始for循环测量自己的子View,测量完所有的子View再来测量自己，由下图可知，接下来要测量ViewRoot的大小



![img](https:////upload-images.jianshu.io/upload_images/966283-4096801e91e2eccc.png?imageMogr2/auto-orient/strip|imageView2/2/w/810/format/webp)



```java
//FrameLayout 的测量
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {  
....
int maxHeight = 0;
int maxWidth = 0;
int childState = 0;
for (int i = 0; i < count; i++) {    
   final View child = getChildAt(i);    
   if (mMeasureAllChildren || child.getVisibility() != GONE) {   
    // 遍历自己的子View，只要不是GONE的都会参与测量，measureChildWithMargins方法在最上面
    // 的源码已经讲过了，如果忘了回头去看看，基本思想就是父View把自己当MeasureSpec 
    // 传给子View结合子View自己的LayoutParams 算出子View 的MeasureSpec，然后继续往下穿，
    // 传递叶子节点，叶子节点没有子View，只要负责测量自己就好了。
     measureChildWithMargins(child, widthMeasureSpec, 0, heightMeasureSpec, 0);      
     ....
     ....
   }
}
....
}  
```

DecorView 测量ViewRoot 的时候把自己的widthMeasureSpec和heightMeasureSpec传进去了，接下来你就要去看measureChildWithMargins的源码了



```java
protected void measureChildWithMargins(View child, int parentWidthMeasureSpec, int widthUsed, int parentHeightMeasureSpec, int heightUsed) { 

final MarginLayoutParams lp = (MarginLayoutParams) child.getLayoutParams();   

final int childWidthMeasureSpec = getChildMeasureSpec(parentWidthMeasureSpec,            
mPaddingLeft + mPaddingRight + lp.leftMargin + lp.rightMargin + widthUsed, lp.width);    

final int childHeightMeasureSpec = getChildMeasureSpec(parentHeightMeasureSpec,           
mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin  + heightUsed, lp.height);  

child.measure(childWidthMeasureSpec, childHeightMeasureSpec);
}
```

ViewRoot 是系统的View，它的LayoutParams默认都是match_parent,根据我们文章最开始MeasureSpec 的计算规则，ViewRoot 的MeasureSpec mode应该等于EXACTLY（DecorView MeasureSpec 的mode是EXACTLY，ViewRoot的layoutparams 是match_parent），size 也等于DecorView的size，所以ViewRoot的MeasureSpec图如下：

![img](https:////upload-images.jianshu.io/upload_images/966283-ed0ffedcca47672a.png?imageMogr2/auto-orient/strip|imageView2/2/w/427/format/webp)



算出ViewRoot的MeasureSpec 之后，开始调用ViewRoot.measure 方法去测量ViewRoot的大小，然而ViewRoot是一个LinearLayout ，ViewRoot.measure最终会执行的LinearLayout 的onMeasure 方法，LinearLayout 的onMeasure 方法又开始逐个测量它的子View，上面的measureChildWithMargins方法又会被调用，那么根据View的层级图，接下来测量的是header（ViewStub）,由于header的Gone，所以直接跳过不做测量工作，所以接下来轮到ViewRoot的第二个child content（android.R.id.content）,我们要算出这个content 的MeasureSpec，所以又要拿ViewRoot 的MeasureSpec 和 android.R.id.content的LayoutParams 做计算了，计算过程就是调用getChildMeasureSpec的方法，



![img](https:////upload-images.jianshu.io/upload_images/966283-527eb25fd49d38ef.png?imageMogr2/auto-orient/strip|imageView2/2/w/777/format/webp)



```java
protected void measureChildWithMargins(View child, int parentWidthMeasureSpec, int widthUsed, int parentHeightMeasureSpec, int heightUsed) { 
   .....
   final int childHeightMeasureSpec = getChildMeasureSpec(parentHeightMeasureSpec,           
mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin  + heightUsed, lp.height);  
   ....
}

public static int getChildMeasureSpec(int spec, int padding, int childDimension) {  
    int specMode = MeasureSpec.getMode(spec);  //获得父View的mode  
    int specSize = MeasureSpec.getSize(spec);  //获得父View的大小  
  
    int size = Math.max(0, specSize - padding); //父View的大小-自己的Padding+子View的Margin，得到值才是子View可能的最大值。  
     .....
}
```

由上面的代码
 **int size = Math.max(0, specSize - padding);**
 而 **padding=mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin  + heightUsed**
 算出android.R.id.content 的MeasureSpec 的size
 由于ViewRoot 的mPaddingBottom=100px(这个可能和状态栏的高度有关，我们测量的最后会发现id/statusBarBackground的View的高度刚好等于100px，ViewRoot 是系统的View的它的Padding 我们没法改变，所以计算出来Content（android.R.id.content） 的MeasureSpec 的高度少了100px ，它的宽高的mode 根据算出来也是EXACTLY（ViewRoot 是EXACTLY和android.R.id.content  是match_parent）。所以Content（android.R.id.content）的MeasureSpec 如下（高度少了100px）：

![img](https:////upload-images.jianshu.io/upload_images/966283-5ce615a3684d7815.png?imageMogr2/auto-orient/strip|imageView2/2/w/380/format/webp)

Paste_Image.png

Content（android.R.id.content） 是FrameLayout，递归调用开始准备计算id/linear的MeasureSpec，我们先给出结果：

![img](https:////upload-images.jianshu.io/upload_images/966283-c7e86f4510ddf84a.png?imageMogr2/auto-orient/strip|imageView2/2/w/768/format/webp)

> 图中有两个要注意的地方：
>  1、id/linear的heightMeasureSpec 的mode=AT_MOST，因为id/linear 的LayoutParams 的layout_height="wrap_content"
>  2、id/linear的heightMeasureSpec  的size 少了200px, 由上面的代码
>  padding=mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin  + heightUsed;
>  int size = Math.max(0, specSize - padding);
>  由于id/linear 的 android:layout_marginTop="50dp"  使得lp.topMargin=200px (本设备的density=4，px=4*pd)，在计算后id/linear的heightMeasureSpec  的size 少了200px。（布局代码前面已给出，可自行查看id/linear 控件xml中设置的属性）

linear.measure接着往下算linear的子View的的MeasureSpec，看下View 层级图，往下走应该是id/text,接下来是计算id/text的MeasureSpec，直接看图，mode=AT_MOST ,size 少了280，别问我为什么 ...specSize - padding.

![img](https:////upload-images.jianshu.io/upload_images/966283-058c5a6ce57b3125.png?imageMogr2/auto-orient/strip|imageView2/2/w/757/format/webp)

算出id/text 的MeasureSpec 后，接下来text.measure(childWidthMeasureSpec, childHeightMeasureSpec);准备测量id/text 的高宽，这时候已经到底了，id/text是TextView，已经没有子类了，这时候跳到TextView的onMeasure方法了。TextView 拿着刚才计算出来的heightMeasureSpec（mode=AT_MOST,size=1980）,这个就是对TextView的高度和宽度的约束，进到TextView 的onMeasure(widthMeasureSpec,heightMeasureSpec) 方法，在onMeasure 方法执行调试过程中，我们发现下面的代码：

![img](https:////upload-images.jianshu.io/upload_images/966283-856ea117c2b84148.png?imageMogr2/auto-orient/strip|imageView2/2/w/698/format/webp)

Paste_Image.png

TextView字符的高度（也就是TextView的content高度[wrap_content]）测出来=107px，107px 并没有超过1980px(允许的最大高度)，所以实际测量出来TextView的高度是107px。
 最终算出id/text 的mMeasureWidth=1440px,mMeasureHeight=107px。

贴一下布局代码，免得你忘了具体布局。



```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout  xmlns:android="http://schemas.android.com/apk/res/android"    
   android:id="@+id/linear"
   android:layout_width="match_parent"    
   android:layout_height="wrap_content"    
   android:layout_marginTop="50dp"    
   android:background="@android:color/holo_blue_dark"    
   android:paddingBottom="70dp"    
   android:orientation="vertical">    
   <TextView        
    android:id="@+id/text"       
    android:layout_width="match_parent"     
    android:layout_height="wrap_content"  
    android:background="@color/material_blue_grey_800"       
    android:text="TextView"        
    android:textColor="@android:color/white"        
    android:textSize="20sp" />    
   <View       
      android:id="@+id/view"       
     android:layout_width="match_parent" 
     android:layout_height="150dp"    
     android:background="@android:color/holo_green_dark" />
</LinearLayout>
```

TextView的高度已经测量出来了，接下来测量id/linear的第二个child（id/view），同样的原理测出id/view的MeasureSpec.

![img](https:////upload-images.jianshu.io/upload_images/966283-55810a48922ac8fe.png?imageMogr2/auto-orient/strip|imageView2/2/w/761/format/webp)

Paste_Image.png

id/view的MeasureSpec 计算出来后，调用view.measure(childWidthMeasureSpec, childHeightMeasureSpec)的测量id/view的高宽，之前已经说过View measure的默认实现是



```java
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {    
  setMeasuredDimension(
  getDefaultSize(getSuggestedMinimumWidth(), widthMeasureSpec),            
  getDefaultSize(getSuggestedMinimumHeight(), heightMeasureSpec));
}
```

最终算出id/view的mMeasureWidth=1440px,mMeasureHeight=600px。

id/linear 的子View的高度都计算完毕了，接下来id/linear就通过所有子View的测量结果计算自己的高宽，id/linear是LinearLayout，所有它的高度计算简单理解就是子View的高度的累积+自己的Padding.

![img](https:////upload-images.jianshu.io/upload_images/966283-b089fd286ca7fc05.png?imageMogr2/auto-orient/strip|imageView2/2/w/693/format/webp)

最终算出id/linear的mMeasureWidth=1440px,mMeasureHeight=987px。

最终算出id/linear出来后，id/content 就要根据它唯一的子View id/linear 的测量结果和自己的之前算出的MeasureSpec一起来测量自己的结果，具体计算的逻辑去看FrameLayout onMeasure 函数的计算过程。以此类推，接下来测量ViewRoot,然后再测量id/statusBarBackground,虽然不知道id/statusBarBackground 是什么，但是调试的过程中，测出的它的高度=100px, 和 id/content 的paddingTop 刚好相等。在最后测量DecorView 的高宽，最终整个测量过程结束。所有的View的大小测量完毕。所有的getMeasureWidth 和 getMeasureWidth 都已经有值了。Measure 分析到此为止，如有不懂，评论留言（简书：kelin）

##### [2] layout过程

```java
mView.measure(childWidthMeasureSpec, childHeightMeasureSpec); 
......
mView.layout(0, 0, mView.getMeasuredWidth(), mView.getMeasuredHeight());
```

performTraversals 方法执行完mView.measure 计算出mMeasuredXXX后就开始执行layout 函数来确定View具体放在哪个位置，我们计算出来的View目前只知道view矩阵的大小，具体这个矩阵放在哪里，这就是layout 的工作了。layout的主要作用 ：**根据子视图的大小以及布局参数将View树放到合适的位置上**。

既然是通过mView.layout(0, 0, mView.getMeasuredWidth(), mView.getMeasuredHeight()); 那我们来看下layout 函数做了什么，mView肯定是个ViewGroup，不会是View,我们直接看下ViewGroup 的layout函数

```java
public final void layout(int l, int t, int r, int b) {    
   if (!mSuppressLayout && (mTransition == null || !mTransition.isChangingLayout())) {        
    if (mTransition != null) {            
       mTransition.layoutChange(this);        
    }       
    super.layout(l, t, r, b);    
    } else {        
    // record the fact that we noop'd it; request layout when transition finishes        
      mLayoutCalledWhileSuppressed = true;    
   }
}
```

代码可以看个大概，LayoutTransition是用于处理ViewGroup增加和删除子视图的动画效果，也就是说如果当前ViewGroup未添加LayoutTransition动画，或者LayoutTransition动画此刻并未运行，那么调用super.layout(l, t, r, b)，继而调用到ViewGroup中的onLayout，否则将mLayoutSuppressed设置为true，等待动画完成时再调用requestLayout()。
 这个函数是final 不能重写，所以ViewGroup的子类都会调用这个函数，layout 的具体实现是在super.layout(l, t, r, b)里面做的，那么我接下来看一下View类的layout函数

```java
 public final void layout(int l, int t, int r, int b) {
       .....
      //设置View位于父视图的坐标轴
       boolean changed = setFrame(l, t, r, b); 
       //判断View的位置是否发生过变化，看有必要进行重新layout吗
       if (changed || (mPrivateFlags & LAYOUT_REQUIRED) == LAYOUT_REQUIRED) {
           if (ViewDebug.TRACE_HIERARCHY) {
               ViewDebug.trace(this, ViewDebug.HierarchyTraceType.ON_LAYOUT);
           }
           //调用onLayout(changed, l, t, r, b); 函数
           onLayout(changed, l, t, r, b);
           mPrivateFlags &= ~LAYOUT_REQUIRED;
       }
       mPrivateFlags &= ~FORCE_LAYOUT;
       .....
   }
```

1、setFrame(l, t, r, b) 可以理解为给mLeft 、mTop、mRight、mBottom赋值，然后基本就能确定View自己在父视图的位置了，这几个值构成的矩形区域就是该View显示的位置，这里的具体位置都是相对与父视图的位置。

2、回调onLayout，对于View来说，onLayout只是一个空实现，一般情况下我们也不需要重载该函数,：

```java
protected void onLayout(boolean changed, int left, int top, int right, int bottom) {  

    }  
```

对于ViewGroup 来说，唯一的差别就是ViewGroup中多了关键字abstract的修饰，要求其子类必须重载onLayout函数。



```java
@Override  
protected abstract void onLayout(boolean changed,  
        int l, int t, int r, int b); 
```

而重载onLayout的目的就是安排其children在父视图的具体位置，那么如何安排子View的具体位置呢？



```java
 int childCount = getChildCount() ; 
  for(int i=0 ;i<childCount ;i++){
       View child = getChildAt(i) ;
       //整个layout()过程就是个递归过程
       child.layout(l, t, r, b) ;
    }
```

代码很简单，就是遍历自己的孩子，然后调用  child.layout(l, t, r, b) ，给子view 通过setFrame(l, t, r, b) 确定位置，而重点是(l, t, r, b) 怎么计算出来的呢。还记得我们之前测量过程，测量出来的MeasuredWidth和MeasuredHeight吗？还记得你在xml 设置的Gravity吗？还有RelativeLayout 的其他参数吗，没错，就是这些参数和MeasuredHeight、MeasuredWidth 一起来确定子View在父视图的具体位置的。具体的计算过程大家可以看下最简单FrameLayout 的onLayout 函数的源码，每个不同的ViewGroup  的实现都不一样，这边不做具体分析了吧。

3、MeasuredWidth和MeasuredHeight这两个参数为layout过程提供了一个很重要的依据（如果不知道View的大小，你怎么固定四个点的位置呢），但是这两个参数也不是必须的，layout过程中的4个参数l, t, r, b完全可以由我们任意指定，而View的最终的布局位置和大小（mRight - mLeft=实际宽或者mBottom-mTop=实际高）完全由这4个参数决定，measure过程得到的mMeasuredWidth和mMeasuredHeight提供了视图大小测量的值，但我们完全可以不使用这两个值，所以measure过程并不是必须的。如果我们不使用这两个值，那么getMeasuredWidth() 和getWidth() 就很有可能不是同一个值，它们的计算是不一样的：



```java
public final int getMeasuredWidth() {  
        return mMeasuredWidth & MEASURED_SIZE_MASK;  
    }  
public final int getWidth() {  
        return mRight - mLeft;  
    }
```

layout 过程相对简单些，分析就到此为止。

##### [3] draw过程

Draw过程比较简单，它的作用就是讲View绘制到屏幕上。View的绘制过程有以下几步：

1. 绘制背景 background.draw(canvas)
2. 绘制自己 （onDraw）
3. 绘制children（dispatchDraw）
4. 绘制装饰 （onDrawScrollBars）

------

performTraversals 方法的下一步就是mView.draw(canvas); 因为View的draw 方法一般不去重写，官网文档也建议不要去重写draw 方法，所以下一步执行就是View.java的draw 方法，我们来看下源码：

```java
public void draw(Canvas canvas) {
    ...
        /*
         * Draw traversal performs several drawing steps which must be executed
         * in the appropriate order:
         *
         *      1. Draw the background
         *      2. If necessary, save the canvas' layers to prepare for fading
         *      3. Draw view's content
         *      4. Draw children
         *      5. If necessary, draw the fading edges and restore layers
         *      6. Draw decorations (scrollbars for instance)
         */

        // Step 1, draw the background, if needed
    ...
        background.draw(canvas);
    ...
        // skip step 2 & 5 if possible (common case)
    ...
        // Step 2, save the canvas' layers
    ...
        if (solidColor == 0) {
            final int flags = Canvas.HAS_ALPHA_LAYER_SAVE_FLAG;

            if (drawTop) {
                canvas.saveLayer(left, top, right, top + length, null, flags);
            }
    ...
        // Step 3, draw the content
        if (!dirtyOpaque) onDraw(canvas);

        // Step 4, draw the children
        dispatchDraw(canvas);

        // Step 5, draw the fade effect and restore layers

        if (drawTop) {
            matrix.setScale(1, fadeHeight * topFadeStrength);
            matrix.postTranslate(left, top);
            fade.setLocalMatrix(matrix);
            canvas.drawRect(left, top, right, top + length, p);
        }
    ...
        // Step 6, draw decorations (scrollbars)
        onDrawScrollBars(canvas);
    }
```

注释写得比较清楚，一共分成6步，看到注释没有（  // skip step 2 & 5 if possible (common case)）除了2 和 5之外 我们一步一步来看：
 **第一步：背景绘制**
 看注释即可，不是重点

```java
private void drawBackground(Canvas canvas) { 
     Drawable final Drawable background = mBackground; 
      ...... 
     //mRight - mLeft, mBottom - mTop layout确定的四个点来设置背景的绘制区域 
     if (mBackgroundSizeChanged) { 
        background.setBounds(0, 0, mRight - mLeft, mBottom - mTop);   
        mBackgroundSizeChanged = false; rebuildOutline(); 
     } 
     ...... 
     //调用Drawable的draw() 把背景图片画到画布上
     background.draw(canvas); 
     ...... 
}
```

**第三步，对View的内容进行绘制。**
 onDraw(canvas) 方法是view用来draw 自己的，具体如何绘制，颜色线条什么样式就需要子View自己去实现，View.java 的onDraw(canvas) 是空实现，ViewGroup 也没有实现，每个View的内容是各不相同的，所以需要由子类去实现具体逻辑。

**第4步 对当前View的所有子View进行绘制**
 dispatchDraw(canvas) 方法是用来绘制子View的，View.java 的dispatchDraw()方法是一个空方法,因为View没有子View,不需要实现dispatchDraw ()方法，ViewGroup就不一样了，它实现了dispatchDraw ()方法：

```java
@Override
 protected void dispatchDraw(Canvas canvas) {
       ...
        if ((flags & FLAG_USE_CHILD_DRAWING_ORDER) == 0) {
            for (int i = 0; i < count; i++) {
                final View child = children[i];
                if ((child.mViewFlags & VISIBILITY_MASK) == VISIBLE || child.getAnimation() != null) {
                    more |= drawChild(canvas, child, drawingTime);
                }
            }
        } else {
            for (int i = 0; i < count; i++) {
                final View child = children[getChildDrawingOrder(count, i)];
                if ((child.mViewFlags & VISIBILITY_MASK) == VISIBLE || child.getAnimation() != null) {
                    more |= drawChild(canvas, child, drawingTime);
                }
            }
        }
      ......
    }
```

代码一眼看出，就是遍历子View然后drawChild(),drawChild()方法实际调用的是子View.draw()方法,ViewGroup类已经为我们实现绘制子View的默认过程，这个实现基本能满足大部分需求，所以ViewGroup类的子类（LinearLayout,FrameLayout）也基本没有去重写dispatchDraw方法，我们在实现自定义控件，除非比较特别，不然一般也不需要去重写它， drawChild()的核心过程就是为子视图分配合适的cavas剪切区，剪切区的大小正是由layout过程决定的，而剪切区的位置取决于滚动值以及子视图当前的动画。设置完剪切区后就会调用子视图的draw()函数进行具体的绘制了。

**第6步 对View的滚动条进行绘制**
 不是重点，知道有这东西就行，onDrawScrollBars 的一句注释 ：*Request the drawing of the horizontal and the vertical scrollbar. The  scrollbars are painted only if they have been awakened first.*

一张图看下整个draw的递归流程。



![img](https:////upload-images.jianshu.io/upload_images/966283-480bf9def58bed74.png?imageMogr2/auto-orient/strip|imageView2/2/w/670/format/webp)

到此整个绘制过程基本讲述完毕了。

#### 7. View事件分发机制 

https://www.jianshu.com/p/238d1b753e64

> 在android开发中会经常遇到滑动冲突（比如ScrollView或是SliddingMenu与ListView的嵌套）的问题，需要我们深入的了解android事件响应机制才能解决，事件响应机制已经是android开发者必不可少的知识。

##### [1] 涉及到事件响应的常用方法构成

　　用户在手指与屏幕接触过程中通过**MotionEvent对象**产生一系列事件，它有四种状态： 　　

- MotionEvent.ACTION_DOWN：手指按下屏幕的瞬间（一切事件的开始）
- MotionEvent.ACTION_MOVE：手指在屏幕上移动
- MotionEvent.ACTION_UP：手指离开屏幕瞬间
- MotionEvent.ACTION_CANCEL：取消手势，一般由程序产生，不会由用户产生

　　Android中的事件onClick, onLongClick，onScroll, onFling等等，都是由许多个Touch事件构成的（一个ACTION_DOWN， n个ACTION_MOVE，1个ACTION_UP）。

　　android 事件响应机制是先 **分发**（先由外部的View接收，然后依次传递给其内层的最小View）再 **处理** （从最小View单元（事件源）开始依次向外层传递。）的形式实现的。

　　复杂性表现在：可以控制每层事件是否继续传递（分发和拦截协同实现），以及事件的具体消费（事件分发也具有事件消费能力）。

##### [2] android事件处理涉及到的三个重要函数

> > - **public boolean dispatchTouchEvent(MotionEvent event)**
> >    通过方法名我们不难猜测，它就是事件分发的重要方法。那么很明显，如果一个MotionEvent传递给了View，那么dispatchTouchEvent方法一定会被调用！
> >    **返回值：表示是否消费了当前事件。可能是View本身的onTouchEvent方法消费，也可能是子View的dispatchTouchEvent方法中消费。返回true表示事件被消费，本次的事件终止。返回false表示View以及子View均没有消费事件，将调用父View的onTouchEvent方法**
>
> > - **public boolean onInterceptTouchEvent(MotionEvent ev)**
> >    事件拦截，当一个ViewGroup在接到MotionEvent事件序列时候，首先会调用此方法判断是否需要拦截。**特别注意，这是ViewGroup特有的方法，View并没有拦截方法**
> >    **返回值：是否拦截事件传递，返回true表示拦截了事件，那么事件将不再向下分发而是调用View本身的onTouchEvent方法。返回false表示不做拦截，事件将向下分发到子View的dispatchTouchEvent方法。**
>
> > - **public boolean onTouchEvent(MotionEvent ev)**
> >    真正对MotionEvent进行处理或者说消费的方法。在dispatchTouchEvent进行调用。
> >    **返回值：返回true表示事件被消费，本次的事件终止。返回false表示事件没有被消费，将调用父View的onTouchEvent方法**
>
> ~~~java
>     public boolean dispatchTouchEvent(MotionEvent ev) {
>         boolean consume = false;//事件是否被消费
>         if (onInterceptTouchEvent(ev)){//调用onInterceptTouchEvent判断是否拦截事件
>             consume = onTouchEvent(ev);//如果拦截则调用自身的onTouchEvent方法
>         }else{
>             consume = child.dispatchTouchEvent(ev);//不拦截调用子View的dispatchTouchEvent方法
>         }
>         return consume;//返回值表示事件是否被消费，true事件终止，false调用父View的onTouchEvent方法
>     }
> ~~~

ViewGroup是View的子类，也就是说**ViewGroup本身就是一个View**，但是它可以包含子View（当然**子View也可能是一个ViewGroup**），所以不难理解，上面所展示的伪代码表示的是ViewGroup 处理事件分发的流程。而View本身是不存在分发，所以也没有拦截方法（onInterceptTouchEvent），它只能在onTouchEvent方法中进行处理消费或者不消费。

![img](https://upload-images.jianshu.io/upload_images/2839355-61a4ace684282818.png?imageMogr2/auto-orient/strip|imageView2/2/w/930/format/webp)

[![这里写图片描述](https://camo.githubusercontent.com/d0cf3f58f4a42af93085a1b9ab45baa5a45450a1/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630343238313631313034333339)](https://camo.githubusercontent.com/d0cf3f58f4a42af93085a1b9ab45baa5a45450a1/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630343238313631313034333339)

（图来自网络）

##### [3] View源码分析

　　Android中ImageView、textView、Button等继承于View但没有重写的dispatchTouchEvent方法，所以都用的View的该方法进行事件分发。看View重要函数部分源码：

```java
public boolean dispatchTouchEvent(MotionEvent event) {
//返回true,表示该View内部消化掉了所有事件。返回false，表示View内部只处理了ACTION_DOWN事件，事件继续传递，向上级View(ViewGroup)传递。

    if (mOnTouchListener != null && (mViewFlags & ENABLED_MASK) == ENABLED &&
            mOnTouchListener.onTouch(this, event)) {
  //此处的onTouch方式就是回调的我们注册OnTouchListener时重写的onTouch()方法
        return true;
    }
    return onTouchEvent(event);
}
```

　首先进行三个条件的判断：

（1）查看是否给button设置了OnTouchListener()事件；

（2）控件是否Enable；（控件默认都是enable的）

（3）button里面实现的OnTouchListener监听里的onTouch()方法是否返回true；

　如果条件都满足，则该事件被消耗掉，不再进入onTouchEvent中处理。否则将事件将交给onTouchEvent方法处理。

```java
 public boolean onTouchEvent(MotionEvent event) {
    ...
 
   /＊ 当前onTouch的组件必须是可点击的比如Button，ImageButton等等，此处CLICKABLE为true，才会进入if方法，最后返回true。
 如果是ImageView、TexitView这些默认为不可点击的View,此处CLICKABLE为false，最后返回false。当然会有特殊情况，如果给这些View设置了onClick监听器，此处CLICKABLE也将为true　　＊／
 
    if (((viewFlags & CLICKABLE) == CLICKABLE ||  
            (viewFlags & LONG_CLICKABLE) == LONG_CLICKABLE)) {
        switch (event.getAction()) {
            case MotionEvent.ACTION_UP:
                ...
                            if (!post(mPerformClick)) {
                                performClick();// 实际就是回调了我们注册的OnClickListener中重新的onClick()方法
                            }
                 ...
                break;
 
            case MotionEvent.ACTION_DOWN:
               ...
                break;
 
            case MotionEvent.ACTION_CANCEL:
                ...
                break;
 
            case MotionEvent.ACTION_MOVE:
               ...
                break;
        }
        return true;
    }
 
    return false;
}
public boolean performClick() {
    ...
 ／／
    if (li != null && li.mOnClickListener != null) {
        ...
        li.mOnClickListener.onClick(this);
        return true;
    }
 
    return false;
}
 public void setOnClickListener(OnClickListener l) {
    if (!isClickable()) {
        setClickable(true);
    }
    getListenerInfo().mOnClickListener = l;
}
```

> 只有我们注册OnTouchListener时重写的 onTouch()方法中
>
> 返回false  —> 执行onTouchEvent方法 —>  导致onClick()回调方法执行　

返回true —> onTouchEvent方法不执行 —>  导致onClick()回调方法不会执行

##### [4] ViewGroup源码分析

　　Android中诸如LinearLayout等的五大布局控件，都是继承自ViewGroup，而ViewGroup本身是继承自View，所以ViewGroup的事件处理机制对这些控件都有效。

　　 部分源码：

```java
public boolean dispatchTouchEvent(MotionEvent ev) {  
       final int action = ev.getAction();  
       final float xf = ev.getX();  
       final float yf = ev.getY();  
       final float scrolledXFloat = xf + mScrollX;  
       final float scrolledYFloat = yf + mScrollY;  
       final Rect frame = mTempRect;  
  
       //这个值默认是false, 然后我们可以通过requestDisallowInterceptTouchEvent(boolean disallowIntercept)方法  
       //来改变disallowIntercept的值  
       boolean disallowIntercept = (mGroupFlags & FLAG_DISALLOW_INTERCEPT) != 0;  
  
       //这里是ACTION_DOWN的处理逻辑  
       if (action == MotionEvent.ACTION_DOWN) {  
        //清除mMotionTarget, 每次ACTION_DOWN都很设置mMotionTarget为null  
           if (mMotionTarget != null) {  
               mMotionTarget = null;  
           }  
  
           //disallowIntercept默认是false, 就看ViewGroup的onInterceptTouchEvent()方法  
           if (disallowIntercept || !onInterceptTouchEvent(ev)) {  //第一点
               ev.setAction(MotionEvent.ACTION_DOWN);  
               final int scrolledXInt = (int) scrolledXFloat;  
               final int scrolledYInt = (int) scrolledYFloat;  
               final View[] children = mChildren;  
               final int count = mChildrenCount;  
               //遍历其子View  
               for (int i = count - 1; i >= 0; i--) {  //第二点
                   final View child = children[i];  
                     
                   //如果该子View是VISIBLE或者该子View正在执行动画, 表示该View才  
                   //可以接受到Touch事件  
                   if ((child.mViewFlags & VISIBILITY_MASK) == VISIBLE  
                           || child.getAnimation() != null) {  
                    //获取子View的位置范围  
                       child.getHitRect(frame);  
                         
                       //如Touch到屏幕上的点在该子View上面  
                       if (frame.contains(scrolledXInt, scrolledYInt)) {  
                           // offset the event to the view's coordinate system  
                           final float xc = scrolledXFloat - child.mLeft;  
                           final float yc = scrolledYFloat - child.mTop;  
                           ev.setLocation(xc, yc);  
                           child.mPrivateFlags &= ~CANCEL_NEXT_UP_EVENT;  
                             
                           //调用该子View的dispatchTouchEvent()方法  
                           if (child.dispatchTouchEvent(ev))  {  
                               // 如果child.dispatchTouchEvent(ev)返回true表示  
                            //该事件被消费了，设置mMotionTarget为该子View  
                               mMotionTarget = child;  
                               //直接返回true  
                               return true;  
                           }  
                           // The event didn't get handled, try the next view.  
                           // Don't reset the event's location, it's not  
                           // necessary here.  
                       }  
                   }  
               }  
           }  
       }  
  
       //判断是否为ACTION_UP或者ACTION_CANCEL  
       boolean isUpOrCancel = (action == MotionEvent.ACTION_UP) ||  
               (action == MotionEvent.ACTION_CANCEL);  
  
       if (isUpOrCancel) {  
           //如果是ACTION_UP或者ACTION_CANCEL, 将disallowIntercept设置为默认的false  
        //假如我们调用了requestDisallowInterceptTouchEvent()方法来设置disallowIntercept为true  
        //当我们抬起手指或者取消Touch事件的时候要将disallowIntercept重置为false  
        //所以说上面的disallowIntercept默认在我们每次ACTION_DOWN的时候都是false  
           mGroupFlags &= ~FLAG_DISALLOW_INTERCEPT;  
       }  
  
       // The event wasn't an ACTION_DOWN, dispatch it to our target if  
       // we have one.  
       final View target = mMotionTarget;  
       //mMotionTarget为null意味着没有找到消费Touch事件的View, 所以我们需要调用ViewGroup父类的  
       //dispatchTouchEvent()方法，也就是View的dispatchTouchEvent()方法  
       if (target == null) {  
           // We don't have a target, this means we're handling the  
           // event as a regular view.  
           ev.setLocation(xf, yf);  
           if ((mPrivateFlags & CANCEL_NEXT_UP_EVENT) != 0) {  
               ev.setAction(MotionEvent.ACTION_CANCEL);  
               mPrivateFlags &= ~CANCEL_NEXT_UP_EVENT;  
           }  
           return super.dispatchTouchEvent(ev);  
       }  
  
       //这个if里面的代码ACTION_DOWN不会执行，只有ACTION_MOVE  
       //ACTION_UP才会走到这里, 假如在ACTION_MOVE或者ACTION_UP拦截的  
       //Touch事件, 将ACTION_CANCEL派发给target，然后直接返回true  
       //表示消费了此Touch事件  
       if (!disallowIntercept && onInterceptTouchEvent(ev)) {  
           final float xc = scrolledXFloat - (float) target.mLeft;  
           final float yc = scrolledYFloat - (float) target.mTop;  
           mPrivateFlags &= ~CANCEL_NEXT_UP_EVENT;  
           ev.setAction(MotionEvent.ACTION_CANCEL);  
           ev.setLocation(xc, yc);  
             
           if (!target.dispatchTouchEvent(ev)) {  
           }  
           // clear the target  
           mMotionTarget = null;  
           // Don't dispatch this event to our own view, because we already  
           // saw it when intercepting; we just want to give the following  
           // event to the normal onTouchEvent().  
           return true;  
       }  
  
       if (isUpOrCancel) {  
           mMotionTarget = null;  
       }  
  
       // finally offset the event to the target's coordinate system and  
       // dispatch the event.  
       final float xc = scrolledXFloat - (float) target.mLeft;  
       final float yc = scrolledYFloat - (float) target.mTop;  
       ev.setLocation(xc, yc);  
  
       if ((target.mPrivateFlags & CANCEL_NEXT_UP_EVENT) != 0) {  
           ev.setAction(MotionEvent.ACTION_CANCEL);  
           target.mPrivateFlags &= ~CANCEL_NEXT_UP_EVENT;  
           mMotionTarget = null;  
       }  
  
       //如果没有拦截ACTION_MOVE, ACTION_DOWN的话，直接将Touch事件派发给target  
       return target.dispatchTouchEvent(ev);  
   }
```

> 1、dispatchTouchEvent作用：决定事件是否由onInterceptTouchEvent来拦截处理。 返回super.dispatchTouchEvent时，由onInterceptTouchEvent来决定事件的流向 返回false时，会继续分发事件，自己内部只处理了ACTION_DOWN 返回true时，不会继续分发事件，自己内部处理了所有事件（ACTION_DOWN,ACTION_MOVE,ACTION_UP）

> 2、onInterceptTouchEvent作用：拦截事件，用来决定事件是否传向子View 返回true时，拦截后交给自己的onTouchEvent处理 返回false时，拦截后交给子View来处理

> 3、onTouchEvent作用：事件最终到达这个方法 返回true时，内部处理所有的事件，换句话说，后续事件将继续传递给该view的onTouchEvent()处理 返回false时，事件会向上传递，由onToucEvent来接受，如果最上面View中的onTouchEvent也返回false的话，那么事件就会消失

##### [5] 总结

- 如果ViewGroup找到了能够处理该事件的View，则直接交给子View处理，自己的onTouchEvent不会被触发；　
- 可以通过复写onInterceptTouchEvent(ev)方法，拦截子View的事件（即return true），把事件交给自己处理，则会执行自己对应的onTouchEvent方法。
- 子View可以通过调用getParent().requestDisallowInterceptTouchEvent(true);  阻止ViewGroup对其MOVE或者UP事件进行拦截；　　
- 一个点击事件产生后，它的传递过程如下： Activity->Window->View。顶级View接收到事件之后，就会按相应规则去分发事件。如果一个View的onTouchEvent方法返回false，那么将会交给父容器的onTouchEvent方法进行处理，逐级往上，如果所有的View都不处理该事件，则交由Activity的onTouchEvent进行处理。　
- 如果某一个View开始处理事件，如果他不消耗ACTION_DOWN事件（也就是onTouchEvent返回false），则同一事件序列比如接下来进行ACTION_MOVE，则不会再交给该View处理。
- ViewGroup默认不拦截任何事件。　
- 诸如TextView、ImageView这些不作为容器的View，一旦接受到事件，就调用onTouchEvent方法，它们本身没有onInterceptTouchEvent方法。正常情况下，它们都会消耗事件（返回true），除非它们是不可点击的（clickable和longClickable都为false），那么就会交由父容器的onTouchEvent处理。　
- 点击事件分发过程如下 dispatchTouchEvent—->OnTouchListener的onTouch方法—->onTouchEvent-->OnClickListener的onClick方法。也就是说，我们平时调用的setOnClickListener，优先级是最低的，所以，onTouchEvent或OnTouchListener的onTouch方法如果返回true，则不响应onClick方法...

#### 8. MVC&MVP&MVVM

#### 9. intentService

#### 10. 内存泄露

#### 11. binder机制 

