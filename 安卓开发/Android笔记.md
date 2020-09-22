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

上面的代码有点多，希望你仔细看一些注释，代码写得很多，其实计算原理很简单!!!!!!：
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

1、如果子View 的layout_xxxx是MATCH_PARENT，因为父View的MeasureSpec是UNSPECIFIED，父View自己的大小并没有任何约束和要求，那么对于子View来说无论是WRAP_CONTENT还是MATCH_PARENT，子View也是没有任何束缚的，想多大就多大，没有不能超过多少的要求，一旦没有任何要求和约束，size的值就没有任何意义了，所以一般都直接设置成0

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
> > - **public boolean onIntercept(拦截)TouchEvent(MotionEvent ev)**
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

> 前言：做客户端开发、前端开发，大致都应该听说过这么几个名词MVC、MVP、MVVM，这些架构的思想大多是为了解决界面应用程序复杂的逻辑问题。同时这些框架的核心目的在于，职责分离，不同的层次要做不同的事情。

无论是哪种MV**系列，都涉及到了Model和View，如果单纯的只有Model和View，他们是没有办法一起协同工作的，所以就有了各种MV..的设计模式

**MVXX模式：**

- MVC
- MVP
- MVVM

这三种架构模式都是现在比较流行的，在不同的项目中，可能采用不同的架构模式，今天我们就围绕着这三种架构模式的试用场景介绍一下他们的概念，以及异同。

##### [1] MVC

[<img src="https://camo.githubusercontent.com/8de6460e4d41c88ad2cf5432caae6b10f82d196e/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76632d6465702e706e67" alt="img" style="zoom:50%;" />](https://camo.githubusercontent.com/8de6460e4d41c88ad2cf5432caae6b10f82d196e/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76632d6465702e706e67)

**MVC(Model-View-Controller),Model:逻辑模型，View:视图模型，Controller控制器**。简单说这就是一种设计应用程序的思想，目的在于将业务逻辑、数据、界面分离，将业务逻辑聚集到一个部件里面，在改进或者想要定制界面及用户交互时，不需要重写编写业务逻辑。**Controller和View都依赖Model层，Controller和View相互依赖。**

操作的过程：用户在界面上进行操作(例如手机屏幕)，这个时候View会捕捉到用户的操作，然后将这个操作的处理权利交给Controller，Controller会对来自View的数据进行预处理，决定调用哪个Model的接口，然后由Model执行相应的逻辑，当Model变更之后，再利用观察者模式通知View，View通过观察者模式收到Model的消息之后，向Model请求最新的数据，然后更新页面，如下图：

[<img src="https://camo.githubusercontent.com/b89ac314c2fd554e7bf33ba1553e10dd91be44fc/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76632d63616c6c2e706e67" alt="img" style="zoom:50%;" />](https://camo.githubusercontent.com/b89ac314c2fd554e7bf33ba1553e10dd91be44fc/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76632d63616c6c2e706e67)

看似没有什么特别的地方，但是由几个需要特别关注的关键点：

1. View是把控制权交移给Controller，Controller执行应用程序相关的应用逻辑（对来自View数据进行预处理、决定调用哪个Model的接口等等）。
2. Controller操作Model，Model执行业务逻辑对数据进行处理。但不会直接操作View，可以说它是对View无知的。
3. View和Model的同步消息是通过观察者模式进行，而同步操作是由View自己请求Model的数据然后对视图进行更新。

需要特别注意的是MVC模式的精髓在于第三点**：Model的更新是通过观察者模式告知View的**，具体表现形式可以是Pub/Sub或者是触发Events。而网上很多对于MVC的描述都没有强调这一点。**通过观察者模式的好处就是：不同的MVC三角关系可能会有共同的Model，一个MVC三角中的Controller操作了Model以后，两个MVC三角的View都会接受到通知，然后更新自己**。保持了依赖同一块Model的不同View显示数据的实时性和准确性。我们每天都在用的观察者模式，在几十年前就已经被大神们整合到MVC的架构当中。

**优点**

1. 首先最重要的一点是多个视图能共享一个模型，同一个模型可以被不同的视图重用，大大提高了代码的可重用性。
2. 由于MVC的三个模块相互独立，在其中改变一个，其他两个可以保持不变，这样可以把耦合降得很低，这样可以使开发人员可以只关注整个系统中的某一层
3. 控制器提高了应用程序的灵活性和可配置型。控制器可以用来连接不同的模型和视图去完成用户的需求，这样控制器可以为构造应用程序提供强有力的手段

**缺点**

1. 增加了系统结构的实现的复杂性
2. 视图与控制器之间的联系过于紧密，视图如果没有控制器的存在，能够做的事情少之又少，这样视图就很难独立应用了
3. 视图对模型的数据的访问效率过低，因为之间需要多次的调用
4. View无法组件化，View依赖于特定的Model，如果需要把这个View抽出来用在下一个应用程序复用就比较困难了

##### [2] MVP

Model(Model View Presenter),Model:逻辑模型，View:视图模型，Presenter:接口。

关于MVP的定义：

```
- MVC的演化版本，让Model和View完全解耦
- 代码清晰，不过增加了很多类
```

MVP中的P，是Presenter的含义，和MVC比较类似，都是将用户对View的操作交付给Presenter，Presenter会执行相应的逻辑，在这过程中会操作Model，当Model执行完业务逻辑之后，同样是通过观察者模式把自己的结果传递出去，不过不是告诉View，而是告诉Presenter，Presenter得到消息后，通过View的接口更新页面。

在Android中，我们的View可能仅仅就是个布局文件，它能做的事情少之又少，真正与布局文件进行数据绑定操作的事Activity，所以这样做就使Activity即像View又像Controller。

应用了MVP之后：

```
- View:对应Activity，负责View的绘制以及与用户交互
- Model:业务逻辑和实体模型
- Presenter:负责完成View与Model之间的交互
```

应用两张图来说明上述内容:

[<img src="https://camo.githubusercontent.com/e2b5d4479225546bfafa3702069e7a7e035e5e48/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132383335353534" alt="img" style="zoom:50%;" />](https://camo.githubusercontent.com/e2b5d4479225546bfafa3702069e7a7e035e5e48/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132383335353534)

[<img src="https://camo.githubusercontent.com/ab02cad1c475e9abde495cec526bc6744c3eceae/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132383536303131" alt="img" style="zoom:50%;" />](https://camo.githubusercontent.com/ab02cad1c475e9abde495cec526bc6744c3eceae/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132383536303131)

**MVP的优点**

1. 便于测试。Presenter对View是通过接口进行，在对Presenter进行不依赖UI环境的单元测试的时候。可以通过Mock一个View对象，这个对象只需要实现了View的接口即可。然后依赖注入到Presenter中，单元测试的时候就可以完整的测试Presenter应用逻辑的正确性。这里根据上面的例子给出了Presenter的单元测试样例。
2. View可以进行组件化。在MVP当中，View不依赖Model。这样就可以让View从特定的业务场景中脱离出来，可以说View可以做到对业务完全无知。它只需要提供一系列接口提供给上层操作。这样就可以做到高度可复用的View组件。

**MVP的缺点**

1. 代码量会一些，实现的难度也会增加一些

**MVP与MVC区别**

如下图所示：

[<img src="https://camo.githubusercontent.com/ffe3507510be194890acf2d449e35e3df123c941/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132393136303534" alt="img" style="zoom: 67%;" />](https://camo.githubusercontent.com/ffe3507510be194890acf2d449e35e3df123c941/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530363232323132393136303534)

##### [3] MVVM

MVVM是Model-View-ViewModel的简写，MVVM是思想上的一种变革，也可以看成是MVP的一种变革，它是将"数据模型数据双向绑定"的思想作为核心，因此在View和Model之间便不需要我们写联系了，我们在修改数据的时候视图就可以发生变化，我们在修改视图的时候数据也是会发生变化的，可以在一定程度上提高我们的开发效率的。

**调用关系**

MVVM的调用关系和MVP一样。但是，在ViewModel当中会有一个叫Binder，或者是Data-binding engine的东西。以前全部由Presenter负责的View和Model之间数据同步操作交由给Binder处理。你只需要在View的模版语法当中，指令式地声明View上的显示的内容是和Model的哪一块数据绑定的。当ViewModel对进行Model更新的时候，Binder会自动把数据更新到View上去，当用户对View进行操作（例如表单输入），Binder也会自动把数据更新到Model上去。这种方式称为：Two-way data-binding，双向数据绑定。可以简单而不恰当地理解为一个模版引擎，但是会根据数据变更实时渲染。

[![img](https://camo.githubusercontent.com/61ef7578cd46b1d37dd3ea52ce0a3be570e427cc/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76766d2d63616c6c2e706e67)](https://camo.githubusercontent.com/61ef7578cd46b1d37dd3ea52ce0a3be570e427cc/687474703a2f2f6c69766f7261732e6769746875622e696f2f626c6f672f6d76632f6d76766d2d63616c6c2e706e67)

也就是说，MVVM把View和Model的同步逻辑自动化了。以前Presenter负责的View和Model同步不再手动地进行操作，而是交由框架所提供的Binder进行负责。只需要告诉Binder，View显示的数据对应的是Model哪一部分即可。

Android官方推出的MVVM的DataBinding，便是一个双向绑定的库。

**优点**

1. 提高可维护性。解决了MVP大量的手动View和Model同步的问题，提供双向绑定机制。提高了代码的可维护性。
2. 简化测试。因为同步逻辑是交由Binder做的，View跟着Model同时变更，所以只需要保证Model的正确性，View就正确。大大减少了对View同步更新的测试。

**缺点**

1. 过于简单的图形界面不适用，或说牛刀杀鸡。
2. 对于大型的图形应用程序，视图状态较多，ViewModel的构建和维护的成本都会比较高。
3. 数据绑定的声明是指令式地写在View的模版当中的，这些内容是没办法去打断点debug的。

#### 9. 内存泄露

##### [1] 前言

对于C++来说，内存泄漏就是new出来的对象没有delete；
对于Java来说，就是new出来的Object 放在Heap上无法被GC回收；

![img](https://pic3.zhimg.com/80/v2-4a25eb2147ada794725317d4be1bf9de_720w.png)



本文通过QQ和Qzone中内存泄漏实例来讲android中内存泄漏分析解法和编写代码应注意的事项。

##### [2] Java 中的内存分配

1. **静态储存区**：编译时就分配好，在程序整个运行期间都存在。它主要存放静态数据和常量；
2. **栈区**：当方法执行时，会在栈区内存中创建方法体内部的局部变量，方法结束后自动释放内存；
3. **堆区**：通常存放 new 出来的对象。由 Java 垃圾回收器回收。

##### [3] 四种引用类型的介绍

1. **强引用**(StrongReference)：JVM 宁可抛出 OOM ，也不会让 GC 回收具有强引用的对象；
2. **软引用**(SoftReference)：只有在内存空间不足时，才会被回的对象；
3. **弱引用**(WeakReference)：在 GC 时，一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存；
4. **虚引用**(PhantomReference)：任何时候都可以被GC回收，当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之关联的引用队列中。程序可以通过判断引用队列中是否存在该对象的虚引用，来了解这个对象是否将要被回收。可以用来作为GC回收Object的标志。

**我们常说的内存泄漏是指new出来的Object无法被GC回收，即为强引用：**

![img](https://pic3.zhimg.com/80/v2-15fbde414508a22c98c9fc6acbc65dad_720w.jpg)



内存泄漏发生时的主要表现为内存抖动，可用内存慢慢变少：

![img](https://pic3.zhimg.com/80/v2-4483280b8b2bab984b40251648f92222_720w.png)



##### [4] Andriod 中分析内存泄漏的工具MAT

MAT（Memory Analyzer Tools）是一个 Eclipse 插件，它是一个快速、功能丰富的JAVA heap分析工具，它可以帮助我们查找内存泄漏和减少内存消耗。

MAT 插件的下载地址：

> [Eclipse Memory Analyzer Open Source Project](https://link.zhihu.com/?target=http%3A//www.eclipse.org/mat/)

MAT 使用方法介绍：

> [内存泄漏 之 MAT工具的使用 - 狐狸已化妖 - 博客园](https://link.zhihu.com/?target=http%3A//www.cnblogs.com/larack/p/6071209.html)

##### [5] QQ 和 Qzone内存泄漏如何监控

![img](https://pic3.zhimg.com/80/v2-f6eb4f13fb1964a3f9807c7112166e1a_720w.png)



QQ和Qzone 的内存泄漏采用SNGAPM解决方案，SNGAPM是一个性能监控、分析的统一解决方案，它从终端收集性能信息，上报到一个后台，后台将监控类信息聚合展示为图表，将分析类信息进行分析并提单，通知开发者；

1. SNGAPM由App（MagnifierApp）和 web server（MagnifierServer）两部分组成；
2. MagnifierApp在自动内存泄漏检测中是一个衔接检测组件（LeakInspector）和自动化云分析（MagnifierCloud）的中间性平台，它从LeakInspector的内存dump自动化上传MagnifierServer；
3. MagnifierServer后台会定时提交分析任务到MagnifierCloud；
4. MagnifierCloud分析结束之后会更新数据到magnifier web上，同时以bug单形式通知开发者。

##### [6] 常见的内存泄漏案例

###### case 1. 单例造成的内存泄露

单例的静态特性导致其生命周期同应用一样长。

**解决方案：**

> 1. 将该属性的引用方式改为弱引用;
> 2. 如果传入Context，使用ApplicationContext;

**example：泄漏代码片段**

```text
 private static ScrollHelper mInstance;    
 private ScrollHelper() {
 }    
 public static ScrollHelper getInstance() {        
     if (mInstance == null) {           
        synchronized (ScrollHelper.class) {                
             if (mInstance == null) {
                 mInstance = new ScrollHelper();
             }
         }
     }        

     return mInstance;
 }    
 /**
  * 被点击的view
  */
 private View mScrolledView = null;    
 public void setScrolledView(View scrolledView) {
     mScrolledView = scrolledView;
 }
```

**Solution：使用WeakReference**

```text
 private static ScrollHelper mInstance;    
 private ScrollHelper() {
 }    
 public static ScrollHelper getInstance() {        
     if (mInstance == null) {            
         synchronized (ScrollHelper.class) {                
             if (mInstance == null) {
                 mInstance = new ScrollHelper();
             }
         }
     }        

     return mInstance;
 }    
 /**
  * 被点击的view
  */
 private WeakReference<View> mScrolledViewWeakRef = null;    
 public void setScrolledView(View scrolledView) {
     mScrolledViewWeakRef = new WeakReference<View>(scrolledView);
 }
```

###### case 2. InnerClass匿名内部类

在Java中，**非静态内部类** 和 **匿名类** 都会潜在的引用它们所属的外部类，但是，静态内部类却不会。如果这个非静态内部类实例做了一些耗时的操作，就会造成外围对象不会被回收，从而导致内存泄漏。

**解决方案：**

> 1. 将内部类变成静态内部类;
>
> 2. 如果有强引用Activity中的属性，则将该属性的引用方式改为弱引用;
>
> 3. 在业务允许的情况下，当Activity执行onDestory时，结束这些耗时任务;
>
> 4. 那么非静态内部类为什么持有外部类的引用？
>
>    **因为非静态内部类依赖着外部类，没有外部类就不能创建内部类。**

**example：**

```text
 public class LeakAct extends Activity {  
     @Override
     protected void onCreate(Bundle savedInstanceState) {    
         super.onCreate(savedInstanceState);
         setContentView(R.layout.aty_leak);
         test();
     } 
     //这儿发生泄漏    
     public void test() {    
         new Thread(new Runnable() {      
             @Override
             public void run() {        
                 while (true) {          
                     try {
                         Thread.sleep(1000);
                     } catch (InterruptedException e) {
                         e.printStackTrace();
                     }
                 }
             }
         }).start();
     }
 }
```

**Solution：**

```text
 public class LeakAct extends Activity {  
     @Override
     protected void onCreate(Bundle savedInstanceState) {    
         super.onCreate(savedInstanceState);
         setContentView(R.layout.aty_leak);
         test();
     }  
     //加上static，变成静态匿名内部类
     public static void test() {    
         new Thread(new Runnable() {     
             @Override
             public void run() {        
                 while (true) {          
                     try {
                         Thread.sleep(1000);
                     } catch (InterruptedException e) {
                         e.printStackTrace();
                     }
                 }
             }
         }).start();
     }
 }
```

###### case 3. Activity Context 的不正确使用

在Android应用程序中通常可以使用两种Context对象：Activity和Application。当类或方法需要Context对象的时候常见的做法是使用第一个作为Context参数。这样就意味着View对象对整个Activity保持引用，因此也就保持对Activty的所有的引用。

假设一个场景，当应用程序有个比较大的Bitmap类型的图片，每次旋转是都重新加载图片所用的时间较多。为了提高屏幕旋转是Activity的创建速度，最简单的方法时将这个Bitmap对象使用Static修饰。 当一个Drawable绑定在View上，实际上这个View对象就会成为这份Drawable的一个Callback成员变量。而静态变量的生命周期要长于Activity。导致了当旋转屏幕时，**Activity无法被回收，而造成内存泄露**。

**解决方案：**

> 1. 使用ApplicationContext代替ActivityContext，因为ApplicationContext会随着应用程序的存在而存在，而不依赖于activity的生命周期；
> 2. 对Context的引用不要超过它本身的生命周期，慎重的对Context使用“static”关键字。Context里如果有线程，一定要在onDestroy()里及时停掉。

**example：**

```text
 private static Drawable sBackground;
 @Override
 protected void onCreate(Bundle state) {  
     super.onCreate(state);
     TextView label = new TextView(this);
     label.setText("Leaks are bad");  
     if (sBackground == null) {
         sBackground = getDrawable(R.drawable.large_bitmap);
     }
     label.setBackgroundDrawable(sBackground);
     setContentView(label);
 }
```

**Solution：**

```text
 private static Drawable sBackground;
 @Override
 protected void onCreate(Bundle state) {  
     super.onCreate(state);
     TextView label = new TextView(this);
     label.setText("Leaks are bad");  
     if (sBackground == null) {
         sBackground = getApplicationContext().getDrawable(R.drawable.large_bitmap);
     }
     label.setBackgroundDrawable(sBackground);
     setContentView(label);
 }
```

###### case 4. Handler引起的内存泄漏

**当Handler中有延迟的的任务或是等待执行的任务队列过长，由于消息持有对Handler的引用，而Handler又持有对其外部类的潜在引用**，这条引用关系会一直保持到消息得到处理，而导致了Activity无法被垃圾回收器回收，而导致了内存泄露。

**解决方案：**

> 1. 可以把Handler类放在单独的类文件中，或者使用静态内部类便可以避免泄露;
> 2. 如果想在Handler内部去调用所在的Activity,那么可以在handler内部使用弱引用的方式去指向所在Activity.使用Static + WeakReference的方式来达到断开Handler与Activity之间存在引用关系的目的。

**Solution：**

```text
 @Override
 protected void doOnDestroy() {        
     super.doOnDestroy();        
     if (mHandler != null) {
         mHandler.removeCallbacksAndMessages(null);
     }
     mHandler = null;
     mRenderCallback = null;
 }
```

###### case 5. 注册监听器的泄漏

系统服务可以通过Context.getSystemService 获取，它们负责执行某些后台任务，或者为硬件访问提供接口。如果Context 对象想要在服务内部的事件发生时被通知，那就需要把自己注册到服务的监听器中。然而，这会让服务持有Activity 的引用，如果在Activity onDestory时没有释放掉引用就会内存泄漏。

**解决方案：**

> 1. 使用ApplicationContext代替ActivityContext;
>    1. 在Activity执行onDestory时，调用反注册;

```text
 mSensorManager = (SensorManager) this.getSystemService(Context.SENSOR_SERVICE);
```

**Solution：**

```text
 mSensorManager = (SensorManager) getApplicationContext().getSystemService(Context.SENSOR_SERVICE);
```

下面是容易造成内存泄漏的系统服务：

```text
 InputMethodManager imm = (InputMethodManager) context.getApplicationContext().getSystemService(Context.INPUT_METHOD_SERVICE);
```

**Solution：**

```text
 protected void onDetachedFromWindow() {        
     if (this.mActionShell != null) {
         this.mActionShell.setOnClickListener((OnAreaClickListener)null);
     }        
     if (this.mButtonShell != null) { 
         this.mButtonShell.setOnClickListener((OnAreaClickListener)null);
     }        
     if (this.mCountShell != this.mCountShell) {
         this.mCountShell.setOnClickListener((OnAreaClickListener)null);
     }        
     super.onDetachedFromWindow();
 }
```

###### case 6. Cursor，Stream没有close，View没有recyle

资源性对象比如(Cursor，File文件等)往往都用了一些缓冲，我们在不使用的时候，应该及时关闭它们，以便它们的缓冲及时回收内存。它们的缓冲不仅存在于 java虚拟机内，还存在于java虚拟机外。如果我们仅仅是把它的引用设置为null,而不关闭它们，往往会造成内存泄漏。因为有些资源性对象，比如SQLiteCursor(在析构函数finalize(),如果我们没有关闭它，它自己会调close()关闭)，如果我们没有关闭它，系统在回收它时也会关闭它，但是这样的效率太低了。因此对于资源性对象在不使用的时候，应该调用它的close()函数，将其关闭掉，然后才置为null. 在我们的程序退出时一定要确保我们的资源性对象已经关闭。

**Solution：**

> 调用onRecycled()

```text
 @Override
 public void onRecycled() {
     reset();
     mSinglePicArea.onRecycled();
 }
```

在View中调用reset()

```text
 public void reset() {
     if (mHasRecyled) {            
         return;
     }
 ...
     SubAreaShell.recycle(mActionBtnShell);
     mActionBtnShell = null;
 ...
     mIsDoingAvatartRedPocketAnim = false;        
     if (mAvatarArea != null) {
             mAvatarArea.reset();
     }        
     if (mNickNameArea != null) {
         mNickNameArea.reset();
     }
 }
```

###### case 7. 集合中对象没清理造成的内存泄漏

我们通常把一些对象的引用加入到了集合容器（比如ArrayList）中，当我们不需要该对象时，并没有把它的引用从集合中清理掉，这样这个集合就会越来越大。如果这个集合是static的话，那情况就更严重了。
所以要在退出程序之前，将集合里的东西clear，然后置为null，再退出程序。

**解决方案：**

> 在Activity退出之前，将集合里的东西clear，然后置为null，再退出程序。

**Solution**

```text
 private List<EmotionPanelInfo> data;    
 public void onDestory() {        
     if (data != null) {
         data.clear();
         data = null;
     }
 }
```

###### case 8. WebView造成的泄露

当我们不要使用WebView对象时，应该调用它的destory()函数来销毁它，并释放其占用的内存，否则其占用的内存长期也不能被回收，从而造成内存泄露。

**解决方案：**

> 为webView开启另外一个进程，通过AIDL与主线程进行通信，WebView所在的进程可以根据业务的需要选择合适的时机进行销毁，从而达到内存的完整释放。

###### case 9. 构造Adapter时，没有使用缓存的ConvertView

初始时ListView会从Adapter中根据当前的屏幕布局实例化一定数量的View对象，同时ListView会将这些View对象 缓存起来。

当向上滚动ListView时，原先位于最上面的List Item的View对象会被回收，然后被用来构造新出现的最下面的List Item。

这个构造过程就是由getView()方法完成的，getView()的第二个形参View ConvertView就是被缓存起来的List Item的View对象(初始化时缓存中没有View对象则ConvertView是null)。

#### 10. 进程间通信

| 名称              | 优点                                                         | 缺点                                                         | 适用场景                                                     |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Bundle            | 简单易用                                                     | 只能传输Bundle支持的数据类型                                 | 四大组件间的进程间通信                                       |
| 文件共享          | 简单易用                                                     | 不适用高并发场景，并且无法做到进程间即时通信                 | 适用于无关发的情况下，交换简单的数据，对实时性要求不高的场景。 |
| AIDL              | 功能强大，支持一对多实时并发通信                             | 使用稍复杂，需要处理好线程间的关系                           | 一对多通信且有RPC需求                                        |
| Messenger         | 功能一般，支持一对多串行通信，支持实时通信                   | 不能很好地处理高并发的情形，不支持RPC，由于数据通过Message传输，因此只能传输Bundle支持的数据类型 | 低并发的一对多实时通信，无RPC需求，或者无需要返回结果的RPC需求 |
| ContentProvider   | 支持一对多的实时并发通信，在数据源共享方面功能强大，可通过Call方法扩展其它操作 | 可以理解为受约束的AIDL，主要提供对数据源的CRUD操作           | 一对多的进程间数据共享                                       |
| BroadcastReceiver | 操作简单，对持一对多实时通信                                 | 只支持数据单向传递，效率低且安全性不高                       | 一对多的低频率单向通信                                       |
| Socket            | 功能强大，可通过网络传输字节流，支持一对多实时并发通信       | 实现细节步骤稍繁琐，不支持直接的RPC                          | 网络间的数据交换                                             |

由于不同的进程拥有不同的数据空间，所以无论是应用内还是应用间，均无法通过共享内存来实现进程间通信。

##### **[1] 使用Bundle ( 搬豆 ) 的方式**

在Android中三大组件（Activity，Service，Receiver）都支持在Intent中传递Bundle数据，由于Bundle实现了Parcelable接口（一种特有的序列化方法），所以它可以很方便的在不同的进程之间进行传输。当在一个进程中启动另外一个进程的Activity，Service，Receiver时，可以在Bundle中附加需要传输给远程的进程的信息，并通过Intent发送出去。

putExtras(Bundle data)：向Intent中放入所需要“携带”的数据包。

Bundle getExtras()：取出Intent中所“携带”的数据包。

**注意：我们传输的数据必须基本数据类型或者能够被序列化。**

 **利用Bundle进行进程间通信，只能是单方向的简单数据传输，使用有一定的局限性。**

##### **[2] 使用文件共享的方式**

**文件共享：**将对象序列化之后保存到文件中，在通过反序列，将对象从文件中读取出来。此方式对文件的格式没有具体的要求，可以是文件、XML、JSON等。

**文件共享方式也存在着很大的局限性，如并发读/写问题，如读取的数据不完整或者读取的数据不是最新的。**文件共享适合在对数据同步要求不高的进程间通信，并且要妥善处理并发读/写的问题。

##### **[3] 使用Messenger的方式**

​    我们也可以通过Messenger来进行进程间通信，在Messenger中放入我们需要传递的数据，实现进程间数据传递。Messenger只能传递Message对象，Messenger是一种轻量级的IPC方案，它的底层实现是AIDL。

服务端

（1）：创建Service；

（2）：构造Handler对象，实现handlerMessage方法；

（3）：通过Handler对象，构造Messenger对象；

（4）：通过Service的onBind()返回这个Messenger对象底层的Binder对象；

客户端

（1）：创建Actvity；

（2）：绑定远程进程Service；

（3）：创建ServiceConnection,监听绑定服务的回调；

（4）：通过onServiceConnected()方法的参数，构造客户端Messenger对象；

（5）：通过Messenger向服务端发送消息。

Messenger的工作原理图：

![image-20200921093824422](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200921093824422.png)

Messenger内部消息处理使用Handler实现的，所以它是以串行的方式处理客服端发送过来的消息的，如果有大量的消息发送给服务器端，服务器端只能一个一个处理，如果并发量大的话用Messenger就不合适了，而且Messenger的主要作用就是为了传递消息，很多时候我们需要跨进程调用服务器端的方法，这种需求Messenger就无法做到了。

##### **[4] 使用AIDL的方式**

AIDL（Android Interface Definition Language）是一种IDL语言，用于生成可以在Android设备上两个进程之间进行进程间通信（IPC）的代码。

如果在一个进程中（例如Activity）要调用另一个进程中（例如Service）对象的操作，就可以使用AIDL生成可序列化的参数。AIDL是IPC的一个轻量级实现，Android也提供了一个工具，可以自动创建Stub（类架构，类骨架）。在应用间通信时，需要以下几步：

（1）：定义一个AIDL接口；

（2）：为远程服务（Service）实现对应Stub；

（3）：将服务“暴露”给客户程序使用；

只有当你允许来自不同的客户端访问你的服务并且需要处理多线程问题时你才必须使用AIDL，其他情况下都可以选择其他方法。**AIDL是处理多线程、多客户端并发访问的，而Messenger是单线程处理。**

##### **[5] 使用ContentProvider的方式**

ContentProvider（内容提供者）是Android中的四大组件之一，为了在应用程序之间进行数据交换，Android提供了ContentProvider，ContentProvider是不同应用之间进行数据交换的API，一旦某个应用程序通过ContentProvider暴露了自己的数据操作的接口，那么不管该应用程序是否启动，其他的应用程序都可以通过接口来操作接口内的数据，包括数据的增、删、改、查等操作。

开发一个ContentProvider：

（1）：定义自己的ContentProvider类，该类集成ContentProvider基类；

（2）：在AndroidMainfest.xml中注册这个ContentProvider，注册时要给ContentProvider绑定一个域名；

（3）：当注册好这个ContentProvider后，其他应用就可以访问ContentProvider暴露出来的数据了。

ContentProvider只是暴露出来可供其他应用操作的数据，其他应用则需要通过ContentProvider来操作。

使用ContentResolver操作数据：

（1）：调用Activity的getContentResolver()获取ContentResolver对象；

（2）：根据调用的ContentResolver的insert()、delete()、update()和query()方法操作数据库。

##### [6] 使用广播接收者（Broadcast）的方式

广播是一种被动跨进程通信方式。当某个程序向系统发送广播时，其他的应用程序只能被动地接收广播数据。

Broadcast Receiver本质上是一个系统级的监听器，它专门监听各个程序发出的Broadcast，因此它拥有自己的进程，只要存在与之匹配的Intent被广播出来，Broadcast Receiver总会被激发。只要注册了某个广播之后，广播接收者才能收到该广播。广播注册的一个行为是将自己感兴趣的Intent Filter注册到Android系统的AMS（Activity Manager Service）中，里面保存了一个Intent Filter列表。广播发送者将Intent Filter的action行为发送到AMS中，然后遍历AMS中的Intent Filter列表，看谁订阅了该广播，然后将消息遍历发送到注册了相应的Intent Filter或者Service中---也就是说：会调用抽象方法onReceive()方法。其中AMS起到了中间桥梁的作用。

程序启动Broadcast Receiver：

（1）：创建需要启动的Broadcast Receiver的intent；

（2）：调用Context的sendBroadcast()或者sendOrderBroadcast()方法来启动指定的BroadcastReceivert。

每当Broadcast事件发生后，系统会创建对应的Broadcast Receiver实例，并自动触发onReceiver()方法，onReceiver()方法执行完后，BroadcastReceiver实例就会被销毁。

**Tips：**onReceiver()方法中尽量不要做耗时操作，如果onReceiver()方法不能再10秒之内完成事件的处理，Android会认为该进程无响应，也就弹出我们熟悉的ANR。

##### **[7] 使用Socket的方式**

Socket也是实现进程间通信的一种方式，Socket也称为“套接字”（网络通信中概念），通过Socket也可以实现跨进程通信，Socaket主要还是应用在网络通信中。

##### **[8] Android 进程间通信不同方式的比较**

- Bundle:四大组件间的进程间通信方式，简单易用，但传输的数据类型受限。
- 文件共享： 不适合高并发场景，并且无法做到进程间的及时通信。
- Messenger: 数据通过Message传输，只能传输Bundle支持的类型。
- ContentProvider：android 系统提供的，简单易用，但使用受限，只能根据特定规则访问数据。
- AIDL:功能强大，支持实时通信，但使用稍微复杂。
- Socket：网络数据交换的常用方式。

#### 11.okhttp原理

> https://www.jianshu.com/p/d98be38a6d3f 
>
> https://juejin.im/post/6844903557632622605

1. 当我们通过**OkhttpClient**创立一个**Call**，并发起**同步**或者**异步**请求时；

2. okhttp会通过Dispatcher对我们所有的RealCall（Call的具体实现类）进行统一管理，并通过**execute()**及**enqueue()**方法对同步或者异步请求进行解决；

3. execute()及enqueue()这两个方法会最终调用RealCall中的**getResponseWithInterceptorChain()**方法，从**阻拦器链**中获取返回结果；

4. 阻拦器链中，依次通过**RetryAndFollowUpInterceptor**（重定向阻拦器）、**BridgeInterceptor**（桥接阻拦器）、**CacheInterceptor**（缓存阻拦器）、**ConnectInterceptor**（连接阻拦器）、**CallServerInterceptor**（网络阻拦器）对请求依次解决，与服务的建立连接后，获取返回数据，再经过上述**阻拦器依次解决后，最后将结果返回给调用方。**

   >**网络配置层**：利用Builder模式配置各种参数，例如：超时时间、拦截器等，这些参数都会由Okhttp分发给各个需要的子系统。
   >**重定向层**：负责重定向。
   >
   >**Header拼接层：**负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。
   >
   >**HTTP缓存层**：负责读取缓存以及更新缓存。
   >
   >**连接层**：连接层是一个比较复杂的层级，它实现了网络协议、内部的拦截器、安全性认证，连接与连接池等功能，但这一层还没有发起真正的连接，它只是做了连接器一些参数的处理。
   >
   >**数据响应层**：负责从服务器读取响应的数据。

5. **责任链模式：责任链模式将各个拦截器连接环环相扣，最终完成一次网络请求。**最核心的方法是处理类， 一般处理类会包含一个指向下一处理类的成员变量，和一个处理请求的方法 ， 如果符合条件就自己处理，否则就传递给下一个处理。

![img](https://upload-images.jianshu.io/upload_images/6855581-bee0a351e8eeb0e8?imageMogr2/auto-orient/strip|imageView2/2/w/853/format/webp)

> **建造者模式：**使用多个简单的对象一步一步构建成一个复杂的对象。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
>
> **责任链模式**：为请求创建了一个接收者对象的链。这种模式给予请求的类型，对请求的发送者和接收者进行解耦。这种类型的设计模式属于行为型模式。在这种模式中，通常**每个接收者都包含对另一个接收者的引用**。如果一个对象不能处理该请求，那么它会把相同的请求传给下一个接收者，依此类推。
>
> **优势：**避免请求发送者与接收者耦合在一起，让多个对象都有可能接收请求，将这些对象连接成一条链，并且沿着这条链传递请求，直到有对象处理它为止

​                       ![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcuc29uZ21hLmNvbS93ZW56aGFuZy8yMDE4MTIxNi9zcnF6M2doMmUxdTEzMi5wbmc?x-oss-process=image/format,png)

##### [1] **文章目录**

>**一 请求与响应流程**
>
>- 1.1 请求的封装
>- 1.2 请求的发送
>- 1.3 请求的调度
>
>**二 拦截器**
>
>- 2.1 RetryAndFollowUpInterceptor
>- 2.2 BridgeInterceptor
>- 2.3 CacheInterceptor
>- 2.4 ConnectInterceptor
>- 2.5 CallServerInterceptor
>
>**三 连接机制**
>
>- 3.1 建立连接
>- 3.2 连接池
>
>**四 缓存机制**
>
>- 4.1 缓存策略
>- 4.2 缓存管理

在Android刀耕火种的哪个年代，我们做网络请求通常会选用HttpURLConnection或者Apache HTTP Client，这两者均支持HTTPS、流的上传和下载、配置超时和连接池等特性，但随着业务场景的负责化以及 对流量消耗的优化需求，Okhttp应运而生，自诞生起，口碑就一直很好。

> An HTTP+HTTP/2 client for Android and Java applications.

官方网站：https://github.com/square/okhttp

源码版本：3.9.1

在正式分析源码之前，我们先来看个简单的小例子，从例子入手，逐步分析Okhttp的实现。

👉 举例

```java
OkHttpClient okHttpClient = new OkHttpClient.Builder()
        .build();
Request request = new Request.Builder()
        .url(url)
        .build();
okHttpClient.newCall(request).enqueue(new Callback() {
    @Override
    public void onFailure(Call call, IOException e) {
    }

    @Override
    public void onResponse(Call call, Response response) throws IOException {

    }
});
```

在上面的例子中，我们构建了一个客户端OkHttpClient和一个请求Request，然后调用newCall()方法将请求发送了出去。从这个小例子中，我们可以发现 OkHttpClient相当于是个上下文或者说是大管家，它接到我们给的任务以后，将具体的工作分发到各个子系统中去完成。

**Okhttp的子系统层级结构图如下所示：**

![img](https://user-gold-cdn.xitu.io/2018/1/30/16146b3c10774857?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 网络配置层：利用Builder模式配置各种参数，例如：超时时间、拦截器等，这些参数都会由Okhttp分发给各个需要的子系统。
- 重定向层：负责重定向。
- Header拼接层：负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。
- HTTP缓存层：负责读取缓存以及更新缓存。
- 连接层：连接层是一个比较复杂的层级，它实现了网络协议、内部的拦截器、安全性认证，连接与连接池等功能，但这一层还没有发起真正的连接，它只是做了连接器一些参数的处理。
- 数据响应层：负责从服务器读取响应的数据。

在整个Okhttp的系统中，我们还要理解以下几个关键角色：

- OkHttpClient：通信的客户端，用来统一管理发起请求与解析响应。
- Call：Call是一个接口，它是HTTP请求的抽象描述，具体实现类是RealCall，它由CallFactory创建。
- Request：请求，封装请求的具体信息，例如：url、header等。
- RequestBody：请求体，用来提交流、表单等请求信息。
- Response：HTTP请求的响应，获取响应信息，例如：响应header等。
- ResponseBody：HTTP请求的响应体，被读取一次以后就会关闭，所以我们重复调用responseBody.string()获取请求结果是会报错的。
- Interceptor：Interceptor是请求拦截器，负责拦截并处理请求，它将网络请求、缓存、透明压缩等功能都统一起来，每个功能都是一个Interceptor，所有的Interceptor最 终连接成一个Interceptor.Chain。典型的责任链模式实现。
- StreamAllocation：用来控制Connections与Streas的资源分配与释放。
- RouteSelector：选择路线与自动重连。
- RouteDatabase：记录连接失败的Route黑名单。

我们首先来分析连接的请求与响应流程，这样我们就可以对整个Okhttp系统有一个整体的认识。

##### [2] 请求与响应流程

Okhttp的整个请求与响应的流程就是Dispatcher不断从Request Queue里取出请求（Call），根据是否已经存存缓存，从内存缓存或者服务器获取请求的数据，请求分为**同步**和**异步**两种，同步请求通过 调用Call.exectute()方法直接返回当前请求的Response，异步请求调用Call.enqueue()方法将请求（AsyncCall）添加到请求队列中去，并通过回调（Callback）获取服务器返回的结果。

一图胜千言，我们来看一下整个的流程图，如下所示：

![img](https://user-gold-cdn.xitu.io/2018/1/30/16146b3c0a2ee472?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

读者仔细看一下这个流程图，是不是很像计算机网络的OSI七层模型，Okhttp正式采用这种思路，利用拦截器Interceptor将整套框架纵向分层，简化了设计逻辑，提升了框架扩展性。

通过上面的流程图，我们可以知道在整个请求与响应流程中，以下几点是我们需要重点关注的：

- Dispatcher是如何进行请求调度的？
- 各个拦截器是如何实现的？
- 连接与连接池是如何建立和维护的？

带着以上问题，我们去源码中一探究竟。

我们先来看一下具体的函数调用链，请求与响应的序列图如下所示：

👉 点击图片查看大图

![img](https://user-gold-cdn.xitu.io/2018/1/30/16146b3c0e9f8411?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

上述序列图可以帮助我们理解整个请求与响应流程的具体细节，我们首先来看一下一个请求和如何被封装并发出的。

###### 2.1 请求的封装

请求是由Okhttp发出，真正的请求都被封装了在了接口Call的实现类RealCall中，如下所示：

Call接口如下所示：

```java
public interface Call extends Cloneable {
    
  //返回当前请求
  Request request();

  //同步请求方法，此方法会阻塞当前线程知道请求结果放回
  Response execute() throws IOException;

  //异步请求方法，此方法会将请求添加到队列中，然后等待请求返回
  void enqueue(Callback responseCallback);

  //取消请求
  void cancel();

  //请求是否在执行，当execute()或者enqueue(Callback responseCallback)执行后该方法返回true
  boolean isExecuted();

  //请求是否被取消
  boolean isCanceled();

  //创建一个新的一模一样的请求
  Call clone();

  interface Factory {
    Call newCall(Request request);
  }
}
复制代码
```

RealCall的构造方法如下所示：

```java
final class RealCall implements Call {
    
  private RealCall(OkHttpClient client, Request originalRequest, boolean forWebSocket) {
    //我们构建的OkHttpClient，用来传递参数
    this.client = client;
    this.originalRequest = originalRequest;
    //是不是WebSocket请求，WebSocket是用来建立长连接的，后面我们会说。
    this.forWebSocket = forWebSocket;
    //构建RetryAndFollowUpInterceptor拦截器
    this.retryAndFollowUpInterceptor = new RetryAndFollowUpInterceptor(client, forWebSocket);
  }
}
复制代码
```

RealCall实现了Call接口，它封装了请求的调用，这个构造函数的逻辑也很简单：赋值外部传入的OkHttpClient、Request与forWebSocket，并 创建了重试与重定向拦截器RetryAndFollowUpInterceptor。

###### 2.2 请求的发送

RealCall将请求分为两种：

- 同步请求
- 异步请求

异步请求只是比同步请求多了个Callback，分别调用的方法如下所示：

```java
final class RealCall implements Call {
    
      @Override public void enqueue(Callback responseCallback) {
        synchronized (this) {
          if (executed) throw new IllegalStateException("Already Executed");
          executed = true;
        }
        captureCallStackTrace();
        client.dispatcher().enqueue(new AsyncCall(responseCallback));
     }
}
```

```java
final class RealCall implements Call {
    @Override public Response execute() throws IOException {
      synchronized (this) {
        if (executed) throw new IllegalStateException("Already Executed");
        executed = true;
      }
      captureCallStackTrace();
      try {
        client.dispatcher().executed(this);
        Response result = getResponseWithInterceptorChain();
        if (result == null) throw new IOException("Canceled");
        return result;
      } finally {
        client.dispatcher().finished(this);
      }
    }
}
```

从上面实现可以看出，不管是同步请求还是异步请求都是**Dispatcher(调度)**在处理：

- 同步请求：直接执行，并返回请求结果
- 异步请求：构造一个AsyncCall，并将自己加入处理队列中。

AsyncCall本质上是一个Runable，Dispatcher会调度ExecutorService来执行这些Runable。

```java
final class AsyncCall extends NamedRunnable {
    private final Callback responseCallback;

    AsyncCall(Callback responseCallback) {
      super("OkHttp %s", redactedUrl());
      this.responseCallback = responseCallback;
    }

    String host() {
      return originalRequest.url().host();
    }

    Request request() {
      return originalRequest;
    }

    RealCall get() {
      return RealCall.this;
    }

    @Override protected void execute() {
      boolean signalledCallback = false;
      try {
        Response response = getResponseWithInterceptorChain();
        if (retryAndFollowUpInterceptor.isCanceled()) {
          signalledCallback = true;
          responseCallback.onFailure(RealCall.this, new IOException("Canceled"));
        } else {
          signalledCallback = true;
          responseCallback.onResponse(RealCall.this, response);
        }
      } catch (IOException e) {
        if (signalledCallback) {
          // Do not signal the callback twice!
          Platform.get().log(INFO, "Callback failure for " + toLoggableString(), e);
        } else {
          responseCallback.onFailure(RealCall.this, e);
        }
      } finally {
        client.dispatcher().finished(this);
      }
    }
  }

```

从上面代码可以看出，不管是同步请求还是异步请求最后都会通过getResponseWithInterceptorChain()获取Response，只不过异步请求多了个线程调度，异步 执行的过程。

我们先来来看看Dispatcher里的实现。

###### 2.3 请求的调度

```java
public final class Dispatcher {
    
      private int maxRequests = 64;
      private int maxRequestsPerHost = 5;
    
      /** Ready async calls in the order they'll be run. */
      private final Deque<AsyncCall> readyAsyncCalls = new ArrayDeque<>();
    
      /** Running asynchronous calls. Includes canceled calls that haven't finished yet. */
      private final Deque<AsyncCall> runningAsyncCalls = new ArrayDeque<>();
    
      /** Running synchronous calls. Includes canceled calls that haven't finished yet. */
      private final Deque<RealCall> runningSyncCalls = new ArrayDeque<>();
      
      /** Used by {@code Call#execute} to signal it is in-flight. */
      synchronized void executed(RealCall call) {
        runningSyncCalls.add(call);
      }

      synchronized void enqueue(AsyncCall call) {
      //正在运行的异步请求不得超过64，同一个host下的异步请求不得超过5个
      if (runningAsyncCalls.size() < maxRequests && runningCallsForHost(call) < maxRequestsPerHost) {
        runningAsyncCalls.add(call);
        executorService().execute(call);
      } else {
        readyAsyncCalls.add(call);
      }
    }
}
```

Dispatcher是一个任务调度器，它内部维护了三个双端队列：

- readyAsyncCalls：准备运行的异步请求
- runningAsyncCalls：正在运行的异步请求
- runningSyncCalls：正在运行的同步请求

记得异步请求与同步骑牛，并利用ExecutorService来调度执行AsyncCall。

同步请求就直接把请求添加到正在运行的同步请求队列runningSyncCalls中，异步请求会做个判断：

如果正在运行的异步请求不超过64，而且同一个host下的异步请求不得超过5个则将请求添加到正在运行的同步请求队列中runningAsyncCalls并开始 执行请求，否则就添加到readyAsyncCalls继续等待。

讲完Dispatcher里的实现，我们继续来看getResponseWithInterceptorChain()的实现，这个方法才是真正发起请求并处理请求的地方。

###### 2.4 请求的处理

```java
final class RealCall implements Call {
      Response getResponseWithInterceptorChain() throws IOException {
        // Build a full stack of interceptors.
        List<Interceptor> interceptors = new ArrayList<>();
        //这里可以看出，我们自定义的Interceptor会被优先执行
        interceptors.addAll(client.interceptors());
        //添加重试和重定向烂机器
        interceptors.add(retryAndFollowUpInterceptor);
        interceptors.add(new BridgeInterceptor(client.cookieJar()));
        interceptors.add(new CacheInterceptor(client.internalCache()));
        interceptors.add(new ConnectInterceptor(client));
        if (!forWebSocket) {
          interceptors.addAll(client.networkInterceptors());
        }
        interceptors.add(new CallServerInterceptor(forWebSocket));
    
        Interceptor.Chain chain = new RealInterceptorChain(
            interceptors, null, null, null, 0, originalRequest);
        return chain.proceed(originalRequest);
      }
}
```

短短几行代码，完成了对请求的所有处理过程，Interceptor将网络请求、缓存、透明压缩等功能统一了起来，它的实现采用责任链模式，各司其职， 每个功能都是一个Interceptor，上一级处理完成以后传递给下一级，它们最后连接成了一个Interceptor.Chain。它们的功能如下：

- RetryAndFollowUpInterceptor：负责重定向。
- BridgeInterceptor：负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。
- CacheInterceptor：负责读取缓存以及更新缓存。
- ConnectInterceptor：负责与服务器建立连接。
- CallServerInterceptor：负责从服务器读取响应的数据。

位置决定功能，位置靠前的先执行，最后一个则复制与服务器通讯，请求从RetryAndFollowUpInterceptor开始层层传递到CallServerInterceptor，每一层 都对请求做相应的处理，处理的结构再从CallServerInterceptor层层返回给RetryAndFollowUpInterceptor，最红请求的发起者获得了服务器返回的结果。

以上便是Okhttp整个请求与响应的具体流程，可以发现拦截器才是Okhttp核心功能所在，我们来逐一分析每个拦截器的实现。

##### [3] 拦截器

从上面的流程可以看出，各个环节都是由相应的拦截器进行处理，所有的拦截器（包括我们自定义的）都实现了Interceptor接口，如下所示：

```java
public interface Interceptor {
  Response intercept(Chain chain) throws IOException;

  interface Chain {
    Request request();

    Response proceed(Request request) throws IOException;
    
    //返回Request执行后返回的连接
    @Nullable Connection connection();
  }
}

复制代码
```

Okhttp内置的拦截器如下所示：

- RetryAndFollowUpInterceptor：负责失败重试以及重定向。
- BridgeInterceptor：负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。
- CacheInterceptor：负责读取缓存以及更新缓存。
- ConnectInterceptor：负责与服务器建立连接。
- CallServerInterceptor：负责从服务器读取响应的数据。

我们继续来看看RealInterceptorChain里是怎么一级级处理的。

```
public final class RealInterceptorChain implements Interceptor.Chain {
    
     public Response proceed(Request request, StreamAllocation streamAllocation, HttpCodec httpCodec,
          RealConnection connection) throws IOException {
        if (index >= interceptors.size()) throw new AssertionError();
    
        calls++;
    
        // If we already have a stream, confirm that the incoming request will use it.
        if (this.httpCodec != null && !this.connection.supportsUrl(request.url())) {
          throw new IllegalStateException("network interceptor " + interceptors.get(index - 1)
              + " must retain the same host and port");
        }
    
        // If we already have a stream, confirm that this is the only call to chain.proceed().
        if (this.httpCodec != null && calls > 1) {
          throw new IllegalStateException("network interceptor " + interceptors.get(index - 1)
              + " must call proceed() exactly once");
        }
    
        // Call the next interceptor in the chain.
        RealInterceptorChain next = new RealInterceptorChain(
            interceptors, streamAllocation, httpCodec, connection, index + 1, request);
        Interceptor interceptor = interceptors.get(index);
        Response response = interceptor.intercept(next);
    
        // Confirm that the next interceptor made its required call to chain.proceed().
        if (httpCodec != null && index + 1 < interceptors.size() && next.calls != 1) {
          throw new IllegalStateException("network interceptor " + interceptor
              + " must call proceed() exactly once");
        }
    
        // Confirm that the intercepted response isn't null.
        if (response == null) {
          throw new NullPointerException("interceptor " + interceptor + " returned null");
        }
    
        return response;
      }
}
复制代码
```

这个方法比较有意思，在调用proceed方法之后，会继续构建一个新的RealInterceptorChain对象，调用下一个interceptor来继续请求，直到所有interceptor都处理完毕，将 得到的response返回。

每个拦截器的方法都遵循这样的规则：

```
@Override public Response intercept(Chain chain) throws IOException {
    Request request = chain.request();
    //1 Request阶段，该拦截器在Request阶段负责做的事情

    //2 调用RealInterceptorChain.proceed()，其实是在递归调用下一个拦截器的intercept()方法
    response = ((RealInterceptorChain) chain).proceed(request, streamAllocation, null, null);

    //3 Response阶段，完成了该拦截器在Response阶段负责做的事情，然后返回到上一层的拦截器。
    return response;     
    }
  }
复制代码
```

从上面的描述可知，Request是按照interpretor的顺序正向处理，而Response是逆向处理的。这参考了OSI七层模型的原理。上面我们也提到过。CallServerInterceptor相当于最底层的物理层， 请求从上到逐层包装下发，响应从下到上再逐层包装返回。很漂亮的设计。

interceptor的执行顺序：RetryAndFollowUpInterceptor -> BridgeInterceptor -> CacheInterceptor -> ConnectInterceptor -> CallServerInterceptor。

###### 3.1 RetryAndFollowUpInterceptor

RetryAndFollowUpInterceptor负责失败重试以及重定向。

```
public final class RetryAndFollowUpInterceptor implements Interceptor {
    
    private static final int MAX_FOLLOW_UPS = 20;
    
     @Override public Response intercept(Chain chain) throws IOException {
        Request request = chain.request();
    
        //1. 构建一个StreamAllocation对象，StreamAllocation相当于是个管理类，维护了
        //Connections、Streams和Calls之间的管理，该类初始化一个Socket连接对象，获取输入/输出流对象。
        streamAllocation = new StreamAllocation(
            client.connectionPool(), createAddress(request.url()), callStackTrace);
    
        //重定向次数
        int followUpCount = 0;
        Response priorResponse = null;
        while (true) {
          if (canceled) {
            streamAllocation.release();
            throw new IOException("Canceled");
          }
    
          Response response = null;
          boolean releaseConnection = true;
          try {
            //2. 继续执行下一个Interceptor，即BridgeInterceptor
            response = ((RealInterceptorChain) chain).proceed(request, streamAllocation, null, null);
            releaseConnection = false;
          } catch (RouteException e) {
            //3. 抛出异常，则检测连接是否还可以继续。
            if (!recover(e.getLastConnectException(), false, request)) {
              throw e.getLastConnectException();
            }
            releaseConnection = false;
            continue;
          } catch (IOException e) {
            // 和服务端建立连接失败
            boolean requestSendStarted = !(e instanceof ConnectionShutdownException);
            if (!recover(e, requestSendStarted, request)) throw e;
            releaseConnection = false;
            continue;
          } finally {
            //检测到其他未知异常，则释放连接和资源
            if (releaseConnection) {
              streamAllocation.streamFailed(null);
              streamAllocation.release();
            }
          }
    
          //构建响应体，这个响应体的body为空。
          if (priorResponse != null) {
            response = response.newBuilder()
                .priorResponse(priorResponse.newBuilder()
                        .body(null)
                        .build())
                .build();
          }
    
          //4。根据响应码处理请求，返回Request不为空时则进行重定向处理。
          Request followUp = followUpRequest(response);
    
          if (followUp == null) {
            if (!forWebSocket) {
              streamAllocation.release();
            }
            return response;
          }
    
          closeQuietly(response.body());
    
          //重定向的次数不能超过20次
          if (++followUpCount > MAX_FOLLOW_UPS) {
            streamAllocation.release();
            throw new ProtocolException("Too many follow-up requests: " + followUpCount);
          }
    
          if (followUp.body() instanceof UnrepeatableRequestBody) {
            streamAllocation.release();
            throw new HttpRetryException("Cannot retry streamed HTTP body", response.code());
          }
    
          if (!sameConnection(response, followUp.url())) {
            streamAllocation.release();
            streamAllocation = new StreamAllocation(
                client.connectionPool(), createAddress(followUp.url()), callStackTrace);
          } else if (streamAllocation.codec() != null) {
            throw new IllegalStateException("Closing the body of " + response
                + " didn't close its backing stream. Bad interceptor?");
          }
    
          request = followUp;
          priorResponse = response;
        }
      }
      
    
 
}
复制代码
```

我们先来说说StreamAllocation这个类的作用，这个类协调了三个实体类的关系：

- Connections：连接到远程服务器的物理套接字，这个套接字连接可能比较慢，所以它有一套取消机制。
- Streams：定义了逻辑上的HTTP请求/响应对，每个连接都定义了它们可以携带的最大并发流，HTTP/1.x每次只可以携带一个，HTTP/2每次可以携带多个。
- Calls：定义了流的逻辑序列，这个序列通常是一个初始请求以及它的重定向请求，对于同一个连接，我们通常将所有流都放在一个调用中，以此来统一它们的行为。

我们再来看看整个方法的流程：

1. 构建一个StreamAllocation对象，StreamAllocation相当于是个管理类，维护了Connections、Streams和Calls之间的管理，该类初始化一个Socket连接对象，获取输入/输出流对象。
2. 继续执行下一个Interceptor，即BridgeInterceptor
3. 抛出异常，则检测连接是否还可以继续，以下情况不会重试：

- 客户端配置出错不再重试
- 出错后，request body不能再次发送
- 发生以下Exception也无法恢复连接：
  - ProtocolException：协议异常
  - InterruptedIOException：中断异常
  - SSLHandshakeException：SSL握手异常
  - SSLPeerUnverifiedException：SSL握手未授权异常
- 没有更多线路可以选择 4。根据响应码处理请求，返回Request不为空时则进行重定向处理，重定向的次数不能超过20次。

最后是根据响应码来处理请求头，由followUpRequest()方法完成，具体如下所示：

```
public final class RetryAndFollowUpInterceptor implements Interceptor {
      private Request followUpRequest(Response userResponse) throws IOException {
        if (userResponse == null) throw new IllegalStateException();
        Connection connection = streamAllocation.connection();
        Route route = connection != null
            ? connection.route()
            : null;
        int responseCode = userResponse.code();
    
        final String method = userResponse.request().method();
        switch (responseCode) {
          //407，代理认证
          case HTTP_PROXY_AUTH:
            Proxy selectedProxy = route != null
                ? route.proxy()
                : client.proxy();
            if (selectedProxy.type() != Proxy.Type.HTTP) {
              throw new ProtocolException("Received HTTP_PROXY_AUTH (407) code while not using proxy");
            }
            return client.proxyAuthenticator().authenticate(route, userResponse);
          //401，未经认证
          case HTTP_UNAUTHORIZED:
            return client.authenticator().authenticate(route, userResponse);
          //307，308
          case HTTP_PERM_REDIRECT:
          case HTTP_TEMP_REDIRECT:
            // "If the 307 or 308 status code is received in response to a request other than GET
            // or HEAD, the user agent MUST NOT automatically redirect the request"
            if (!method.equals("GET") && !method.equals("HEAD")) {
              return null;
            }
            // fall-through
          //300，301，302，303
          case HTTP_MULT_CHOICE:
          case HTTP_MOVED_PERM:
          case HTTP_MOVED_TEMP:
          case HTTP_SEE_OTHER:
              
            //客户端在配置中是否允许重定向
            if (!client.followRedirects()) return null;
    
            String location = userResponse.header("Location");
            if (location == null) return null;
            HttpUrl url = userResponse.request().url().resolve(location);
    
            // url为null，不允许重定向
            if (url == null) return null;
    
            //查询是否存在http与https之间的重定向
            boolean sameScheme = url.scheme().equals(userResponse.request().url().scheme());
            if (!sameScheme && !client.followSslRedirects()) return null;
    
            // Most redirects don't include a request body.
            Request.Builder requestBuilder = userResponse.request().newBuilder();
            if (HttpMethod.permitsRequestBody(method)) {
              final boolean maintainBody = HttpMethod.redirectsWithBody(method);
              if (HttpMethod.redirectsToGet(method)) {
                requestBuilder.method("GET", null);
              } else {
                RequestBody requestBody = maintainBody ? userResponse.request().body() : null;
                requestBuilder.method(method, requestBody);
              }
              if (!maintainBody) {
                requestBuilder.removeHeader("Transfer-Encoding");
                requestBuilder.removeHeader("Content-Length");
                requestBuilder.removeHeader("Content-Type");
              }
            }
    
            // When redirecting across hosts, drop all authentication headers. This
            // is potentially annoying to the application layer since they have no
            // way to retain them.
            if (!sameConnection(userResponse, url)) {
              requestBuilder.removeHeader("Authorization");
            }
    
            return requestBuilder.url(url).build();
          //408，超时
          case HTTP_CLIENT_TIMEOUT:
            // 408's are rare in practice, but some servers like HAProxy use this response code. The
            // spec says that we may repeat the request without modifications. Modern browsers also
            // repeat the request (even non-idempotent ones.)
            if (userResponse.request().body() instanceof UnrepeatableRequestBody) {
              return null;
            }
    
            return userResponse.request();
    
          default:
            return null;
        }
      }    
}
复制代码
```

重定向会涉及到一些网络编程的知识，这里如果没有完成理解，你只要知道RetryAndFollowUpInterceptor的作用就是处理了一些连接异常以及重定向就可以了。我们接着来看看下一个BridgeInterceptor。

###### 3.2 BridgeInterceptor

BridgeInterceptor就跟它的名字那样，它是一个连接桥，它负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。 转换的过程就是添加一些服务端需要的header信息。

```
public final class BridgeInterceptor implements Interceptor {
    @Override public Response intercept(Chain chain) throws IOException {
        Request userRequest = chain.request();
        Request.Builder requestBuilder = userRequest.newBuilder();
    
        RequestBody body = userRequest.body();
        if (body != null) {
          //1 进行Header的包装
          MediaType contentType = body.contentType();
          if (contentType != null) {
            requestBuilder.header("Content-Type", contentType.toString());
          }
    
          long contentLength = body.contentLength();
          if (contentLength != -1) {
            requestBuilder.header("Content-Length", Long.toString(contentLength));
            requestBuilder.removeHeader("Transfer-Encoding");
          } else {
            requestBuilder.header("Transfer-Encoding", "chunked");
            requestBuilder.removeHeader("Content-Length");
          }
        }
    
        if (userRequest.header("Host") == null) {
          requestBuilder.header("Host", hostHeader(userRequest.url(), false));
        }
    
        if (userRequest.header("Connection") == null) {
          requestBuilder.header("Connection", "Keep-Alive");
        }
    
        //这里有个坑：如果你在请求的时候主动添加了"Accept-Encoding: gzip" ，transparentGzip=false，那你就要自己解压，如果
        // 你没有吹解压，或导致response.string()乱码。
        // If we add an "Accept-Encoding: gzip" header field we're responsible for also decompressing
        // the transfer stream.
        boolean transparentGzip = false;
        if (userRequest.header("Accept-Encoding") == null && userRequest.header("Range") == null) {
          transparentGzip = true;
          requestBuilder.header("Accept-Encoding", "gzip");
        }
    
        //创建OkhttpClient配置的cookieJar
        List<Cookie> cookies = cookieJar.loadForRequest(userRequest.url());
        if (!cookies.isEmpty()) {
          requestBuilder.header("Cookie", cookieHeader(cookies));
        }
    
        if (userRequest.header("User-Agent") == null) {
          requestBuilder.header("User-Agent", Version.userAgent());
        }
    
        Response networkResponse = chain.proceed(requestBuilder.build());
    
        //解析服务器返回的Header，如果没有这事cookie，则不进行解析
        HttpHeaders.receiveHeaders(cookieJar, userRequest.url(), networkResponse.headers());
    
        Response.Builder responseBuilder = networkResponse.newBuilder()
            .request(userRequest);
    
        //判断服务器是否支持gzip压缩，如果支持，则将压缩提交给Okio库来处理
        if (transparentGzip
            && "gzip".equalsIgnoreCase(networkResponse.header("Content-Encoding"))
            && HttpHeaders.hasBody(networkResponse)) {
          GzipSource responseBody = new GzipSource(networkResponse.body().source());
          Headers strippedHeaders = networkResponse.headers().newBuilder()
              .removeAll("Content-Encoding")
              .removeAll("Content-Length")
              .build();
          responseBuilder.headers(strippedHeaders);
          responseBuilder.body(new RealResponseBody(strippedHeaders, Okio.buffer(responseBody)));
        }
    
        return responseBuilder.build();
      }
}
复制代码
```

就跟它的名字描述的那样，它是一个桥梁，负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。 在Request阶段配置用户信息，并添加一些请求头。在Response阶段，进行gzip解压。

这个方法主要是针对Header做了一些处理，这里主要提一下"Accept-Encoding", "gzip"，关于它有以下几点需要注意：

- 开发者没有添加Accept-Encoding时，自动添加Accept-Encoding: gzip
- 自动添加Accept-Encoding，会对request，response进行自动解压
- 手动添加Accept-Encoding，不负责解压缩
- 自动解压时移除Content-Length，所以上层Java代码想要contentLength时为-1
- 自动解压时移除 Content-Encoding
- 自动解压时，如果是分块传输编码，Transfer-Encoding: chunked不受影响。

BridgeInterceptor主要就是针对Header做了一些处理，我们接着来看CacheInterceptor。

###### 3.3 CacheInterceptor

我们知道为了节省流量和提高响应速度，Okhttp是有自己的一套缓存机制的，CacheInterceptor就是用来负责读取缓存以及更新缓存的。

```
public final class CacheInterceptor implements Interceptor {
    
     @Override public Response intercept(Chain chain) throws IOException {
         
        //1. 读取候选缓存，具体如何读取的我们下面会讲。
        Response cacheCandidate = cache != null
            ? cache.get(chain.request())
            : null;
    
        long now = System.currentTimeMillis();
    
        //2. 创建缓存策略，强制缓存、对比缓存等，关于缓存策略我们下面也会讲。
        CacheStrategy strategy = new CacheStrategy.Factory(now, chain.request(), cacheCandidate).get();
        Request networkRequest = strategy.networkRequest;
        Response cacheResponse = strategy.cacheResponse;
    
        if (cache != null) {
          cache.trackResponse(strategy);
        }
    
        if (cacheCandidate != null && cacheResponse == null) {
          closeQuietly(cacheCandidate.body());
        }
    
        //3. 根据策略，不使用网络，又没有缓存的直接报错，并返回错误码504。
        if (networkRequest == null && cacheResponse == null) {
          return new Response.Builder()
              .request(chain.request())
              .protocol(Protocol.HTTP_1_1)
              .code(504)
              .message("Unsatisfiable Request (only-if-cached)")
              .body(Util.EMPTY_RESPONSE)
              .sentRequestAtMillis(-1L)
              .receivedResponseAtMillis(System.currentTimeMillis())
              .build();
        }
    
        //4. 根据策略，不使用网络，有缓存的直接返回。
        if (networkRequest == null) {
          return cacheResponse.newBuilder()
              .cacheResponse(stripBody(cacheResponse))
              .build();
        }
    
        Response networkResponse = null;
        try {
          //5. 前面两个都没有返回，继续执行下一个Interceptor，即ConnectInterceptor。
          networkResponse = chain.proceed(networkRequest);
        } finally {
          //如果发生IO异常，则释放掉缓存
          if (networkResponse == null && cacheCandidate != null) {
            closeQuietly(cacheCandidate.body());
          }
        }
    
        //6. 接收到网络结果，如果响应code式304，则使用缓存，返回缓存结果。
        if (cacheResponse != null) {
          if (networkResponse.code() == HTTP_NOT_MODIFIED) {
            Response response = cacheResponse.newBuilder()
                .headers(combine(cacheResponse.headers(), networkResponse.headers()))
                .sentRequestAtMillis(networkResponse.sentRequestAtMillis())
                .receivedResponseAtMillis(networkResponse.receivedResponseAtMillis())
                .cacheResponse(stripBody(cacheResponse))
                .networkResponse(stripBody(networkResponse))
                .build();
            networkResponse.body().close();
    
            cache.trackConditionalCacheHit();
            cache.update(cacheResponse, response);
            return response;
          } else {
            closeQuietly(cacheResponse.body());
          }
        }
    
        //7. 读取网络结果。
        Response response = networkResponse.newBuilder()
            .cacheResponse(stripBody(cacheResponse))
            .networkResponse(stripBody(networkResponse))
            .build();
    
        //8. 对数据进行缓存。
        if (cache != null) {
          if (HttpHeaders.hasBody(response) && CacheStrategy.isCacheable(response, networkRequest)) {
            // Offer this request to the cache.
            CacheRequest cacheRequest = cache.put(response);
            return cacheWritingResponse(cacheRequest, response);
          }
    
          if (HttpMethod.invalidatesCache(networkRequest.method())) {
            try {
              cache.remove(networkRequest);
            } catch (IOException ignored) {
              // The cache cannot be written.
            }
          }
        }
    
        //9. 返回网络读取的结果。
        return response;
      }
}
复制代码
```

整个方法的流程如下所示：

1. 读取候选缓存，具体如何读取的我们下面会讲。
2. 创建缓存策略，强制缓存、对比缓存等，关于缓存策略我们下面也会讲。
3. 根据策略，不使用网络，又没有缓存的直接报错，并返回错误码504。
4. 根据策略，不使用网络，有缓存的直接返回。
5. 前面两个都没有返回，继续执行下一个Interceptor，即ConnectInterceptor。
6. 接收到网络结果，如果响应code式304，则使用缓存，返回缓存结果。
7. 读取网络结果。
8. 对数据进行缓存。
9. 返回网络读取的结果。

我们再接着来看ConnectInterceptor。

###### 3.4 ConnectInterceptor

在RetryAndFollowUpInterceptor里初始化了一个StreamAllocation对象，我们说在这个StreamAllocation对象里初始化了一个Socket对象用来做连接，但是并没有 真正的连接，等到处理完hader和缓存信息之后，才调用ConnectInterceptor来进行真正的连接

```java
public final class ConnectInterceptor implements Interceptor {
    
      @Override public Response intercept(Chain chain) throws IOException {
        RealInterceptorChain realChain = (RealInterceptorChain) chain;
        Request request = realChain.request();
        StreamAllocation streamAllocation = realChain.streamAllocation();
    
        boolean doExtensiveHealthChecks = !request.method().equals("GET");
        //创建输出流
        HttpCodec httpCodec = streamAllocation.newStream(client, doExtensiveHealthChecks);
        //建立连接
        RealConnection connection = streamAllocation.connection();
    
        return realChain.proceed(request, streamAllocation, httpCodec, connection);
      }
}
```

ConnectInterceptor在Request阶段建立连接，处理方式也很简单，创建了两个对象：

- HttpCodec：用来编码HTTP requests和解码HTTP responses
- RealConnection：连接对象，负责发起与服务器的连接。

这里事实上包含了连接、连接池等一整套的Okhttp的连接机制，我们放在下面单独讲，先来继续看最后一个Interceptor：CallServerInterceptor。

###### 3.5 CallServerInterceptor

CallServerInterceptor负责从服务器读取响应的数据。

```
public final class CallServerInterceptor implements Interceptor {
    
    @Override public Response intercept(Chain chain) throws IOException {
        
        //这些对象在前面的Interceptor都已经创建完毕
        RealInterceptorChain realChain = (RealInterceptorChain) chain;
        HttpCodec httpCodec = realChain.httpStream();
        StreamAllocation streamAllocation = realChain.streamAllocation();
        RealConnection connection = (RealConnection) realChain.connection();
        Request request = realChain.request();
    
        long sentRequestMillis = System.currentTimeMillis();
        //1. 写入请求头 
        httpCodec.writeRequestHeaders(request);
    
        Response.Builder responseBuilder = null;
        if (HttpMethod.permitsRequestBody(request.method()) && request.body() != null) {
          // If there's a "Expect: 100-continue" header on the request, wait for a "HTTP/1.1 100
          // Continue" response before transmitting the request body. If we don't get that, return what
          // we did get (such as a 4xx response) without ever transmitting the request body.
          if ("100-continue".equalsIgnoreCase(request.header("Expect"))) {
            httpCodec.flushRequest();
            responseBuilder = httpCodec.readResponseHeaders(true);
          }
    
          //2 写入请求体
          if (responseBuilder == null) {
            // Write the request body if the "Expect: 100-continue" expectation was met.
            Sink requestBodyOut = httpCodec.createRequestBody(request, request.body().contentLength());
            BufferedSink bufferedRequestBody = Okio.buffer(requestBodyOut);
            request.body().writeTo(bufferedRequestBody);
            bufferedRequestBody.close();
          } else if (!connection.isMultiplexed()) {
            // If the "Expect: 100-continue" expectation wasn't met, prevent the HTTP/1 connection from
            // being reused. Otherwise we're still obligated to transmit the request body to leave the
            // connection in a consistent state.
            streamAllocation.noNewStreams();
          }
        }
    
        httpCodec.finishRequest();
    
        //3 读取响应头
        if (responseBuilder == null) {
          responseBuilder = httpCodec.readResponseHeaders(false);
        }
    
        Response response = responseBuilder
            .request(request)
            .handshake(streamAllocation.connection().handshake())
            .sentRequestAtMillis(sentRequestMillis)
            .receivedResponseAtMillis(System.currentTimeMillis())
            .build();
    
        //4 读取响应体
        int code = response.code();
        if (forWebSocket && code == 101) {
          // Connection is upgrading, but we need to ensure interceptors see a non-null response body.
          response = response.newBuilder()
              .body(Util.EMPTY_RESPONSE)
              .build();
        } else {
          response = response.newBuilder()
              .body(httpCodec.openResponseBody(response))
              .build();
        }
    
        if ("close".equalsIgnoreCase(response.request().header("Connection"))
            || "close".equalsIgnoreCase(response.header("Connection"))) {
          streamAllocation.noNewStreams();
        }
    
        if ((code == 204 || code == 205) && response.body().contentLength() > 0) {
          throw new ProtocolException(
              "HTTP " + code + " had non-zero Content-Length: " + response.body().contentLength());
        }
    
        return response;
      }
}
复制代码
```

我们通过ConnectInterceptor已经连接到服务器了，接下来我们就是写入请求数据以及读出返回数据了。整个流程：

1. 写入请求头
2. 写入请求体
3. 读取响应头
4. 读取响应体

这篇文章就到这里，后续的文章我们会来分析Okhttp的缓存机制、连接机制、编辑吗机制等实现。

##### [4] 连接机制

连接的创建是在StreamAllocation对象统筹下完成的，我们前面也说过它早在RetryAndFollowUpInterceptor就被创建了，StreamAllocation对象 主要用来管理两个关键角色：

- RealConnection：真正建立连接的对象，利用Socket建立连接。
- ConnectionPool：连接池，用来管理和复用连接。

在里初始化了一个StreamAllocation对象，我们说在这个StreamAllocation对象里初始化了一个Socket对象用来做连接，但是并没有

###### 4.1 创建连接

我们在前面的ConnectInterceptor分析中已经说过，onnectInterceptor用来完成连接。而真正的连接在RealConnect中实现，连接由连接池ConnectPool来管理，连接池最多保 持5个地址的连接keep-alive，每个keep-alive时长为5分钟，并有异步线程清理无效的连接。

主要由以下两个方法完成：

1. HttpCodec httpCodec = streamAllocation.newStream(client, doExtensiveHealthChecks);
2. RealConnection connection = streamAllocation.connection();

我们来具体的看一看。

StreamAllocation.newStream()最终调动findConnect()方法来建立连接。

```java
public final class StreamAllocation {
    
      /**
       * Returns a connection to host a new stream. This prefers the existing connection if it exists,
       * then the pool, finally building a new connection.
       */
      private RealConnection findConnection(int connectTimeout, int readTimeout, int writeTimeout,
          boolean connectionRetryEnabled) throws IOException {
        Route selectedRoute;
        synchronized (connectionPool) {
          if (released) throw new IllegalStateException("released");
          if (codec != null) throw new IllegalStateException("codec != null");
          if (canceled) throw new IOException("Canceled");
    
          //1 查看是否有完好的连接
          RealConnection allocatedConnection = this.connection;
          if (allocatedConnection != null && !allocatedConnection.noNewStreams) {
            return allocatedConnection;
          }
    
          //2 连接池中是否用可用的连接，有则使用
          Internal.instance.get(connectionPool, address, this, null);
          if (connection != null) {
            return connection;
          }
    
          selectedRoute = route;
        }
    
        //线程的选择，多IP操作
        if (selectedRoute == null) {
          selectedRoute = routeSelector.next();
        }
    
        //3 如果没有可用连接，则自己创建一个
        RealConnection result;
        synchronized (connectionPool) {
          if (canceled) throw new IOException("Canceled");
    
          // Now that we have an IP address, make another attempt at getting a connection from the pool.
          // This could match due to connection coalescing.
          Internal.instance.get(connectionPool, address, this, selectedRoute);
          if (connection != null) {
            route = selectedRoute;
            return connection;
          }
    
          // Create a connection and assign it to this allocation immediately. This makes it possible
          // for an asynchronous cancel() to interrupt the handshake we're about to do.
          route = selectedRoute;
          refusedStreamCount = 0;
          result = new RealConnection(connectionPool, selectedRoute);
          acquire(result);
        }
    
        //4 开始TCP以及TLS握手操作
        result.connect(connectTimeout, readTimeout, writeTimeout, connectionRetryEnabled);
        routeDatabase().connected(result.route());
    
        //5 将新创建的连接，放在连接池中
        Socket socket = null;
        synchronized (connectionPool) {
          // Pool the connection.
          Internal.instance.put(connectionPool, result);
    
          // If another multiplexed connection to the same address was created concurrently, then
          // release this connection and acquire that one.
          if (result.isMultiplexed()) {
            socket = Internal.instance.deduplicate(connectionPool, address, this);
            result = connection;
          }
        }
        closeQuietly(socket);
    
        return result;
      }    
}
复制代码
```

整个流程如下：

1. 查找是否有完整的连接可用：

- Socket没有关闭
- 输入流没有关闭
- 输出流没有关闭
- Http2连接没有关闭

1. 连接池中是否有可用的连接，如果有则可用。
2. 如果没有可用连接，则自己创建一个。
3. 开始TCP连接以及TLS握手操作。
4. 将新创建的连接加入连接池。

上述方法完成后会创建一个RealConnection对象，然后调用该方法的connect()方法建立连接，我们再来看看RealConnection.connect()方法的实现。

```java
public final class RealConnection extends Http2Connection.Listener implements Connection {
    
    public void connect(
         int connectTimeout, int readTimeout, int writeTimeout, boolean connectionRetryEnabled) {
       if (protocol != null) throw new IllegalStateException("already connected");
   
       //线路选择
       RouteException routeException = null;
       List<ConnectionSpec> connectionSpecs = route.address().connectionSpecs();
       ConnectionSpecSelector connectionSpecSelector = new ConnectionSpecSelector(connectionSpecs);
   
       if (route.address().sslSocketFactory() == null) {
         if (!connectionSpecs.contains(ConnectionSpec.CLEARTEXT)) {
           throw new RouteException(new UnknownServiceException(
               "CLEARTEXT communication not enabled for client"));
         }
         String host = route.address().url().host();
         if (!Platform.get().isCleartextTrafficPermitted(host)) {
           throw new RouteException(new UnknownServiceException(
               "CLEARTEXT communication to " + host + " not permitted by network security policy"));
         }
       }
       
       //开始连接
       while (true) {
         try {
            //如果是通道模式，则建立通道连接
           if (route.requiresTunnel()) {
             connectTunnel(connectTimeout, readTimeout, writeTimeout);
           } 
           //否则进行Socket连接，一般都是属于这种情况
           else {
             connectSocket(connectTimeout, readTimeout);
           }
           //建立https连接
           establishProtocol(connectionSpecSelector);
           break;
         } catch (IOException e) {
           closeQuietly(socket);
           closeQuietly(rawSocket);
           socket = null;
           rawSocket = null;
           source = null;
           sink = null;
           handshake = null;
           protocol = null;
           http2Connection = null;
   
           if (routeException == null) {
             routeException = new RouteException(e);
           } else {
             routeException.addConnectException(e);
           }
   
           if (!connectionRetryEnabled || !connectionSpecSelector.connectionFailed(e)) {
             throw routeException;
           }
         }
       }
   
       if (http2Connection != null) {
         synchronized (connectionPool) {
           allocationLimit = http2Connection.maxConcurrentStreams();
         }
       }
     }

    /** Does all the work necessary to build a full HTTP or HTTPS connection on a raw socket. */
      private void connectSocket(int connectTimeout, int readTimeout) throws IOException {
        Proxy proxy = route.proxy();
        Address address = route.address();
    
        //根据代理类型的不同处理Socket
        rawSocket = proxy.type() == Proxy.Type.DIRECT || proxy.type() == Proxy.Type.HTTP
            ? address.socketFactory().createSocket()
            : new Socket(proxy);
    
        rawSocket.setSoTimeout(readTimeout);
        try {
          //建立Socket连接
          Platform.get().connectSocket(rawSocket, route.socketAddress(), connectTimeout);
        } catch (ConnectException e) {
          ConnectException ce = new ConnectException("Failed to connect to " + route.socketAddress());
          ce.initCause(e);
          throw ce;
        }
    
        // The following try/catch block is a pseudo hacky way to get around a crash on Android 7.0
        // More details:
        // https://github.com/square/okhttp/issues/3245
        // https://android-review.googlesource.com/#/c/271775/
        try {
          //获取输入/输出流
          source = Okio.buffer(Okio.source(rawSocket));
          sink = Okio.buffer(Okio.sink(rawSocket));
        } catch (NullPointerException npe) {
          if (NPE_THROW_WITH_NULL.equals(npe.getMessage())) {
            throw new IOException(npe);
          }
        }
      }
}
复制代码
```

最终调用Java里的套接字Socket里的connect()方法。

###### 4.2 连接池

**我们知道在负责的网络环境下，频繁的进行建立Sokcet连接（TCP三次握手）和断开Socket（TCP四次分手）是非常消耗网络资源和浪费时间的，HTTP中的keepalive连接对于 降低延迟和提升速度有非常重要的作用。**

复用连接就需要对连接进行管理，这里就引入了连接池的概念。

Okhttp支持5个并发KeepAlive，默认链路生命为5分钟(链路空闲后，保持存活的时间)，连接池有ConectionPool实现，对连接进行回收和管理。

ConectionPool在内部维护了一个线程池，来清理连接，如下所示：

```java
public final class ConnectionPool {
    
        private static final Executor executor = new ThreadPoolExecutor(0 /* corePoolSize */,
          Integer.MAX_VALUE /* maximumPoolSize */, 60L /* keepAliveTime */, TimeUnit.SECONDS,
          new SynchronousQueue<Runnable>(), Util.threadFactory("OkHttp ConnectionPool", true));
      
        //清理连接，在线程池executor里调用。
        private final Runnable cleanupRunnable = new Runnable() {
          @Override public void run() {
            while (true) {
              //执行清理，并返回下次需要清理的时间。
              long waitNanos = cleanup(System.nanoTime());
              if (waitNanos == -1) return;
              if (waitNanos > 0) {
                long waitMillis = waitNanos / 1000000L;
                waitNanos -= (waitMillis * 1000000L);
                synchronized (ConnectionPool.this) {
                  try {
                    //在timeout时间内释放锁
                    ConnectionPool.this.wait(waitMillis, (int) waitNanos);
                  } catch (InterruptedException ignored) {
                  }
                }
              }
            }
          }
        };
}
复制代码
```

ConectionPool在内部维护了一个线程池，来清理连，清理任务由cleanup()方法完成，它是一个阻塞操作，首先执行清理，并返回下次需要清理的间隔时间，调用调用wait() 方法释放锁。等时间到了以后，再次进行清理，并返回下一次需要清理的时间，循环往复。

我们来看一看cleanup()方法的具体实现。

```java
public final class ConnectionPool {
    
      long cleanup(long now) {
        int inUseConnectionCount = 0;
        int idleConnectionCount = 0;
        RealConnection longestIdleConnection = null;
        long longestIdleDurationNs = Long.MIN_VALUE;
    
     
        synchronized (this) {
            //遍历所有的连接，标记处不活跃的连接。
          for (Iterator<RealConnection> i = connections.iterator(); i.hasNext(); ) {
            RealConnection connection = i.next();
    
            //1. 查询此连接内部的StreanAllocation的引用数量。
            if (pruneAndGetAllocationCount(connection, now) > 0) {
              inUseConnectionCount++;
              continue;
            }
    
            idleConnectionCount++;
    
            //2. 标记空闲连接。
            long idleDurationNs = now - connection.idleAtNanos;
            if (idleDurationNs > longestIdleDurationNs) {
              longestIdleDurationNs = idleDurationNs;
              longestIdleConnection = connection;
            }
          }
    
          if (longestIdleDurationNs >= this.keepAliveDurationNs
              || idleConnectionCount > this.maxIdleConnections) {
            //3. 如果空闲连接超过5个或者keepalive时间大于5分钟，则将该连接清理掉。
            connections.remove(longestIdleConnection);
          } else if (idleConnectionCount > 0) {
            //4. 返回此连接的到期时间，供下次进行清理。
            return keepAliveDurationNs - longestIdleDurationNs;
          } else if (inUseConnectionCount > 0) {
            //5. 全部都是活跃连接，5分钟时候再进行清理。
            return keepAliveDurationNs;
          } else {
            //6. 没有任何连接，跳出循环。
            cleanupRunning = false;
            return -1;
          }
        }
    
        //7. 关闭连接，返回时间0，立即再次进行清理。
        closeQuietly(longestIdleConnection.socket());
        return 0;
      }
}
复制代码
```

整个方法的流程如下所示：

1. 查询此连接内部的StreanAllocation的引用数量。
2. 标记空闲连接。
3. 如果空闲连接超过5个或者keepalive时间大于5分钟，则将该连接清理掉。
4. 返回此连接的到期时间，供下次进行清理。
5. 全部都是活跃连接，5分钟时候再进行清理。
6. 没有任何连接，跳出循环。
7. 关闭连接，返回时间0，立即再次进行清理。

在RealConnection里有个StreamAllocation虚引用列表，每创建一个StreamAllocation，就会把它添加进该列表中，如果留关闭以后就将StreamAllocation 对象从该列表中移除，正是利用利用这种引用计数的方式判定一个连接是否为空闲连接，

```
public final List<Reference<StreamAllocation>> allocations = new ArrayList<>();
复制代码
```

查找引用计数由pruneAndGetAllocationCount()方法实现，具体实现如下所示：

```java
public final class ConnectionPool {
    
     private int pruneAndGetAllocationCount(RealConnection connection, long now) {
       //虚引用列表
       List<Reference<StreamAllocation>> references = connection.allocations;
       //遍历虚引用列表
       for (int i = 0; i < references.size(); ) {
         Reference<StreamAllocation> reference = references.get(i);
         //如果虚引用StreamAllocation正在被使用，则跳过进行下一次循环，
         if (reference.get() != null) {
           //引用计数
           i++;
           continue;
         }
   
         // We've discovered a leaked allocation. This is an application bug.
         StreamAllocation.StreamAllocationReference streamAllocRef =
             (StreamAllocation.StreamAllocationReference) reference;
         String message = "A connection to " + connection.route().address().url()
             + " was leaked. Did you forget to close a response body?";
         Platform.get().logCloseableLeak(message, streamAllocRef.callStackTrace);
   
         //否则移除该StreamAllocation引用
         references.remove(i);
         connection.noNewStreams = true;
   
         // 如果所有的StreamAllocation引用都没有了，返回引用计数0
         if (references.isEmpty()) {
           connection.idleAtNanos = now - keepAliveDurationNs;
           return 0;
         }
       }
       
       //返回引用列表的大小，作为引用计数
       return references.size();
     } 
}
复制代码
```

##### [5] 缓存机制

###### 5.1 缓存策略

在分析Okhttp的缓存机制之前，我们先来回顾一下HTTP与缓存相关的理论知识，这是实现Okhttp机制的基础。

HTTP的缓存机制也是依赖于请求和响应header里的参数类实现的，最终响应式从缓存中去，还是从服务端重新拉取，HTTP的缓存机制的流程如下所示：

HTTP的缓存可以分为两种：

- **强制缓存**：需要服务端参与判断是否继续使用缓存，当客户端第一次请求数据是，服务端返回了缓存的过期时间（Expires与Cache-Control），没有过期就可以继续使用缓存，否则则不适用，无需再向服务端询问。
- **对比缓存**：需要服务端参与判断是否继续使用缓存，当客户端第一次请求数据时，服务端会将缓存标识（Last-Modified/If-Modified-Since与Etag/If-None-Match）与数据一起返回给客户端，客户端将两者都备份到缓存中 ，再次请求数据时，客户端将上次备份的缓存 标识发送给服务端，服务端根据缓存标识进行判断，如果返回304，则表示通知客户端可以继续使用缓存。

**强制缓存优先于对比缓存**。

上面提到强制缓存使用的的两个标识：

- Expires：Expires的值为服务端返回的到期时间，即下一次请求时，请求时间小于服务端返回的到期时间，直接使用缓存数据。到期时间是服务端生成的，客户端和服务端的时间可能有误差。
- Cache-Control：Expires有个时间校验的问题，所有HTTP1.1采用Cache-Control替代Expires。

Cache-Control的取值有以下几种：

- private:             客户端可以缓存。
- public:              客户端和代理服务器都可缓存。
- max-age=xxx:   缓存的内容将在 xxx 秒后失效
- no-cache:          需要使用对比缓存来验证缓存数据。
- no-store:           所有内容都不会缓存，强制缓存，对比缓存都不会触发。

我们再来看看对比缓存的两个标识：

**Last-Modified/If-Modified-Since**

Last-Modified 表示资源上次修改的时间。

当客户端发送第一次请求时，服务端返回资源上次修改的时间：

```
Last-Modified: Tue, 12 Jan 2016 09:31:27 GMT
复制代码
```

客户端再次发送，会在header里携带If-Modified-Since。将上次服务端返回的资源时间上传给服务端。

```
If-Modified-Since: Tue, 12 Jan 2016 09:31:27 GMT 
复制代码
```

服务端接收到客户端发来的资源修改时间，与自己当前的资源修改时间进行对比，如果自己的资源修改时间大于客户端发来的资源修改时间，则说明资源做过修改， 则返回200表示需要重新请求资源，否则返回304表示资源没有被修改，可以继续使用缓存。

上面是一种时间戳标记资源是否修改的方法，还有一种资源标识码ETag的方式来标记是否修改，如果标识码发生改变，则说明资源已经被修改，ETag优先级高于Last-Modified。

**Etag/If-None-Match**

ETag是资源文件的一种标识码，当客户端发送第一次请求时，服务端会返回当前资源的标识码：

```
ETag: "5694c7ef-24dc"
复制代码
```

客户端再次发送，会在header里携带上次服务端返回的资源标识码：

```
If-None-Match:"5694c7ef-24dc"
复制代码
```

服务端接收到客户端发来的资源标识码，则会与自己当前的资源吗进行比较，如果不同，则说明资源已经被修改，则返回200，如果相同则说明资源没有被修改，返回 304，客户端可以继续使用缓存。

以上便是HTTP缓存策略的相关理论知识，我们来看看具体实现。

Okhttp的缓存策略就是根据上述流程图实现的，具体的实现类是CacheStrategy，CacheStrategy的构造函数里有两个参数：

```
CacheStrategy(Request networkRequest, Response cacheResponse) {
this.networkRequest = networkRequest;
this.cacheResponse = cacheResponse;
}
复制代码
```

这两个参数参数的含义如下：

- networkRequest：网络请求。
- cacheResponse：缓存响应，基于DiskLruCache实现的文件缓存，可以是请求中url的md5，value是文件中查询到的缓存，这个我们下面会说。

CacheStrategy就是利用这两个参数生成最终的策略，有点像map操作，将networkRequest与cacheResponse这两个值输入，处理之后再将这两个值输出，们的组合结果如下所示：

- 如果networkRequest为null，cacheResponse为null：only-if-cached(表明不进行网络请求，且缓存不存在或者过期，一定会返回503错误)。
- 如果networkRequest为null，cacheResponse为non-null：不进行网络请求，而且缓存可以使用，直接返回缓存，不用请求网络。
- 如果networkRequest为non-null，cacheResponse为null：需要进行网络请求，而且缓存不存在或者过期，直接访问网络。
- 如果networkRequest为non-null，cacheResponse为non-null：Header中含有ETag/Last-Modified标签，需要在条件请求下使用，还是需要访问网络。

那么这四种情况是如何判定的，我们来看一下。

CacheStrategy是利用Factory模式进行构造的，CacheStrategy.Factory对象构建以后，调用它的get()方法即可获得具体的CacheStrategy，CacheStrategy.Factory.get()方法内部 调用的是CacheStrategy.Factory.getCandidate()方法，它是核心的实现。

如下所示：

```java
public static class Factory {
    
        private CacheStrategy getCandidate() {
          //1. 如果缓存没有命中，就直接进行网络请求。
          if (cacheResponse == null) {
            return new CacheStrategy(request, null);
          }
    
          //2. 如果TLS握手信息丢失，则返回直接进行连接。
          if (request.isHttps() && cacheResponse.handshake() == null) {
            return new CacheStrategy(request, null);
          }

          //3. 根据response状态码，Expired时间和是否有no-cache标签就行判断是否进行直接访问。
          if (!isCacheable(cacheResponse, request)) {
            return new CacheStrategy(request, null);
          }
    
          //4. 如果请求header里有"no-cache"或者右条件GET请求（header里带有ETag/Since标签），则直接连接。
          CacheControl requestCaching = request.cacheControl();
          if (requestCaching.noCache() || hasConditions(request)) {
            return new CacheStrategy(request, null);
          }
    
          CacheControl responseCaching = cacheResponse.cacheControl();
          if (responseCaching.immutable()) {
            return new CacheStrategy(null, cacheResponse);
          }
    
          //计算当前age的时间戳：now - sent + age
          long ageMillis = cacheResponseAge();
          //刷新时间，一般服务器设置为max-age
          long freshMillis = computeFreshnessLifetime();
    
          if (requestCaching.maxAgeSeconds() != -1) {
            //一般取max-age
            freshMillis = Math.min(freshMillis, SECONDS.toMillis(requestCaching.maxAgeSeconds()));
          }
    
          long minFreshMillis = 0;
          if (requestCaching.minFreshSeconds() != -1) {
            //一般取0
            minFreshMillis = SECONDS.toMillis(requestCaching.minFreshSeconds());
          }
    
          long maxStaleMillis = 0;
          if (!responseCaching.mustRevalidate() && requestCaching.maxStaleSeconds() != -1) {
            maxStaleMillis = SECONDS.toMillis(requestCaching.maxStaleSeconds());
          }
    
          //5. 如果缓存在过期时间内则可以直接使用，则直接返回上次缓存。
          if (!responseCaching.noCache() && ageMillis + minFreshMillis < freshMillis + maxStaleMillis) {
            Response.Builder builder = cacheResponse.newBuilder();
            if (ageMillis + minFreshMillis >= freshMillis) {
              builder.addHeader("Warning", "110 HttpURLConnection \"Response is stale\"");
            }
            long oneDayMillis = 24 * 60 * 60 * 1000L;
            if (ageMillis > oneDayMillis && isFreshnessLifetimeHeuristic()) {
              builder.addHeader("Warning", "113 HttpURLConnection \"Heuristic expiration\"");
            }
            return new CacheStrategy(null, builder.build());
          }
    
          //6. 如果缓存过期，且有ETag等信息，则发送If-None-Match、If-Modified-Since、If-Modified-Since等条件请求
          //交给服务端判断处理
          String conditionName;
          String conditionValue;
          if (etag != null) {
            conditionName = "If-None-Match";
            conditionValue = etag;
          } else if (lastModified != null) {
            conditionName = "If-Modified-Since";
            conditionValue = lastModifiedString;
          } else if (servedDate != null) {
            conditionName = "If-Modified-Since";
            conditionValue = servedDateString;
          } else {
            return new CacheStrategy(request, null); // No condition! Make a regular request.
          }
    
          Headers.Builder conditionalRequestHeaders = request.headers().newBuilder();
          Internal.instance.addLenient(conditionalRequestHeaders, conditionName, conditionValue);
    
          Request conditionalRequest = request.newBuilder()
              .headers(conditionalRequestHeaders.build())
              .build();
          return new CacheStrategy(conditionalRequest, cacheResponse);
        }
}
复制代码
```

整个函数的逻辑就是按照上面那个HTTP缓存判定流程图来实现，具体流程如下所示：

1. 如果缓存没有命中，就直接进行网络请求。
2. 如果TLS握手信息丢失，则返回直接进行连接。
3. 根据response状态码，Expired时间和是否有no-cache标签就行判断是否进行直接访问。
4. 如果请求header里有"no-cache"或者右条件GET请求（header里带有ETag/Since标签），则直接连接。
5. 如果缓存在过期时间内则可以直接使用，则直接返回上次缓存。
6. 如果缓存过期，且有ETag等信息，则发送If-None-Match、If-Modified-Since、If-Modified-Since等条件请求交给服务端判断处理

整个流程就是这样，另外说一点，Okhttp的缓存是根据服务器header自动的完成的，整个流程也是根据RFC文档写死的，客户端不必要进行手动控制。

理解了缓存策略，我们来看看缓存在磁盘上是如何被管理的。

###### 5.2 缓存管理

这篇文章我们来分析Okhttp的缓存机制，缓存机制是基于DiskLruCache做的。Cache类封装了缓存的实现，实现了InternalCache接口。

InternalCache接口如下所示：

**InternalCache**

```java
public interface InternalCache {
  //获取缓存
  Response get(Request request) throws IOException;
  //存入缓存
  CacheRequest put(Response response) throws IOException;
  //移除缓存
  void remove(Request request) throws IOException;
  //更新缓存
  void update(Response cached, Response network);
  //跟踪一个满足缓存条件的GET请求
  void trackConditionalCacheHit();
  //跟踪满足缓存策略CacheStrategy的响应
  void trackResponse(CacheStrategy cacheStrategy);
}
复制代码
```

我们接着来看看它的实现类。

Cache没有直接实现InternalCache这个接口，而是在其内部实现了InternalCache的匿名内部类，内部类的方法调用Cache对应的方法，如下所示：

```java
final InternalCache internalCache = new InternalCache() {
@Override public Response get(Request request) throws IOException {
  return Cache.this.get(request);
}

@Override public CacheRequest put(Response response) throws IOException {
  return Cache.this.put(response);
}

@Override public void remove(Request request) throws IOException {
  Cache.this.remove(request);
}

@Override public void update(Response cached, Response network) {
  Cache.this.update(cached, network);
}

@Override public void trackConditionalCacheHit() {
  Cache.this.trackConditionalCacheHit();
}

@Override public void trackResponse(CacheStrategy cacheStrategy) {
  Cache.this.trackResponse(cacheStrategy);
}
};

InternalCache internalCache() {
return cache != null ? cache.internalCache : internalCache;
}
复制代码
```

` 在Cache类里还定义一些内部类，这些类封装了请求与响应信息。

- Cache.Entry：封装了请求与响应等信息，包括url、varyHeaders、protocol、code、message、responseHeaders、handshake、sentRequestMillis与receivedResponseMillis。
- Cache.CacheResponseBody：继承于ResponseBody，封装了缓存快照snapshot，响应体bodySource，内容类型contentType，内容长度contentLength。

除了两个类以外，Okhttp还封装了一个文件系统类FileSystem类，这个类利用Okio这个库对Java的FIle操作进行了一层封装，简化了IO操作。理解了这些剩下的就是DiskLruCahe里的插入缓存 、获取缓存和删除缓存的操作。

关于这一部分的内容，可以参考我们之前写的内容[07Android开源框架源码分析：LruCache与DiskLruCache](https://github.com/guoxiaoxing/android-open-framwork-analysis/blob/master/doc/源码分析/07Android开源框架源码分析：LruCache与DiskLruCache.md) 。

好了，到这里关于Okhttp的全部内容就都讲完了，可以说Okhttp是设计非常优良的一个库，有很多值得我们学习的地方，下一篇我们来分析它的好搭档Retrofit。

#### 12.View和ViewGroup的区别

View和ViewGroup的区别：

​     可以从两方面来说：

​     一. 事件分发方面的区别；

​     二. UI绘制方面的区别；

##### [1] 事件分发方面的区别

​     事件分发机制主要有三个方法：**dispatchTouchEvent()**、**onInterceptTouchEvent()**、onTouchEvent()

​     1. ViewGroup包含这三个方法，而View则只包含dispatchTouchEvent()、onTouchEvent()两个方法，不包含onInterceptTouchEvent()。

​     2. 触摸事件由Action_Down、Action_Move、Action_Up组成，一次完整的触摸事件，包含一个Down和Up，以及若干个Move（可以为0）；

     3. 在Action_Down的情况下，事件会先传递到最顶层的ViewGroup，调用ViewGroup的dispatchTouchEvent()，①如果ViewGroup的onInterceptTouchEvent()返回false不拦截该事件，则会分发给子View，调用子View的dispatchTouchEvent()，如果子View的dispatchTouchEvent()返回true，则调用View的onTouchEvent()消费事件。②如果ViewGroup的onInterceptTouchEvent()返回true拦截该事件，则调用ViewGroup的onTouchEvent()消费事件，接下来的Move和Up事件将由该ViewGroup直接进行处理。

​     4. 当某个子View的dispatchTouchEvent()返回true时，会中止Down事件的分发，同时在ViewGroup中记录该子View。接下来的Move和Up事件将由该子View直接进行处理。

​     5. 当ViewGroup中所有子View都不捕获Down事件时，将触发ViewGroup自身的onTouch();触发的方式是调用super.dispatchTouchEvent函数，即父类View的dispatchTouchEvent方法。在所有子View都不处理的情况下，触发Acitivity的onTouchEvent方法。

​     6. 由于子View是保存在ViewGroup中的，多层ViewGroup的节点结构时，上层ViewGroup保存的会是真实处理事件的View所在的ViewGroup对象。如ViewGroup0——ViewGroup1——TextView的结构中，TextView返回了true，它将被保存在ViewGroup1中，而ViewGroup1也会返回true，将被保存在ViewGroup0中；当Move和Up事件来时，会先从ViewGroup0传递到ViewGroup1，再由ViewGroup1传递到TextView，最后事件由TextView消费掉。

​     7.子View可以调getParent().requestDisallowInterceptTouchEvent(),请求父ViewGroup不拦截事件。

##### [2] UI绘制方面的区别

​     UI绘制主要有五个方法：onDraw(),onLayout(),onMeasure()，dispatchDraw(),drawChild()

​     1.ViewGroup包含这五个方法，而View只包含onDraw(),onLayout(),onMeasure()三个方法，不包含dispatchDraw(),drawChild()。

​     2.绘制流程：onMeasure（测量）——》onLayout（布局）——》onDraw（绘制）。

​     3.绘制按照视图树的顺序执行，视图绘制时会先绘制子控件。如果视图的背景可见，视图会在调用onDraw()之前调用drawBackGround()绘制背景。强制重绘，可以使用invalidate();

​     4.如果发生视图的尺寸变化，则该视图会调用requestLayou()，向父控件请求再次布局。如果发生视图的外观变化，则该视图会调用invalidate()，强制重绘。如果requestLayout()或invalidate()有一个被调用，框架会对视图树进行相关的测量、布局和绘制。

​     注意：视图树是单线程操作，直接调用其它视图的方法必须要在UI线程里。跨线程的操作必须使用Handler。

​     5.onLayout()：对于View来说，onLayout()只是一个空实现；而对于ViewGroup来说，onLayout()使用了关键字abstract的修饰，要求其子类必须重载该方法，目的就是安排其children在父视图的具体位置。

​     6.draw过程：drawBackground()绘制背景——》onDraw()对View的内容进行绘制——》dispatchDraw()对当前View的所有子View进行绘制——》onDrawScrollBars()对View的滚动条进行绘制。

![img](https://img-blog.csdn.net/20180907173011161?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxOTQxMjYzMDEz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 

方法说明：

​     1.onDraw(Canvas canvas)：UI绘制最重要的方法，用于UI重绘。这个方法是所有View、ViewGroup及其派生类都具有的方法。自定义控件时，可以重载该方法，并在内容基于canvas绘制自定义的图形、图像效果。

​     2.onLayout(boolean changed, int left, int top, int right, int bottom)：布局发生变化时调用此方法。这个方法是所有View、ViewGroup及其派生类都具有的方法。自定义控件时，可以重载该方法，在布局发生改变时实现特效等定制处理。

​     3.onMeasure(int widthMeasureSpec, int heightMeasureSpec)：用于计算自己及所有子对象的大小。这个方法是所有View、ViewGroup及其派生类都具有的方法。自定义控件时，可以重载该方法，重新计算所有对象的大小。 MeasureSpec包含了测量的模式和测量的大小，通过MeasureSpec.getMode()获取测量模式，通过MeasureSpec.getSize()获取测量大小。mode共有三种情况： 分别为MeasureSpec.UNSPECIFIED（ View想多大就多大）, MeasureSpec.EXACTLY（默认模式，精确值模式：将layout_width或layout_height属性指定为具体数值或者match_parent。）, MeasureSpec.AT_MOST（ 最大值模式：将layout_width或layout_height指定为wrap_content。）。

​     4.dispatchDraw(Canvas canvas)：ViewGroup及其派生类具有的方法，主要用于控制子View的绘制分发。自定义控件时，重载该方法可以改变子View的绘制，进而实现一些复杂的视效。

​     5.drawChild(Canvas canvas, View child, long drawingTime)：ViewGroup及其派生类具有的方法，用于直接绘制具体的子View。自定义控件时，重载该方法可以直接绘制具体的子View。

#### 13. Application的生命周期

1. **onCreate（）** 程序创建的时候执行；
2. **onTerminate（）** 程序终止的时候执行；在模拟环境下执行。当终止应用程序对象时调用，不保证一定被调用，当程序是被内核终止以便为其他应用程序释放资源，那么将不会提醒，并且不调用应用程序Application对象的onTerminate方法而直接终止进程。
3. **onLowMemory（）** 低内存的时候执行好的应用程序一般会在这个方法里面释放一些不必要的资源来应付当后台程序已经终止，前台应用程序内存还不够时的情况。
4. **onConfigurationChanged（Configuration newConfig）** 配置改变时触发这个方法。
5. **onTrimMemory（int level）**程序在进行内存清理时执行

~~~java
class MyApplication : Application(){
 
    //应用创建时调用
    override fun onCreate() {
        super.onCreate()
    }
 
    //在低内存时被调用
    override fun onLowMemory() {
        super.onLowMemory()
    }
 
    //程序终止的时候被调用，该函数不一定会执行，
    //或者说不会在真机环境下被执行，通过该方法的注释，我们可以得知
    //该方法只有在模拟器环境下才会被执行
    override fun onTerminate() {
        super.onTerminate()
    }
 
    //程序在内存清理的时候被执行
    override fun onTrimMemory(level: Int) {
        super.onTrimMemory(level)
    }
 
    //系统设置被修改时调用
    override fun onConfigurationChanged(newConfig: Configuration) {
        super.onConfigurationChanged(newConfig)
    }
~~~

#### 14. Android多线程方式

##### [1] 前言

在Android开发中经常会使用到多线程，这里主要是总结Android开发中常见的多线程实现方式，以及这些多线程实现方式的一些特点 
多线程实现方式主要有：

- 实现Thread的run()方法或者实现Runable接口
- HandlerThread
- AsyncTask
- LoaderManager

##### [2] Thread方式

一般使用异步操作最常见的一种方式，我们可以继承Thread，并重写run(）方法，如下所示：

```java
Thread syncTask = new Thread() {
    @Override
    public void run() {
        // 执行耗时操作
    }
};

syncTask.start();12345678
```

还有另外一种启动线程的方式，即在创建Thread对象时，传入一个实现了Runable接口的对象，如下所示：

```java
Thread syncTask = new Thread(new Runnable() {
    @Override
    public void run() {
        // 执行耗时操作
    }
});

syncTask.start();12345678
```

Thread类中有几个方法的作用有些模糊，这里给出说明：

- interrupt( )：

  我们一般会使用该方法中断线程的执行，但该方法并不会中断线程，它的作用只是设置一个中断标志位，我们还得在run( )方法中判断这个标志位，并决定是否继续执行，通过这样的方式来达到中断的效果。 但该方法根据线程状态的不同，会有不同的结果。结果如下：

  1. 当线程由于调用wait( )、join( )、sleep( )而阻塞时，中断标志位将会被清空，并接收到InterruptedException异常。
  2. 当线程由于正在进行InterruptibleChannel类型的I/O操作而阻塞时，中断标志位将会置位，并接收到ClosedByInterruptException异常（I/O流也会自动关闭）
  3. 当线程由于进行Selector操作而阻塞时，中断标志位将会置位，但不会接收到异常

interrupted( )和isInterrupted( )的区别： 
两个方法都是判断当前线程的中断标志位是否被置位，但调用interrupted( )方法后，中断标志位将会重置，而isInterrupted(）不会被重置。

- join( )和sleep( )的区别：两个方法都会让线程暂停执行

join(）方法是让出执行资源（如：CPU时间片），使得其它线程可以获得执行的资源。所以调用join()方法会使进入阻塞状态，该线程被唤醒后会进入runable状态，等待下一个时间片的到来才能再次执行。 
sleep( )不会让出资源，只是处于睡眠状态（类似只执行空操作）。调用sleep()方法会使进入等待状态，当等待时间到后，如果还在时间片内，则直接进入运行状态，否则进入runable状态，等待下个时间片。

##### [3] HandlerThread

有些需求需要子线程不断的从一个消息队列中取出消息，并进行处理，处理完毕以后继续取出下一个处理。对于这个需求我们可以使用第一种方式，实现一个Thread对象，并创建一个消息队列，在Thread对象的run方法中不断的从消息队列中取出消息进行处理。多以该线程的这些特点有点像一个Looper线程，我们可复用Handler机制提供的消息队列MessageQueue，而无需自己重新创建。 
HandlerThread的内部实现机制很简单，在创建新的线程后，使该线程成为一个Looper线程，让该线程不断的从MessageQueue取出消息并处理。我们看一下HandlerThread的实现：

```java
public class HandlerThread extends Thread {
    int mPriority;
    Looper mLooper;

    /**
    * Constructs a HandlerThread.
    */
    public HandlerThread(String name, int priority) {
        super(name);
        mPriority = priority;
    }

    @Override
    public void run() {
        // 要想让某个线程成为Looper线程，先调用Looper.prepare（）为该线程创建一个Looper对象，并初始化MessageQueue对象
        Looper.prepare();
        synchronized (this) {
            mLooper = Looper.myLooper();
            notifyAll();
        }
        Process.setThreadPriority(mPriority);
        // 调用Looper.loop（），让该线程的Looper实例循环从MessageQueue中取出Message进行处理
        Looper.loop();
    }
}
```

##### [4] Async(A森克)Task

这是我们最经常使用的一种异步方式，在前面的两种多线程方式中，如果在子线程中进行了耗时的处理操作（如：网络请求、读写数据库等），当操作完毕后，我们需要更新UI上的显示状态，但在Android开发中我们是不能在子线程中更新UI界面的，所以还得在子线程中发送一个通知到主线程，让主线程去更新UI。这样的操作流程有些复杂，且都是重复性的工作。所以Android sdk中为我们抽象出AsyncTask这个类。

```java
public class CustomAsyncTask extends AsyncTask<String, Integer, String> {
    @Override
    protected void onPreExecute() {
        // 在开始执行异步操作前回调，该方法在主线程中执行
    }

    @Override
    protected String doInBackground(String... strings) {
        // 在该方法中进行异步操作，参数strings是在启动异步任务时execute(...)传递进来的
        // 该异步任务放回的结果类型为String
        return null;
    }

    @Override
    protected void onProgressUpdate(Integer... values) {
        // 该方法用户通知用户doInBackground()方法的处理进度，在主线程中被回调，所以可在该方法中更新UI
        // 参数values用于指示处理进度
    }

    @Override
    protected void onPostExecute(String result) {
        // 该方法是在异步操作doInBackground()处理完毕后回调，参数result是doInBackground()的处理结果
        // 该方法在主线程中被回调，可直接更新UI
    }

    @Override
    protected void onCancelled(String result) {
        super.onCancelled(result);

        // 当调用cancel(boolean), 则在doInBackground()完成后回调该方法
        // 注意: 参数result可能为null，
    }
}
```

AsyncTask的内部使用了两个线程池，我们大概看一下AsyncTask的内部实现

```java
// 顺序执行任务的线程池，注意这个线程池是静态的，每个AsyncTask对象共用这个线程池
public static final Executor SERIAL_EXECUTOR = new SerialExecutor();
private static volatile Executor sDefaultExecutor = SERIAL_EXECUTOR;

// 我们启动异步任务的三个方法，都是向SerialExecutor.execute（runable）传递一个runable对象
public final AsyncTask<Params, Progress, Result> execute(Params... params) {
    return executeOnExecutor(sDefaultExecutor, params);
}

public final AsyncTask<Params, Progress, Result> executeOnExecutor(Executor exec,
        Params... params) {
    ...
    exec.execute(mFuture);
    ...
    return this;
}

public static void execute(Runnable runnable) {
    sDefaultExecutor.execute(runnable);
}

```

看一下SerialExecutor的实现

```java
private static class SerialExecutor implements Executor {
    // 存储待执行的异步任务
    final ArrayDeque<Runnable> mTasks = new ArrayDeque<Runnable>();
    Runnable mActive;

    public synchronized void execute(final Runnable r) {
        // 其实并没有马上执行，而是添加到队列mTasks中, 进行一个排队
        mTasks.offer(new Runnable() {
            public void run() {
                try {
                    r.run();
                } finally {
                    // 一个任务执行完后，再执行下一个
                    scheduleNext();
                }
            }
        });

        // 当前没有异步任务执行时，启动开始执行
        if (mActive == null) {
            scheduleNext();
        }
    }

    protected synchronized void scheduleNext() {
        if ((mActive = mTasks.poll()) != null) {
            // 使用另外一个线程池分配线程，并执行任务
            THREAD_POOL_EXECUTOR.execute(mActive);
        }
    }
}

```

所以在使用AsyncTask执行异步操作时，会先在SerialExecutor进行一个顺序排队， 后再用ThreadPoolExcutor线程池为你分配一个线程并执行。而整个应用的AsyncTask任务都在排同一条队，有可能等待排队的任务很多，所以一般不会使用AsyncTask执行一些优先级比较高的异步任务。 
当然我们是可以跳过不需要进行排队，直接就通过线程池分配一个线程并执行异步任务，但需要注意同时执行太多的异步任务，会影响用户体验，我想Google就是为了限制同时创建太多的线程才会采用一个排队机制的。

```java
/** @hide */
public static void setDefaultExecutor(Executor exec) {
    sDefaultExecutor = exec;
}
```

该方法是隐藏，但可使用反射，设置一个线程池。

##### [5] Loader&LoaderManager

上面三种异步方式都可以用来加载一些耗时的数据，但有时我们加载数据的过程与Activity、Fragment的生命息息相关的。所以在使用上面说的那几种异步方式进行异步数据加载时，是需要去考虑Activity(Fragment)的生命周期是处于哪个阶段的。于是Android在Android 3.0以后引入了LoaderManager，主要用于执行一些耗时的异步数据加载操作，并根据Activity生命周期对异步处理进行调整，LoaderManager可以解决的问题包括：

1. 加载的数据有变化时，会自动通知我们，而不自己监控数据的变化情况，如：用CursorLoader来加载数据库数据，当数据库数据有变化时，可是个展示变化的数据
2. 数据的请求处理时机会结合Activity和Fragment的生命周期进行调整，如：若Acivity销毁了，那就不会再去请求新的数据

使用该方法加载数据涉及到两个类重要的类，Loader和LoaderManager：

Loader：该类用于数据的加载 ，类型参数D用于指定Loader加载的数据类型

```java
public class Loader<D> {
}
```

一般我们不直接继承Loader，而是继承AsyncTaskLoader，因为Loader的加载工作并不是在异步线程中。而AsyncTaskLoader实现了异步线程，加载流程在子线程中执行。注意：对该类的调用应该在主线程中完成。

LoaderManager: 
LoaderManager用于管理与Activity和Fragment关联的Loader实例，LoaderManager负责根据的Activity的生命周期对Loader的数据加载器进行调度，所以这里分工明确，Loader负责数据加载逻辑，LoaderManager 
负责Loader的调度，开发者只需要自定义自己的Loader，实现数据的加载逻辑，而不再关注数据加载时由于Activity销毁引发的问题。

注意：其实AsyncTaskLoader内部实现异步的方式是使用AsyncTask完成的，上面我们说过AsyncTask的内部是有一个排队机制，但AsyncTaskLoader内部使用AsyncTask进行数据异步加载时，异步任务并不进行排队。而直接又线程池分配新线程来执行。

##### [6] 总结

我们来总结一下异步处理的方式，以及每种处理方式适合什么样的场景

- 直接使用**Thread**实现方式，这种方式简单，但不是很优雅。适合数量很少（偶尔一两次）的异步任务，但要处理的异步任务很多的话，使用该方式会导致创建大量的线程，这会影响用户交互。
- **HandlerThread**，这种方式适合子线程有序的执行异步操作，异步任务的执行一个接着一个。
- **AsyncTask**， 通常用于耗时的异步处理，且时效性要求不是非常高的那种异步操作。如果时效性要求非常高的操作，不建议使用这个方式，**因为AsyncTask的默认实现是有内部排队机制，且是整个应用的AsyncTask的任务进行排队，所以不能保证异步任务能很快的被执行**。
- **LoaderManager**，当请求处理时机需要根据Activity的生命周期进行调整，或需要时刻监测数据的变化，那LoaderManager是很不错的解决方案。

#### 15.图片缓存原理

> 移动开发本质上就是手机和服务器之间进行通信，需要从服务端获取数据。反复通过网络获取数据是比较耗时的，特别是访问比较多的时候，会极大影响了性能，Android中可通过缓存机制来减少频繁的网络操作，减少流量、提升性能。

##### [1] 实现原理

　　把不需要实时更新的数据缓存下来，通过时间或者其他因素　来判别是读缓存还是网络请求，这样可以缓解服务器压力，一定程度上提高应用响应速度，并且支持离线阅读。 　　

##### [2] Bitmap的缓存

　　在许多的情况下(像 ListView, GridView 或 ViewPager 之类的组件 )我们需要一次性加载大量的图片，在屏幕上显示的图片和所有待显示的图片有可能需要马上就在屏幕上无限制的进行滚动、切换。

　　像ListView, GridView 这类组件，它们的子项当不可见时，所占用的内存会被回收以供正在前台显示子项使用。垃圾回收器也会释放你已经加载了的图片占用的内存。如果你想让你的UI运行流畅的话，就不应该每次显示时都去重新加载图片。保持一些内存和文件缓存就变得很有必要了。

##### [3] 使用内存缓存

　　通过预先消耗应用的一点内存来存储数据，便可快速的为应用中的组件提供数据，是一种典型的以**空间换时间**的策略。LruCache  类（Android v4 Support Library 类库中开始提供）非常适合来做图片缓存任务 ，它可以使用一个LinkedHashMap  的强引用来保存最近使用的对象，并且当它保存的对象占用的内存总和超出了为它设计的最大内存时会把**不经常使用(LRU)**的对象成员踢出以供垃圾回收器回收。

> LruCache是Android中的一个缓存工具类，它采用了一种**最近最少使用**算法，可以将一些对象进行内存缓存，当缓存满后，会优先删除**近期最少使用**的对象。

> **LruCache源码解析**：https://www.jianshu.com/p/8b17bf6fc2d5

　　给LruCache 设置一个合适的内存大小，需考虑如下因素：

- 还剩余多少内存给你的activity或应用使用
- 屏幕上需要一次性显示多少张图片和多少图片在等待显示
- 手机的大小和密度是多少（密度越高的设备需要越大的 缓存）
- 图片的尺寸（决定了所占用的内存大小）
- 图片的访问频率（频率高的在内存中一直保存）
- 保存图片的质量（不同像素的在不同情况下显示）

具体的要根据应用图片使用的具体情况来找到一个合适的解决办法，一个设置 LruCache 例子：

```java
private LruCache<String, Bitmap> mMemoryCache;

@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    // 获得虚拟机能提供的最大内存，超过这个大小会抛出OutOfMemory的异常
    final int maxMemory = (int) (Runtime.getRuntime().maxMemory() / 1024);

    // 用１／８的内存大小作为内存缓存
    final int cacheSize = maxMemory / 8;

    mMemoryCache = new LruCache<String, Bitmap>(cacheSize) {
        @Override
        protected int sizeOf(String key, Bitmap bitmap) {
            // 这里返回的不是item的个数，是cache的size（单位1024个字节）
            return bitmap.getByteCount() / 1024;
        }
    };
    ...
}

public void addBitmapToMemoryCache(String key, Bitmap bitmap) {
    if (getBitmapFromMemCache(key) == null) {
        mMemoryCache.put(key, bitmap);
    }
}

public Bitmap getBitmapFromMemCache(String key) {
    return mMemoryCache.get(key);
}
```

　　当为ImageView加载一张图片时，会先在LruCache 中看看有没有缓存这张图片，如果有的话直接更新到ImageView中，如果没有的话，一个后台线程会被触发来加载这张图片。

```java
public void loadBitmap(int resId, ImageView imageView) {
    final String imageKey = String.valueOf(resId);

    // 查看下内存缓存中是否缓存了这张图片
    final Bitmap bitmap = getBitmapFromMemCache(imageKey);
    if (bitmap != null) {
        mImageView.setImageBitmap(bitmap);
    } else {
        mImageView.setImageResource(R.drawable.image_placeholder);
BitmapWorkerTask task = new BitmapWorkerTask(mImageView);
        task.execute(resId);
    }
}
```

在图片加载的Task中，需要把加载好的图片加入到内存缓存中。

```java
class BitmapWorkerTask extends AsyncTask<Integer, Void, Bitmap> {
    ...
    // 在后台完成
    @Override
    protected Bitmap doInBackground(Integer... params) {
        final Bitmap bitmap = decodeSampledBitmapFromResource(
                getResources(), params[0], 100, 100));
    addBitmapToMemoryCache(String.valueOf(params[0]), bitmap);
        return bitmap;
    }
    ...
}
```

##### [4] 使用磁盘缓存

　　内存缓存能够快速的获取到最近显示的图片，但不一定就能够获取到。当数据集过大时很容易把内存缓存填满（如GridView ）。你的应用也有可能被其它的任务（比如来电）中断进入到后台，后台应用有可能会被杀死，那么相应的内存缓存对象也会被销毁。 当你的应用重新回到前台显示时，你的应用又需要一张一张的去加载图片了。

　磁盘文件缓存能够用来处理这些情况，保存处理好的图片，当内存缓存不可用的时候，直接读取在硬盘中保存好的图片，这样可以有效的减少图片加载的次数。读取磁盘文件要比直接从内存缓存中读取要慢一些，而且需要在一个UI主线程外的线程中进行，因为磁盘的读取速度是不能够保证的，磁盘文件缓存显然也是一种以**空间换时间**的策略。

　　如果图片使用非常频繁的话，一个 ContentProvider 可能更适合代替去存储缓存图片，比如图片gallery 应用。

　　下面是一个DiskLruCache的部分代码：

```java
private DiskLruCache mDiskLruCache;
private final Object mDiskCacheLock = new Object();
private boolean mDiskCacheStarting = true;
private static final int DISK_CACHE_SIZE = 1024 * 1024 * 10; // 10MB
private static final String DISK_CACHE_SUBDIR = "thumbnails";

@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    // 初始化内存缓存
    ...
    // 在后台线程中初始化磁盘缓存
    File cacheDir = getDiskCacheDir(this, DISK_CACHE_SUBDIR);
    new InitDiskCacheTask().execute(cacheDir);
    ...
}

class InitDiskCacheTask extends AsyncTask<File, Void, Void> {
    @Override
    protected Void doInBackground(File... params) {
        synchronized (mDiskCacheLock) {
            File cacheDir = params[0];
  mDiskLruCache = DiskLruCache.open(cacheDir, DISK_CACHE_SIZE);
　 mDiskCacheStarting = false; // 结束初始化
　 mDiskCacheLock.notifyAll(); // 唤醒等待线程
        }
        return null;
    }
}

class BitmapWorkerTask extends AsyncTask<Integer, Void, Bitmap> {
    ...
    // 在后台解析图片
    @Override
    protected Bitmap doInBackground(Integer... params) {
        final String imageKey = String.valueOf(params[0]);

        // 在后台线程中检测磁盘缓存
        Bitmap bitmap = getBitmapFromDiskCache(imageKey);

        if (bitmap == null) { // 没有在磁盘缓存中找到图片
 final Bitmap bitmap = decodeSampledBitmapFromResource(
                    getResources(), params[0], 100, 100));
        }

        // 把这个final类型的bitmap加到缓存中
        addBitmapToCache(imageKey, bitmap);

        return bitmap;
    }
    ...
}

public void addBitmapToCache(String key, Bitmap bitmap) {
    // 先加到内存缓存
    if (getBitmapFromMemCache(key) == null) {
        mMemoryCache.put(key, bitmap);
    }

    //再加到磁盘缓存
    synchronized (mDiskCacheLock) {
        if (mDiskLruCache != null && mDiskLruCache.get(key) == null) {
            mDiskLruCache.put(key, bitmap);
        }
    }
}

public Bitmap getBitmapFromDiskCache(String key) {
    synchronized (mDiskCacheLock) {
        // 等待磁盘缓存从后台线程打开
        while (mDiskCacheStarting) {
            try {
                mDiskCacheLock.wait();
            } catch (InterruptedException e) {}
        }
        if (mDiskLruCache != null) {
            return mDiskLruCache.get(key);
        }
    }
    return null;
}

public static File getDiskCacheDir(Context context, String uniqueName) {
    // 优先使用外缓存路径，如果没有挂载外存储，就使用内缓存路径
final String cachePath =
            Environment.MEDIA_MOUNTED.equals(Environment.getExternalStorageState()) ||
!isExternalStorageRemovable() ?getExternalCacheDir(context).getPath():context.getCacheDir().getPath();

    return new File(cachePath + File.separator + uniqueName);
}
```

　　不能在UI主线程中进行这项操作，因为初始化磁盘缓存也需要对磁盘进行操作。上面的程序片段中，一个锁对象确保了磁盘缓存没有初始化完成之前不能够对磁盘缓存进行访问。

　　 内存缓存在UI线程中进行检测，磁盘缓存在UI主线程外的线程中进行检测，当图片处理完成之后，分别存储到内存缓存和磁盘缓存中。

**设备配置参数改变时加载问题**

　　由于应用在运行的时候设备配置参数可能会发生改变，比如设备朝向改变，会导致Android销毁你的Activity然后按照新的配置重启，这种情况下，我们要避免重新去加载处理所有的图片，让用户能有一个流畅的体验。

　使用Fragment 能够把内存缓存对象传递到新的activity实例中，调用setRetainInstance(true)) 方法来保留Fragment实例。当activity重新创建好后， 被保留的Fragment依附于activity而存在，通过Fragment就可以获取到已经存在的内存缓存对象了，这样就可以快速的获取到图片，并设置到ImageView上，给用户一个流畅的体验。

下面是一个示例程序片段：

```java
private LruCache<String, Bitmap> mMemoryCache;

@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
RetainFragment mRetainFragment =            RetainFragment.findOrCreateRetainFragment(getFragmentManager());
    mMemoryCache = RetainFragment.mRetainedCache;
    if (mMemoryCache == null) {
        mMemoryCache = new LruCache<String, Bitmap>(cacheSize) {
            ... //像上面例子中那样初始化缓存
        }
        mRetainFragment.mRetainedCache = mMemoryCache;
    }
    ...
}

class RetainFragment extends Fragment {
    private static final String TAG = "RetainFragment";
    public LruCache<String, Bitmap> mRetainedCache;

    public RetainFragment() {}

    public static RetainFragment findOrCreateRetainFragment(FragmentManager fm) {
        RetainFragment fragment = (RetainFragment) fm.findFragmentByTag(TAG);
        if (fragment == null) {
            fragment = new RetainFragment();
        }
        return fragment;
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 使得Fragment在Activity销毁后还能够保留下来
        setRetainInstance(true);
    }
}
```

　　可以在不适用Fragment（没有界面的服务类Fragment）的情况下旋转设备屏幕。在保留缓存的情况下，你应该能发现填充图片到Activity中几乎是瞬间从内存中取出而没有任何延迟的感觉。任何图片优先从内存缓存获取，没有的话再到硬盘缓存中找，如果都没有，那就以普通方式加载图片。 　　 参考：

[Caching Bitmaps](http://developer.android.com/training/displaying-bitmaps/cache-bitmap.html)

[LruCache](http://developer.android.com/reference/android/util/LruCache.html)

##### [5] 使用SQLite进行缓存

　　网络请求数据完成后，把文件的相关信息（如url（一般作为唯一标示），下载时间，过期时间）等存放到数据库。下次加载的时候根据url先从数据库中查询，如果查询到并且时间未过期，就根据路径读取本地文件，从而实现缓存的效果。

　　注意：缓存的数据库是存放在/data/data//databases/目录下，是占用内存空间的，如果缓存累计，容易浪费内存，需要及时清理缓存。

##### [6] 文件缓存

　　思路和一般缓存一样，把需要的数据存储在文件中，下次加载时判断文件是否存在和过期（使用File.lastModified()方法得到文件的最后修改时间，与当前时间判断），存在并未过期就加载文件中的数据，否则请求服务器重新下载。

　　注意，无网络环境下就默认读取文件缓存中的。

##### [7] LruCache与DiskLruCache的使用

在前面的Bitmap文章中提到，Bitmap在使用中非常容易出现OOM，而本节主要介绍2个方法对加载多图/大图的情况进行优化，有效的避免OOM。

###### 7.1 LruCache缓存

在使用RecyclerView、ListView等加载多图时，屏幕上显示的图片会通过滑动屏幕等事件不断地增加，最终导致OOM。为了保证内存始终维持在一个合理的范围，当item移除屏幕时要对图片进行回收，重新滚入屏幕时又要重新加载；Google官方推荐的是使用LruCache内存缓存技术，完美的解决了上面的问题。

> 内存缓存技术对大量占用程序应用内存的对象提供快速访问的方法。主要算法：把最近使用的对象用强引用存储在LinkedHashMap中，把最近最少使用的对象在缓存值达到限定时进行移除。

在使用LruCache缓存时应该考虑的因素：

1. 设备最大为每个程序分配的内存
2. 图片被访问的频率有多高，如存在个别访问频率高的图片可以考虑使用多个LruCache来区分对象组
3. 图片的尺寸大小，每张图片占用的内存大小
4. 设备的屏幕大小和分辨率
5. 存储多个低像素的图片，而在后台去开线程加载高像素的图片会更加的有效

**使用案例**：
使用程序内存的1/8作为缓存，向ImageView加载一张图片时，先从LruCache缓存中获取，为空则开启线程去加载；否则直接填充。

```java
private LruCache<String, Bitmap> mMemoryCache;
 
@Override
protected void onCreate(Bundle savedInstanceState) {
	// 获取到可用内存的最大值，使用内存超出这个值会引起OutOfMemory异常。
	// LruCache通过构造函数传入缓存值，以KB为单位。
	int maxMemory = (int) (Runtime.getRuntime().maxMemory() / 1024);
	// 使用最大可用内存值的1/8作为缓存的大小。
	int cacheSize = maxMemory / 8;
	mMemoryCache = new LruCache<String, Bitmap>(cacheSize) {
		@Override
		protected int sizeOf(String key, Bitmap bitmap) {
			return bitmap.getByteCount() / 1024;
		}
	};
}
 
 /*
 添加Bitmap到内存缓存中去
*/
public void addBitmapToMemoryCache(String key, Bitmap bitmap) {
	if (getBitmapFromMemCache(key) == null) {
		mMemoryCache.put(key, bitmap);
	}
}
 
  /*
 内存缓存中获取对应key的Bitmap
*/
public Bitmap getBitmapFromMemCache(String key) {
	return mMemoryCache.get(key);
}

// 从缓存中删除指定的Bitmap
    public void removeBitmapFromMemory(String key) {
        mMemoryCache.remove(key);
    }

public void loadBitmap(int resId, ImageView imageView) {
	final String imageKey = String.valueOf(resId);
	final Bitmap bitmap = getBitmapFromMemCache(imageKey);
	if (bitmap != null) {
		imageView.setImageBitmap(bitmap);
	} else {
		imageView.setImageResource(R.drawable.image_placeholder);
		BitmapWorkerTask task = new BitmapWorkerTask(imageView);
		task.execute(resId);
	}
}
```

加载的异步任务：

```java
class BitmapWorkerTask extends AsyncTask<Integer, Void, Bitmap> {
	// 在后台加载图片。
	@Override
	protected Bitmap doInBackground(Integer... params) {
		final Bitmap bitmap = decodeSampledBitmapFromResource(
				getResources(), params[0], 100, 100);
		addBitmapToMemoryCache(String.valueOf(params[0]), bitmap);
		return bitmap;
	}
}
```

###### 7.2 DiskLruCache硬盘缓存

第一部分中提到LruCache缓存技术实现了管理内存中图片的存储与释放，如果图片从内存中被移除的话，那么又需要从网络上重新加载一次图片，这显然非常耗时。因此，Google又提出了一个新的方法，使用DiskLruCache对图片进行硬盘缓存。

现在我们大多数加载图片等用的都是第三方的框架如Glide等，会发现它们内部其实使用的也是DiskLruCache，它是如何使用的呢？

先从缓存的位置来说，它可以自定义缓存的路径，默认的路径为`/sdcard/Android/data/<application package>/cache路径`；默认路径的好处：

1. 存储在SD卡上，不会对内置存储造成影响
2. 应用程序卸载后，相应的文件也会被删除

以包名为com.wdl.card的APP为例，它的硬盘缓存的路径为：/sdcard/Android/data/com.wdl.card/cache

**使用DiskLruCache的标志：一个名为journal的文件，它是DiskLruCache的一个日志文件**

使用简介：工具类中包含获取APP版本号/获取缓存文件位置等功能

```java
package com.example.cachedemo;

import android.content.Context;
import android.content.pm.PackageManager;
import android.os.Environment;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.IOException;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.security.MessageDigest;

/**
 * 项目名：  PhotoWallDemo
 * 包名：    com.example.photowalldemo
 * 创建者：   wdl
 * 创建时间： 2019/2/18 14:39
 * 描述：    TODO
 */
public class Util {
    public static File getDiskCacheDir(Context context, String uniqueName) {
        String cachePath;
        if (Environment.MEDIA_MOUNTED.equals(Environment.getExternalStorageState())
                || !Environment.isExternalStorageRemovable()) {
            //SD卡存在且不可被移除时，调用getExternalCacheDir()获取缓存地址
            //  cachePath = /sdcard/Android/data/<application package>/cache
            cachePath = context.getExternalCacheDir().getPath();
        } else {
            // cachePath = /data/data/<application package>/cache
            cachePath = context.getCacheDir().getPath();
        }
        return new File(cachePath + File.separator + uniqueName);
    }

    /**
     * 网络下载并写入文件
     *
     * @param urlStr ip地址
     * @param os     OutputStream输出流
     * @return 是否写入成功
     */
    public static boolean downUrlToStream(final String urlStr, OutputStream os) {
        HttpURLConnection urlConnection = null;
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
            final URL url = new URL(urlStr);
            urlConnection = (HttpURLConnection) url.openConnection();
            bis = new BufferedInputStream(urlConnection.getInputStream(), 8 * 1024);
            bos = new BufferedOutputStream(os, 8 * 1024);
            int b;
            while ((b = bis.read()) != -1) {
                bos.write(b);
            }
            return true;
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (urlConnection != null) {
                urlConnection.disconnect();
            }
            try {
                if (bos != null) {
                    bos.close();
                }
                if (bis != null) {
                    bis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return false;
    }


    /**
     * 获取加密key
     *
     * @param key 图片对应的url
     * @return 加密后的url, 即为缓存文件的名称
     */
    public static String hashKeyForDisk(String key) {
        String cacheKey;
        try {
            final MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            messageDigest.update(key.getBytes());
            cacheKey = bytesToHexString(messageDigest.digest());
        } catch (Exception e) {
            return String.valueOf(key.hashCode());
        }
        return cacheKey;
    }

    private static String bytesToHexString(byte[] bytes) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < bytes.length; i++) {
            String hex = Integer.toHexString(0xFF & bytes[i]);
            if (hex.length() == 1) {
                sb.append('0');
            }
            sb.append(hex);
        }
        return sb.toString();
    }


    /**
     * 获取版本号
     *
     * @param context
     * @return
     */
    public static int getVersionCode(Context context) {
        int versionCode = 0;
        try {
            versionCode = context.getPackageManager().getPackageInfo(context.getPackageName(), 0).versionCode;
        } catch (PackageManager.NameNotFoundException e) {
            e.printStackTrace();
        }
        return versionCode;
    }

}

```

**1.打开缓存 调用其open()方法**

```java
public static DiskLruCache open(File directory, int appVersion, int valueCount, long maxSize)
1
```

各个参数的含义如下表：

| 参数       | 含义                                                         |
| ---------- | ------------------------------------------------------------ |
| directory  | 数据的缓存地址–获取缓存地址(考虑SD卡不存在或者SD卡刚刚被移除) |
| appVersion | app版本号                                                    |
| valueCount | 一个Key对应的缓存文件数                                      |
| maxSize    | 最多可以缓存多少字节的数据                                   |

例子：省略抛出异常

```java
DiskLruCache mDiskLruCache = null;
File cacheDir = getDiskCacheDir(context,'bitmap');
if(!cacheDir.exists()){
	cacheDir.mkdirs();
}
mDiskLruCache = DiskLruCache.open(cacheDir,getVersion(context),1,10*1024*1024);
123456
```

获得DiskLruCache实例后，就可以对其进行缓存的读取/写入/删除了

**2.写入**

先获取editor的实例后进行操作。

```
public Editor edit(String key) throws IOException key：代表缓存文件的名称且必须和图片url一一对应（利用MD5进行加密实现）
1
 new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    String url = "https://img-my.csdn.net/uploads/201309/01/1378037235_7476.jpg";
                    //获取缓存文件名
                    String key = Util.hashKeyForDisk(url);

                    DiskLruCache.Editor editor = mDiskLruCache.edit(key);
                    if (editor != null) {
                        OutputStream os = editor.newOutputStream(0);
                        if (Util.downUrlToStream(url, os)) {
                            editor.commit();
                        } else {
                            editor.abort();
                        }
                    }
                    mDiskLruCache.flush();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }).start();
```

获取实例后可调用它的newOutputStream(inte index)获取输出流，然后将其传入downloadUrlToStream中，即可实现下载并写入缓存目录
index:由于前面在设置valueCount的时候指定的是1，所以这里index传0就可以了。

写入后必须调用editor.commit()进行提交，调用abort()方法的话则表示放弃此次写入。

**3.读取–借助DiskLruCache.get()方法**

```
public synchronized Snapshot get(String key) throws IOException key：缓存文件名  Snapshot为返回值
1
```

利用 返回值的getInputStream(int index)获取输入流，最后进行显示

**4.移除缓存–DiskLruCache.remove(String key)**

```
public synchronized boolean remove(String key) throws IOException
1
```

**5.常用API**
`size()`获取缓存文件的大小
`flush()`将内存中的操作记录同步至日志文件（也就是journal文件）。。比较标准的做法就是在Activity的onPause()方法中去调用一次flush()方法就可以了。
`close()`关闭，通常是在destroy中调用，关闭后不可进行操作
`delete()`将缓存数据全部删除

###### **7.3 journal解读**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226101849862.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzQxMzM4,size_16,color_FFFFFF,t_70)

第一行 ： libcore.io.DiskLruCache固定字符，标志我们使用DiskLruCache技术
第二行 ： DiskLruCache的版本号，恒为1
第三行 ： open时传入的app版本号
第四行 ： open时传入的每个key对应的缓存文件数
第五行 ： 空行

第六行 ： DIRTTY前缀，后跟缓存图片的key； 每次调用DiskLruCache.edit(String key时)都会产生一条
后一行代表edit的结果，假如editor.commit()产生CLEAN key +该条缓存数据的大小，以字节为单位;缓存成功；假如editor.abort()产生REMOVE key,写入失败，删除；

前面我们所学的size()方法可以获取到当前缓存路径下所有缓存数据的总字节数，其实它的工作原理就是把journal文件中所有CLEAN记录的字节数相加，求出的总合再把它返回而已。

READ key 即调用DiskLruCache.get(String key)时产生的。

DiskLruCache中使用了一个redundantOpCount变量来记录用户操作的次数，每执行一次写入、读取或移除缓存的操作，这个变量值都会加1，当变量值达到2000的时候就会触发重构journal的事件，这时会自动把journal中一些多余的、不必要的记录全部清除掉，保证journal文件的大小始终保持在一个合理的范围内。

###### 7.4 DiskLruCache与LruCache结合实现照片墙

案例：

**RecyclerView的设配器类**：内部包含LruCache与DiskLruCache的使用；详见注释

```
package com.example.cachedemo;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.AsyncTask;
import android.support.annotation.NonNull;
import android.support.v7.widget.RecyclerView;
import android.util.LruCache;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.FrameLayout;
import android.widget.ImageView;

import com.jakewharton.disklrucache.DiskLruCache;

import java.io.File;
import java.io.FileDescriptor;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Random;
import java.util.Set;

/**
 * 创建时间： 2019/2/20 9:16
 * 描述：    TODO
 */
public class Adapter extends RecyclerView.Adapter<Adapter.ViewHolder> {

    private List<String> mList;
    private LruCache<String, Bitmap> lruCache;
    private DiskLruCache mDiskLruCache;
    private Set<Task> tasks;
    private RecyclerView rv;
    private Context context;
    private boolean isScrolling = false;

    /**
     * 记录每个子项的高度。
     */
    private List<Integer> hList;//定义一个List来存放图片的height

    public Adapter(List<String> mList, Context context, RecyclerView rv) {
        this.mList = mList;
        this.rv = rv;
        this.context = context;
        tasks = new HashSet<>();

        hList = new ArrayList<>();
        for (int i = 0; i < mList.size(); i++) {
            //每次随机一个高度并添加到hList中
            int height = new Random().nextInt(200) + 300;//[100,500)的随机数
            hList.add(height);
        }
        //初始化内存缓存
        int size = (int) ((Runtime.getRuntime().maxMemory() / 1024) / 8);
        lruCache = new LruCache<String, Bitmap>(size) {
            @Override
            protected int sizeOf(String key, Bitmap value) {
                return value.getByteCount() / 1024;
            }
        };

        //初始化硬盘缓存
        try {
            File cacheDir = Util.getDiskCacheDir(context, "bitmap");
            if (!cacheDir.exists())
                cacheDir.mkdirs();
            mDiskLruCache = DiskLruCache.open(cacheDir,
                    Util.getVersionCode(context), 1, 30 * 1024 * 1024);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    /**
     * 创建viewHolder,将xml传给viewholder
     *
     * @param parent
     * @param viewType
     * @return
     */
    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.recycler_view_item, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder viewHolder, int position) {
        final String urlStr = mList.get(position);
        //设置tag
        viewHolder.imageView.setTag(urlStr);
        //设置占位 防止图片错位
        viewHolder.imageView.setImageResource(R.drawable.ic_launcher_background);
        //设置宽高
        FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(context
                .getResources().getDisplayMetrics().widthPixels / 3, hList.get(position));
        viewHolder.imageView.setLayoutParams(params);

            loadBitmaps(viewHolder.imageView, urlStr);
    }

    public void setScrolling(boolean scrolling) {
        isScrolling = scrolling;
        notifyDataSetChanged();
    }

    /**
     * 加载图片
     *
     * @param imageView ImageView
     * @param urlStr    先从内存缓存中找，找不到，从硬盘缓存中找，找不到，网络下载并加载（存储硬盘缓存），存储到内存缓存
     */
    private void loadBitmaps(ImageView imageView, String urlStr) {
        Bitmap bitmap = getBitmapFromMemoryCache(urlStr);
        //根据滑动的状态判断是否加载图片
        if (bitmap == null&&!isScrolling) {
            Task task = new Task();
            tasks.add(task);
            task.execute(urlStr);
        } else {
            if (imageView != null) {
                imageView.setImageBitmap(bitmap);
            }
        }
    }


    @Override
    public int getItemCount() {
        return mList.size();
    }


    /**
     * 添加内存缓存中不存在的Bitmap
     *
     * @param key    键
     * @param bitmap 值
     */
    private void addBitmapToLruCache(String key, Bitmap bitmap) {
        if (getBitmapFromMemoryCache(key) == null)
            lruCache.put(key, bitmap);
    }

    /**
     * 从内存缓存中获取键为key的Bitmap
     *
     * @param key 键
     * @return Bitmap
     */
    private Bitmap getBitmapFromMemoryCache(String key) {
        return lruCache.get(key);
    }

    /**
     * 取消所有正在下载或等待下载的任务。
     */
    public void cancelAllTasks() {
        if (tasks != null) {
            for (Task task : tasks) {
                task.cancel(false);
            }
        }
    }


    /**
     * 将缓存记录同步到journal文件中。
     */
    public void flushCache() {
        if (mDiskLruCache != null) {
            try {
                mDiskLruCache.flush();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }


    class ViewHolder extends RecyclerView.ViewHolder {
        ImageView imageView;

        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            imageView = itemView.findViewById(R.id.iv_image);
        }
    }


    class Task extends AsyncTask<String, Void, Bitmap> {

        private String imageUrl;

        @Override
        protected Bitmap doInBackground(String... strings) {
            imageUrl = strings[0];
            FileDescriptor fd = null;
            FileInputStream fis = null;
            DiskLruCache.Snapshot snapshot = null;
            try {
                //生成key
                final String key = Util.hashKeyForDisk(imageUrl);
                snapshot = mDiskLruCache.get(key);
                //如果未找到缓存，则从网络上下载并存储至缓存中
                if (snapshot == null) {
                    DiskLruCache.Editor editor = mDiskLruCache.edit(key);
                    if (editor != null) {
                        OutputStream os = editor.newOutputStream(0);
                        if (Util.downUrlToStream(imageUrl, os)) {
                            editor.commit();
                        } else {
                            editor.abort();
                        }
                    }
                    //缓存被写入后再次从缓存中查找
                    snapshot = mDiskLruCache.get(key);
                }
                if (snapshot != null) {
                    fis = (FileInputStream) snapshot.getInputStream(0);
                    fd = fis.getFD();
                }
                //将缓存数据加载成Bitmap
                Bitmap bitmap = null;
                if (fd != null) {
                    bitmap = BitmapFactory.decodeFileDescriptor(fd);
                }
                if (bitmap != null) {
                    //将bitmap写入内存缓存中去
                    addBitmapToLruCache(imageUrl, bitmap);
                }
                return bitmap;
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                try {
                    if (fd == null && fis != null)
                        fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            return null;
        }

        @Override
        protected void onPostExecute(Bitmap bitmap) {
            super.onPostExecute(bitmap);
            ImageView imageView = rv.findViewWithTag(imageUrl);
            if (bitmap != null && imageView != null) {
                imageView.setImageBitmap(bitmap);
            }
            tasks.remove(this);

        }
    }
}

```

**MainActivity**：使用

```
package com.example.cachedemo;

import android.support.annotation.NonNull;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.StaggeredGridLayoutManager;
import android.util.Log;
import android.view.ViewTreeObserver;

import com.google.gson.Gson;
import com.google.gson.reflect.TypeToken;

import java.lang.reflect.Type;
import java.util.Arrays;
import java.util.List;

import static android.support.v7.widget.RecyclerView.SCROLL_STATE_DRAGGING;
import static android.support.v7.widget.RecyclerView.SCROLL_STATE_IDLE;

public class MainActivity extends AppCompatActivity {

    private RecyclerView rv;
    private Adapter adapter;
    @Override
    protected void onPause() {
        super.onPause();
        adapter.flushCache();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 退出程序时结束所有的下载任务
        adapter.cancelAllTasks();
    }
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        rv = findViewById(R.id.recycler_view);
        //设置瀑布流，2列竖直
        StaggeredGridLayoutManager layoutManager = new StaggeredGridLayoutManager(3,
                StaggeredGridLayoutManager.VERTICAL);
        //解决item跳动
       // layoutManager.setGapStrategy(StaggeredGridLayoutManager.GAP_HANDLING_NONE);
        rv.setLayoutManager(layoutManager);

        rv.setItemAnimator(null);
        adapter = new Adapter(Arrays.asList(Common.urls),this,rv);
        rv.setAdapter(adapter);

        //添加recycler view 滚动状态的监听，控制是否加载图片
        rv.addOnScrollListener(new RecyclerView.OnScrollListener() {
            @Override
            public void onScrollStateChanged(@NonNull RecyclerView recyclerView, int newState) {
                super.onScrollStateChanged(recyclerView, newState);
                switch (newState){
                    case SCROLL_STATE_IDLE:
                        //滑动停止
                        adapter.setScrolling(false);
                        break;
                    case SCROLL_STATE_DRAGGING:
                        //正在滚动
                        adapter.setScrolling(true);
                        break;

                }

            }

            @Override
            public void onScrolled(@NonNull RecyclerView recyclerView, int dx, int dy) {
                super.onScrolled(recyclerView, dx, dy);
            }
        });
//        Gson gson = new Gson();
//        List<Entity> mList = gson.fromJson(Common.s, new TypeToken<List<Entity>>() {
//        }.getType());
//        StringBuilder str = new StringBuilder();
//        for (Entity entity : mList) {
//            str.append("\"").append(entity.getUrl()).append("\",").append("\n");
//        }
//        Log.e("wdl",str.toString());

//        Entity[] entities = gson.fromJson(Common.s,new TypeToken<Entity>() {
//        }.getType());
//        for (Entity entity : entities) {
//            str.append(entity.getUrl()).append("\n");
//        }
//        Log.e("wdl",str.toString());
    }
}


```

效果展示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226102756231.gif)

**onScrollStateChanged()回调方法的主要功能。**
**优化之一，在RecyclerView子项滚动时禁止加载图片，停止滑动时开始加载图片**

## 【Activity专题】

##### [1] Activity是什么？

> **Android 程序核心组件:**
>
> **View**: 界面视图,组织 UI 控件 
>
> **Intent**: 意图,支持组件间通信 
>
> **Activity**: 处理界面与 UI 互动 
>
> **Content Provider**: 存储共享数据 
>
> **IntentReceiver**: 接收信息及事件处理
>
> **Service**: 后台服务(如硬件与驱动的服务) 
>
> **Notification**: 消息与通知。

我们都知道android中有四大组件（**Activity 活动，Service 服务，Content Provider 内容提供者，BroadcastReceiver 广播接收器**），Activity是我们用的最多也是最基本的组件，因为应用的所有操作都与用户相关，Activity 提供窗口来和用户进行交互。

官方文档这么说： 　　

> An activity is a single, focused thing that the user can do. Almost all activities interact with the user, so the Activity class takes care of creating a window for you in which you can place your UI with setContentView(View).
>
> 大概的意思：

> activity是独立平等的，用来处理用户操作。几乎所有的activity都是用来和用户交互的，所以activity类会创建了一个窗口，开发者可以通过setContentView(View)的接口把UI放到给窗口上。

　　Android中的activity全都归属于task管理 。task 是多个 activity 的集合，这些 activity 按照启动顺序排队存入一个栈（即“back stack”）。android默认会为每个App维持一个task来存放该app的所有activity，task的默认name为该app的packagename。

　　当然我们也可以在AndroidMainfest.xml中申明activity的taskAffinity属性来自定义task，但不建议使用，如果其他app也申明相同的task，它就有可能启动到你的activity，带来各种安全问题（比如拿到你的Intent）。

##### [2] Activity的生命周期

　　上面已经说了，系统通过堆栈来管理activity，当一个新的activity开始时，它被放置在堆栈的顶部和成为运行活动，以前的activity始终保持低于它在堆栈，而不会再次到达前台，直到新的活动退出。

还是上这张官网的activity_lifecycle图： 　　[![这里写图片描述](https://camo.githubusercontent.com/f986bb2922053692d116dda08d9173371414673d/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630343235313731373131303534)](https://camo.githubusercontent.com/f986bb2922053692d116dda08d9173371414673d/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630343235313731373131303534)　

1. 首先打开一个新的activity实例的时候，系统会依次调用

> onCreate（）  -> onStart() -> onResume() 然后开始running

2. running的时候被覆盖了（从它打开了新的activity或是被锁屏，但是它**依然在前台**运行， lost focus but is still visible），系统调用onPause();

> 　该方法执行activity暂停，通常用于提交未保存的更改到持久化数据，停止动画和其他的东西。但这个activity还是完全活着（它保持所有的状态和成员信息，并保持连接到**窗口管理器**）

3. 接下来它有三条出路：

 ①用户返回到该activity就调用onResume()方法重新running

 ②用户回到桌面或是打开其他activity，就会调用onStop()进入停止状态（保留所有的状态和成员信息，**对用户不可见**）

 ③系统内存不足，拥有更高限权的应用需要内存，那么该activity的进程就可能会被系统回收。（回收onRause()和onStop()状态的activity进程）要想重新打开就必须重新创建一遍。

4. 如果用户返回到onStop()状态的activity（又显示在前台了），系统会调用

> onRestart() ->  onStart() -> onResume() 然后重新running

5. 在activity结束（调用finish ()）或是被系统杀死之前会调用onDestroy()方法释放所有占用的资源。

> activity生命周期中三个嵌套的循环

- activity的完整生存期会在 onCreate() 调用和 onDestroy() 调用之间发生。　
- activity的可见生存期会在 onStart() 调用和 onStop() 调用之间发生。系统会在activity的整个生存期内多次调用 onStart() 和onStop()， 因为activity可能会在显示和隐藏之间不断地来回切换。　
- activity的前后台切换会在 onResume() 调用和 onPause() 之间发生。 因为这个状态可能会经常发生转换，为了避免切换迟缓引起的用户等待，**这两个方法中的代码应该相当地轻量化**。

##### [3] activity被回收的状态和信息保存和恢复过程

```java
public class MainActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		if(savedInstanceState!=null){ //判断是否有以前的保存状态信息
			 savedInstanceState.get("Key"); 
			 }
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
	}
   @Override
protected void onSaveInstanceState(Bundle outState) {
	// TODO Auto-generated method stub
	 //可能被回收内存前保存状态和信息，
	   Bundle data = new Bundle(); 
	   data.putString("key", "last words before be kill");
	   outState.putAll(data);
	super.onSaveInstanceState(outState);
}
   @Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
	// TODO Auto-generated method stub
	   if(savedInstanceState!=null){ //判断是否有以前的保存状态信息
			 savedInstanceState.get("Key"); 
			 }
	super.onRestoreInstanceState(savedInstanceState);
}
}
```

**onSaveInstanceState方法**

　　在activity　可能被回收之前　调用,用来保存自己的状态和信息，以便回收后重建时恢复数据（在onCreate()或onRestoreInstanceState()中恢复）。旋转屏幕重建activity会调用该方法，但其他情况在onRause()和onStop()状态的activity不一定会调用 ，下面是该方法的文档说明。

> One example of when onPause and onStop is called and not this method is when a user navigates back from activity B to activity A: there is no need to call onSaveInstanceState on B because that particular instance will never be restored, so the system avoids calling it. An example when onPause is called and not onSaveInstanceState is when activity B is launched in front of activity A: the system may avoid calling onSaveInstanceState on activity A if it isn't killed during the lifetime of B since the state of the user interface of A will stay intact.

也就是说，系统灵活的来决定调不调用该方法，**但是如果要调用就一定发生在onStop方法之前，但并不保证发生在onPause的前面还是后面。**

**onRestoreInstanceState方法**

　　这个方法在onStart 和 onPostCreate之间调用，在onCreate中也可以状态恢复，但有时候需要所有布局初始化完成后再恢复状态。

　　onPostCreate：一般不实现这个方法，当程序的代码开始运行时，它调用系统做最后的初始化工作。

##### [4] activity启动模式

**启动模式什么？**简单的说就是定义activity 实例与task 的关联方式。 　　

**为什么要定义启动模式？**

　　 为了实现一些默认启动（standard）模式之外的需求： 　　

- 让某个 activity 启动一个新的 task （而不是被放入当前 task ）
- 让 activity 启动时只是调出已有的某个实例（而不是在 back stack 顶创建一个新的实例）　
- 或者，你想在用户离开 task 时只保留根 activity，而 back stack 中的其它 activity 都要清空

**怎样定义启动模式？**

　　定义启动模式的方法有两种：

**使用 manifest 文件**

　　在 manifest 文件中activity声明时，利用 activity 元素的 launchMode 属性来设定 activity 与 task 的关系。

```
 <activity
            ．．．．．．
            android:launchMode="standard"
             >
           ．．．．．．．
        </activity>
```

> 注意： 你用 launchMode 属性为 activity 设置的模式可以被启动 activity 的 intent 标志所覆盖。

**有哪些启动模式？**

- **"standard"** （默认模式）　

　　当通过这种模式来启动Activity时,　Android总会为目标 Activity创建一个新的实例,并将该Activity添加到当前Task栈中。这种方式不会启动新的Task,只是将新的 Activity添加到原有的Task中。　 　　

- **"singleTop"**　

　　该模式和standard模式基本一致,但有一点不同: 当将要被启动的Activity已经位于Task栈顶时,系统不会重新创建目标Activity实例,而是直接复用Task栈顶的Activity。

- **"singleTask"**

　　Activity在同一个Task内只有一个实例。如果将要启动的Activity不存在,那么系统将会创建该实例,并将其加入Task栈顶；　

　　如果将要启动的Activity已存在,且存在栈顶,直接复用Task栈顶的Activity。　

　　如果Activity存在但是没有位于栈顶,那么此时系统会把位于该Activity上面的所有其他Activity全部移出Task,从而使得该目标Activity位于栈顶。

- **"singleInstance"**　

　　无论从哪个Task中启动目标Activity,只会创建一个目标Activity实例且会用一个全新的Task栈来装载该Activity实例（**全局单例**）.

　　如果将要启动的Activity不存在,那么系统将会先创建一个全新的Task,再创建目标Activity实例并将该Activity实例放入此全新的Task中。

　　如果将要启动的Activity已存在,那么无论它位于哪个应用程序,哪个Task中;系统都会把该Activity所在的Task转到前台,从而使该Activity显示出来。

**使用 Intent 标志**

　　在要启动 activity 时，你可以在传给 startActivity() 的 **intent** 中包含相应标志，以修改 **activity 与 task** 的默认关系。

```java
　　　　　Intent i = new Intent(this,ＮewActivity.class);
		i.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
		startActivity(i);
```

**可以通过标志修改的默认模式有哪些？**

- FLAG_ACTIVITY_NEW_TASK

　　与"singleTask"模式相同，在新的 task 中启动 activity。如果要启动的 activity 已经运行于某 task 中，则那个 task 将调入前台。

- FLAG_ACTIVITY_SINGLE_TOP

　　与 "singleTop"模式相同，如果要启动的 activity位于back stack 顶，系统不会重新创建目标Activity实例,而是直接复用Task栈顶的Activity。

- FLAG_ACTIVITY_CLEAR_TOP

　　**此种模式在launchMode中没有对应的属性值。**如果要启动的 activity 已经在当前 task 中运行，则不再启动一个新的实例，且所有在其上面的 activity 将被销毁。

**关于启动模式的一些建议**

　　 一般不要改变 activity 和 task 默认的工作方式。 如果你确定有必要修改默认方式，请保持谨慎，并确保 activity 在启动和从其它 activity 返回时的可用性，多做测试和安全方面的工作。

##### [5] Intent Filter

　　android的3个核心组件——Activity、services、广播接收器——是通过intent传递消息的。intent消息用于在运行时绑定不同的组件。在 Android 的 AndroidManifest.xml 配置文件中可以通过 intent-filter 节点为一个 Activity 指定其 Intent Filter，以便告诉系统该 Activity 可以响应什么类型的 Intent。

**intent-filter 的三大属性**

**Action**

　　一个 Intent Filter 可以包含多个 Action，Action 列表用于标示 Activity 所能接受的“动作”，它是一个用户自定义的字符串。

```
<intent-filter > 
 <action android:name="android.intent.action.MAIN" /> 
 <action android:name="com.scu.amazing7Action" /> 
……
 </intent-filter>
```

在代码中使用以下语句便可以启动该Intent 对象：

```
Intent i=new Intent(); 
i.setAction("com.scu.amazing7Action");
```

Action 列表中包含了“com.scu.amazing7Action”的 Activity 都将会匹配成功

**URL**

　　在 intent-filter 节点中，通过 data节点匹配外部数据，也就是通过 URI 携带外部数据给目标组件。

```
<data android:mimeType="mimeType" 
	android:scheme="scheme" 
	 android:host="host"
	 android:port="port" 
	 android:path="path"/>
```

注意：只有data的所有的属性都匹配成功时 URI 数据匹配才会成功

**Category**

　　为组件定义一个 类别列表，当 Intent 中包含这个类别列表的所有项目时才会匹配成功。

```
<intent-filter . . . >
   <action android:name="code android.intent.action.MAIN" />
   <category android:name="code　android.intent.category.LAUNCHER" />
</intent-filter>
```

**Activity 中 Intent Filter 的匹配过程**

① 加载所有的Intent Filter列表 　　

② 去掉action匹配失败的Intent Filter 　　

③ 去掉url匹配失败的Intent Filter 　

④ 去掉Category匹配失败的Intent Filter 　

⑤ 判断剩下的Intent Filter数目是否为0。如果为0查找失败返回异常；如果大于0，就按优先级排序，返回最高优先级的Intent Filter

##### [6] 开发中Activity的一些问题

一般设置Activity为非公开的

```java
<activity  
．．．．．． 
android:exported="false" /> 
```

注意：非公开的Activity不能设置intent-filter，以免被其他activity唤醒（如果拥有相同的intent-filter）。

- 不要指定activity的taskAffinity属性
- 不要设置activity的LaunchMode（保持默认）

　　注意Activity的intent最好也不要设定为FLAG_ACTIVITY_NEW_TASK

- 在匿名内部类中使用this时加上activity类名（类名.this,不一定是当前activity）
- 设置activity全屏

　　在其 onCreate()方法中加入：

```java
// 设置全屏模式
 getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN); 
 // 去除标题栏
 requestWindowFeature(Window.FEATURE_NO_TITLE);
```

## 【Service专题】

##### [1] 什么是服务？　　

　　Service是一个应用程序组件，它能够在后台执行一些耗时较长的操作，并且不提供用户界面。服务能被其它应用程序的组件启动，即使用户切换到另外的应用时还能保持后台运行。此外，应用程序组件还能与服务绑定，并与服务进行交互，甚至能进行进程间通信（IPC）。 比如，服务可以处理网络传输、音乐播放、执行文件I/O、或者与content provider进行交互，所有这些都是后台进行的。

##### [2] Service 与Thread的区别

　　服务仅仅是一个组件，即使用户不再与你的应用程序发生交互，它仍然能在后台运行。因此，应该只在需要时才创建一个服务。

　　如果你需要在主线程之外执行一些工作，但仅当用户与你的应用程序交互时才会用到，那你应该创建一个新的线程而不是创建服务。 比如，如果你需要播放一些音乐，但只是当你的activity在运行时才需要播放，你可以在onCreate()中创建一个线程，在onStart()中开始运行，然后在onStop()中终止运行。还可以考虑使用AsyncTask或HandlerThread来取代传统的Thread类。

　　**由于无法在不同的 Activity 中对同一 Thread 进行控制**，这个时候就要考虑用服务实现。如果你使用了服务，它默认就运行于应用程序的主线程中。因此，如果服务执行密集计算或者阻塞操作，你仍然应该在服务中创建一个新的线程来完成（避免ANR）。

##### [3] 服务的分类

**1. 按运行分类**

- 前台服务

　　前台服务是指那些经常会被用户关注的服务，因此内存过低时它不会成为被杀的对象。 前台服务必须提供一个状态栏通知，并会置于“正在进行的”（“Ongoing”）组之下。这意味着只有在服务被终止或从前台移除之后，此通知才能被解除。例如，用服务来播放音乐的播放器就应该运行在前台，因为用户会清楚地知晓它的运行情况。 状态栏通知可能会标明当前播放的歌曲，并允许用户启动一个activity来与播放器进行交互。

　　要把你的服务请求为前台运行，可以调用**startForeground()**方法。此方法有两个参数：唯一标识通知的整数值、状态栏通知Notification对象。例如：

```java
Notification notification = new Notification(R.drawable.icon, getText(R.string.ticker_text),System.currentTimeMillis());
Intent notificationIntent = new Intent(this,ExampleActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, notificationIntent, 0);
notification.setLatestEventInfo(this, getText(R.string.notification_title),
        getText(R.string.notification_message), pendingIntent);  
startForeground(ONGOING_NOTIFICATION, notification);
```

　　要从前台移除服务，请调用**stopForeground()**方法，这个方法接受个布尔参数，表示是否同时移除状态栏通知。此方法不会终止服务。不过，如果服务在前台运行时被你终止了，那么通知也会同时被移除。

- 后台服务

**2. 按使用分类**　　

- **本地服务**：用于应用程序内部，实现一些耗时任务，并不占用应用程序比如Activity所属线程，而是单开线程后台执行。调用Context.startService()启动，调用Context.stopService()结束。在内部可以调用Service.stopSelf() 或 Service.stopSelfResult()来自己停止。

- **远程服务**：用于Android系统内部的应用程序之间，可被其他应用程序复用，比如天气预报服务，其他应用程序不需要再写这样的服务，调用已有的即可。可以定义接口并把接口暴露出来，以便其他应用进行操作。客户端建立到服务对象的连接，并通过那个连接来调用服务。调用Context.bindService()方法建立连接，并启动，以调用 Context.unbindService()关闭连接。多个客户端可以绑定至同一个服务。如果服务此时还没有加载，bindService()会先加载它。

##### [4] Service生命周期

　                                   ![img](https://upload-images.jianshu.io/upload_images/4625401-84380bfeb9c4b0ff.png?imageMogr2/auto-orient/strip|imageView2/2/w/526/format/webp)



【链接：https://www.jianshu.com/p/cc25fbb5c0b3】

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200901224652977.png" alt="image-20200901224652977" style="zoom:80%;" />



**Service生命周期方法：**

```java
public class ExampleService extends Service {
    int mStartMode;       // 标识服务被杀死后的处理方式
    IBinder mBinder;      // 用于客户端绑定的接口
    boolean mAllowRebind; // 标识是否使用onRebind

    @Override
    public void onCreate() {
        // 服务正被创建
    }
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // 服务正在启动，由startService()调用引发
        return mStartMode;
    }
    @Override
    public IBinder onBind(Intent intent) {
        // 客户端用bindService()绑定服务
        return mBinder;
    }
    @Override
    public boolean onUnbind(Intent intent) {
        // 所有的客户端都用unbindService()解除了绑定
        return mAllowRebind;
    }
    @Override
    public void onRebind(Intent intent) {
        // 某客户端正用bindService()绑定到服务,
        // 而onUnbind()已经被调用过了
    }
    @Override
    public void onDestroy() {
        // 服务用不上了，将被销毁
    }
}
```

> 请注意onStartCommand()方法必须返回一个整数。这个整数是描述系统在杀死服务之后应该如何继续运行。onStartCommand()的返回值必须是以下常量之一：

> START_NOT_STICKY 如果系统在onStartCommand()返回后杀死了服务，则不会重建服务了，除非还存在未发送的intent。 当服务不再是必需的，并且应用程序能够简单地重启那些未完成的工作时，这是避免服务运行的最安全的选项。START_STICKY 如果系统在onStartCommand()返回后杀死了服务，则将重建服务并调用onStartCommand()，但不会再次送入上一个intent， 而是用null intent来调用onStartCommand() 。除非还有启动服务的intent未发送完，那么这些剩下的intent会继续发送。 这适用于媒体播放器（或类似服务），它们不执行命令，但需要一直运行并随时待命。　

> START_REDELIVER_INTENT 如果系统在onStartCommand()返回后杀死了服务，则将重建服务并用上一个已送过的intent调用onStartCommand()。任何未发送完的intent也都会依次送入。这适用于那些需要立即恢复工作的活跃服务，比如下载文件。

　　服务的生命周期与activity的非常类似。不过，更重要的是你需密切关注服务的创建和销毁环节，因为后台运行的服务是不会引起用户注意的。

　　服务的生命周期——从创建到销毁——可以有两种路径：

- **一个started服务**

　　这类服务由其它组件调用startService()来创建。然后保持运行，且**必须通过调用stopSelf()自行终止**。其它组件也可通过调用stopService() 终止这类服务。服务终止后，系统会把它销毁。

　　如果一个Service被startService 方法多次启动，那么onCreate方法只会调用一次，onStart将会被调用多次（对应调用startService的次数），并且**系统只会创建Service的一个实例**（因此你应该知道只需要一次stopService调用）。该Service将会一直在后台运行，而不管对应程序的Activity是否在运行，直到被调用stopService，或自身的stopSelf方法。当然如果系统资源不足，android系统也可能结束服务。

- **一个bound服务**

　　服务由其它组件（客户端）调用bindService()来创建。然后客户端通过一个**IBinder接口与服务进行通信**。客户端可以通过调用unbindService()来关闭联接。多个客户端可以绑定到同一个服务上，当所有的客户端都解除绑定后，系统会销毁服务。（服务不需要自行终止。）

　　如果一个Service被某个Activity 调用 Context.bindService 方法绑定启动，不管调用 bindService 调用几次，onCreate方法都只会调用一次，同时onStart方法始终不会被调用。当连接建立之后，Service将会一直运行，除非调用Context.unbindService 断开连接或者之前调用bindService 的 Context 不存在了（如Activity被finish的时候），系统将会自动停止Service，对应onDestroy将被调用。

![img](https://upload-images.jianshu.io/upload_images/4625401-756d89b600d55081.png?imageMogr2/auto-orient/strip|imageView2/2/w/404/format/webp)

　　这两条路径并不是完全隔离的。也就是说，你可以绑定到一个已经用startService()启动的服务上。例如，一个后台音乐服务可以通过调用startService()来启动，传入一个指明所需播放音乐的 Intent。 之后，用户也许需要用播放器进行一些控制，或者需要查看当前歌曲的信息，这时一个activity可以通过调用bindService()与此服务绑定。在类似这种情况下，stopService()或stopSelf()不会真的终止服务，除非所有的客户端都解除了绑定。

> 　　当在旋转手机屏幕的时候，当手机屏幕在“横”“竖”变换时，此时如果你的 Activity 如果会自动旋转的话，旋转其实是 Activity 的重新创建，因此旋转之前的使用 bindService 建立的连接便会断开（Context 不存在了）。

**在manifest中声明服务**

　　无论是什么类型的服务都必须在manifest中申明，格式如下：

```
<manifest ... >
  ...
  <application ... >
      <service android:name=".ExampleService" />
      ...
  </application>
</manifest>
```

Service 元素的属性有：

> android:name　　-------------　　服务类名

> android:label　　--------------　　服务的名字，如果此项不设置，那么默认显示的服务名则为类名

> android:icon　　--------------　　服务的图标

> android:permission　　-------　　申明此服务的权限，这意味着只有提供了该权限的应用才能控制或连接此服务

> android:process　　----------　　表示该服务是否运行在另外一个进程，如果设置了此项，那么将会在包名后面加上这段字符串表示另一进程的名字

> android:enabled　　----------　　如果此项设置为 true，那么 Service 将会默认被系统启动，不设置默认此项为 false

> android:exported　　---------　　表示该服务是否能够被其他应用程序所控制或连接，不设置默认此项为 false　

　　android:name是唯一必需的属性——它定义了服务的类名。与activity一样，服务可以定义intent过滤器，使得其它组件能用隐式intent来调用服务。如果你想让服务只能内部使用（其它应用程序无法调用），那么就不必（也不应该）提供任何intent过滤器。 　　此外，如果包含了android:exported属性并且设置为"false"， 就可以确保该服务是你应用程序的私有服务。即使服务提供了intent过滤器，本属性依然生效。　

**startService 启动服务**

　　从activity或其它应用程序组件中可以启动一个服务，调用startService()并传入一个Intent（指定所需启动的服务）即可。

```java
	Intent intent = new Intent(this, MyService.class);
	startService(intent);
```

服务类：

```java
public class MyService extends Service {

	  /**
     * onBind 是 Service 的虚方法，因此我们不得不实现它。
     * 返回 null，表示客服端不能建立到此服务的连接。
     */
	@Override
	public IBinder onBind(Intent intent) {
		// TODO Auto-generated method stub
		return null;
	}
    
	@Override
    public void onCreate() {
        super.onCreate();
    }
     
    @Override
 public int onStartCommand(Intent intent, int flags, int startId)  　　 {  	
    //接受传递过来的intent的数据 
     return START_STICKY; 
    };
     
    @Override
    public void onDestroy() {
        super.onDestroy();
    }
	
}
```

　　一个started服务必须自行管理生命周期。也就是说，系统不会终止或销毁这类服务，除非必须恢复系统内存并且服务返回后一直维持运行。 因此，服务必须通过调用stopSelf()自行终止，或者其它组件可通过调用stopService()来终止它。

**bindService 启动服务**　　

　　当应用程序中的activity或其它组件需要与服务进行交互，或者应用程序的某些功能需要暴露给其它应用程序时，你应该创建一个bound服务，并通过进程间通信（IPC）来完成。

方法如下：

```
 Intent intent=new Intent(this,BindService.class); 
 bindService(intent, ServiceConnection conn, int flags)  
```

> 注意bindService是Context中的方法，当没有Context时传入即可。

在进行服务绑定的时，其flags有：

- Context.BIND_AUTO_CREATE

　　表示收到绑定请求的时候，如果服务尚未创建，则即刻创建，在系统内存不足需要先摧毁优先级组件来释放内存，且只有驻留该服务的进程成为被摧毁对象时，服务才被摧毁　

- Context.BIND_DEBUG_UNBIND    　

　　通常用于调试场景中判断绑定的服务是否正确，但容易引起内存泄漏，因此非调试目的的时候不建议使用

- Context.BIND_NOT_FOREGROUND    　

　　表示系统将阻止驻留该服务的进程具有前台优先级，仅在后台运行。

服务类：

```
public class BindService extends Service {

	 // 实例化MyBinder得到mybinder对象；
	private final MyBinder binder = new MyBinder();
	
	  /**
     * 返回Binder对象。
     */
	@Override
	public IBinder onBind(Intent intent) {
		// TODO Auto-generated method stub
		return binder;
	}
    
     /**
      * 新建内部类MyBinder，继承自Binder(Binder实现IBinder接口),
      * MyBinder提供方法返回BindService实例。
      */
　　public class MyBinder extends Binder{
        
        public BindService getService(){
            return BindService.this;
        }
    }
     

	@Override
	public boolean onUnbind(Intent intent) {
		// TODO Auto-generated method stub
		return super.onUnbind(intent);
	}
}
```

启动服务的activity代码：

```
public class MainActivity extends Activity {

	/** 是否绑定 */  
	boolean mIsBound = false; 
	BindService mBoundService;
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		doBindService();
	}
	/**
	 * 实例化ServiceConnection接口的实现类,用于监听服务的状态
	 */
	private ServiceConnection conn = new ServiceConnection() {  
		  
	    @Override  
	    public void onServiceConnected(ComponentName name, IBinder service) {  
	        BindService mBoundService = ((BindService.MyBinder) service).getService();  
	        
	    }  
	  
	    @Override  
	    public void onServiceDisconnected(ComponentName name) {  
	        mBoundService = null;  
	     
	    }  
	}; 
	
	/** 绑定服务 */  
	public void doBindService() {  
	    bindService(new Intent(MainActivity.this, BindService.class), conn,Context.BIND_AUTO_CREATE);  
	    mIsBound = true;  
	}  
	
	/** 解除绑定服务 */  
	public void doUnbindService() {  
	    if (mIsBound) {  
	        // Detach our existing connection.  
	        unbindService(conn);  
	        mIsBound = false;  
	    }  
	} 
	
	@Override
	protected void onDestroy() {
		// TODO Auto-generated method stub
		super.onDestroy();
		
		doUnbindService();
	}
}
```

> 注意在AndroidMainfest.xml中对Service进行显式声明

判断Service是否正在运行：

```
private boolean isServiceRunning() {
    ActivityManager manager = (ActivityManager) getSystemService(ACTIVITY_SERVICE);
    
 　{
        if ("com.example.demo.BindService".equals(service.service.getClassName())) 　　{
            return true;
        }
    }
    return false;
}
```

##### [5] [bindService与startService区别](https://www.cnblogs.com/yesphet/p/4766786.html)

1. Started Service中使用startService（）方法来进行方法的调用，调用者和服务之间没有联系，即使调用者退出了，服务依然在进行 【onCreate()-  >onStartCommand()->startService()->onDestroy()】，注意其中没有 onStart()，主要是被onStartCommand()方法给取代了，onStart方法不推荐使用了。
2. BindService中使用bindService()方法来绑定服务，调用者和绑定者绑在一起，调用者一旦退出服务也就终止了【onCreate()->onBind()->onUnbind()->onDestroy()】。

>采用**Context.startService()**方法启动服务，在服务未被创建时，系统会先调用服务的onCreate()方法，接着调用onStart()方法。如果调用startService()方法前服务已经被创建，多次调用startService()方法并不会导致多次创建服务，但会导致多次调用onStart()方法。采用startService()方法启动的服务，只能调用Context.stopService()方法结束服务，服务结束时会调用onDestroy()方法。
>
>
>采用**Context.bindService()**方法启动服务，在服务未被创建时，系统会先调用服务的 onCreate()方法，接着调用onBind()方法。这个时候调用者和服务绑定在一起，调用者退出了，系统就会先调用服务的onUnbind()方 法，接着调用onDestroy()方法。如果调用bindService()方法前服务已经被绑定，多次调用bindService()方法并不会导致 多次创建服务及绑定(也就是说onCreate()和onBind()方法并不会被多次调用)。如果调用者希望与正在绑定的服务解除绑定，可以调用 unbindService()方法，调用该方法也会导致系统调用服务的onUnbind()-->onDestroy()方法。 

##### [6] IntentService详细解析

1. **IntentService定义**

　　IntentService继承于Service，用来处理异步请求。客户端可以通过startService(Intent)方法传递请求给IntentService。IntentService在onCreate()函数中通过HandlerThread单独开启一个线程来依次处理所有Intent请求对象所对应的任务。这样以免事务处理阻塞主线程（ＡＮＲ）。执行完所一个Intent请求对象所对应的工作之后，如果没有新的Intent请求达到，则**自动停止**Service；否则执行下一个Intent请求所对应的任务。　 　　    IntentService在处理事务时，还是采用的Handler方式，创建一个名叫ServiceHandler的内部Handler，并把它直接绑定到HandlerThread所对应的子线程。 ServiceHandler把处理一个intent所对应的事务都封装到叫做**onHandleIntent**的虚函数；因此我们直接实现虚函数onHandleIntent，再在里面根据Intent的不同进行不同的事务处理就可以了。 另外，IntentService默认实现了Onbind（）方法，返回值为null。

使用IntentService需要实现的两个方法： 　　

- **构造函数**　

　　IntentService的构造函数一定是**参数为空**的构造函数，然后再在其中调用super("name")这种形式的构造函数。因为Service的实例化是系统来完成的，而且系统是用参数为空的构造函数来实例化Service的

- **实现虚函数onHandleIntent**

　　在里面根据Intent的不同进行不同的事务处理。好处：处理异步请求的时候可以减少写代码的工作量，比较轻松地实现项目的需求。

2. **IntentService与Service的区别**

　　Service不是独立的进程，也不是独立的线程，它是依赖于应用程序的主线程的，不建议在Service中编写耗时的逻辑和操作，否则会引起ANR。

　　IntentService 它创建了一个独立的工作线程来处理所有的通过onStartCommand()传递给服务的intents（把intent插入到工作队列中）。通过工作队列把intent逐个发送给onHandleIntent()。不需要主动调用stopSelft()来结束服务。因为，在所有的intent被处理完后，系统会自动关闭服务。

　　 默认实现的onBind()返回null。

3. **IntentService实例介绍**

　　首先是myIntentService.java

```java
public class myIntentService extends IntentService {

	//------------------必须实现-----------------------------
	
	public myIntentService() {
		super("myIntentService");
		// 注意构造函数参数为空，这个字符串就是worker thread的名字
	}

	@Override
	protected void onHandleIntent(Intent intent) {
		//根据Intent的不同进行不同的事务处理 
        String taskName = intent.getExtras().getString("taskName");  
        switch (taskName) {
		case "task1":
			Log.i("myIntentService", "do task1");
			break;
		case "task2":
			Log.i("myIntentService", "do task2");
			break;
		default:
			break;
		}		
	}
  //--------------------用于打印生命周期--------------------	
   @Override
  public void onCreate() {
		Log.i("myIntentService", "onCreate");
	super.onCreate();
}
	
	@Override
	public int onStartCommand(Intent intent, int flags, int startId) {
		Log.i("myIntentService", "onStartCommand");
		return super.onStartCommand(intent, flags, startId);
	}
	
	@Override
	public void onDestroy() {
		Log.i("myIntentService", "onDestroy");
		super.onDestroy();
	}
}
```

然后记得在Manifest.xml中注册服务

```java
 <service android:name=".myIntentService">
            <intent-filter >  
                <action android:name="cn.scu.finch"/>  
            </intent-filter>     
        </service>
```

最后在Activity中开启服务

```java
public class MainActivity extends Activity {
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		// TODO Auto-generated method stub
		super.onCreate(savedInstanceState);
		
		//同一服务只会开启一个worker thread，在onHandleIntent函数里依次处理intent请求。
		
        Intent i = new Intent("cn.scu.finch");  
        Bundle bundle = new Bundle();  
        bundle.putString("taskName", "task1");  
        i.putExtras(bundle);  
        startService(i);  
           
        Intent i2 = new Intent("cn.scu.finch");  
        Bundle bundle2 = new Bundle();  
        bundle2.putString("taskName", "task2");  
        i2.putExtras(bundle2);  
        startService(i2); 
        
        startService(i);  //多次启动
	}
}
```

运行结果：

[![这里写图片描述](https://camo.githubusercontent.com/fb6bf8fc2ff7c1713ef558183b6ab0f47cb846e3/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630353133313335343131303337)](https://camo.githubusercontent.com/fb6bf8fc2ff7c1713ef558183b6ab0f47cb846e3/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630353133313335343131303337)　

　　IntentService在onCreate()函数中通过HandlerThread单独开启一个线程来依次处理所有Intent请求对象所对应的任务。通过onStartCommand()传递给服务intent被**依次**插入到工作队列中。工作队列又把intent逐个发送给onHandleIntent()。

> 注意： 它只有一个工作线程，名字就是构造函数的那个字符串，也就是“myIntentService”，我们知道多次开启service，只会调用一次onCreate方法（创建一个工作线程），多次onStartCommand方法（用于传入intent通过工作队列再发给onHandleIntent函数做处理）。

##### [7] IntentService——Handler与Service的结合 

**综述**

　　我们都知道Service是作为后台服务运行再程序中的。但是Service他依然是运行在主线程中的，所以我们依然不能在Service中进行耗时的操作。所以当我们在Service处理时，我们需要在Service中开启一个子线程，并且在子线程中运行。当然为了简化我们的操作，在Android中为我们提供了IntentService来进行这一处理，下面我们就来看一下这个IntentService用法以及它的工作原理。

**用法简介**

　　IntentService它继承自Service，一来说我们开启一个Service可以通过startService和bindService两个方式进行开启一个服务，但是对于IntentService我们采用startService方法进行开启服务，对于为什么要这么做，在后面会进行分析讲解。下面我们来看一下如何使用这个IntentService的。

**效果演示**

　　在这里我们做一个倒计时的程序，以毫秒为单位。这里先看一下效果演示。 

​                                                ![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTpy8CspBHm5RjmJsZbU6YsKibeaWobtRBCg7ahv5g76bqR8TosABUmDA/0?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

**代码分析**

　　在这里我们使用到了开源框架EventBus，对于EventBus的使用可以参考 EventBus3.0使用详解这篇文章。由于我们用到这EventBus,首先我们创建一个实体类，在EventBus中进行发送，接收处理。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTkzbscibibDjE0rNJxRhpCgmk7xcZrkkWl3tlu1UWsmibfX3nJ93FlAVCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

下面我们看一下IntentService中的代码。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTO8QD9S1YNfsbpseDhazeHJLplSvQv4xiaS6PjRne1AmC2rT5lkFhmCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSThDRPckUxibsNm9yicNEL07HEMW8NFic1dP3ehWYMt2S5VjPFCWejrK4Yg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
    在上面的handleActionFoo方法中进行我们的耗时任务。然后我们在看一下Activity中的代码。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTwRIh3HDECYkicHnkUIB8SjanSUW59HrKBaNNbc6djlYUHu0pJDPupkA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTTTiaDiacJZZmJTCbmBKRuHItpUV1pbrictSPx0oAiaEsia9sH22CdWLSb4Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

　　最后是布局代码。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTXoG5nZJrnP1Exh0KUFjriaVqEInkokB2ZdvLqTdYgz74yRl3mZSSmqw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

　　对于上面代码实现起来都是非常的简单，在这里就不在进行详细介绍。

**IntentService工作原理分析**

　　其实对于IntentService的工作原理也不复杂，既然在IntentService中能够进行耗时操作，也就是说在这个IntentService中必然也创建了一个子线程，在Android中我们称为工作者线程。然后在这个工作者线程中进行我们的任务。在分析IntentService之前，我们先看一下HandlerThread。

**HandlerThread**

　　其实HandlerThread就是一个工作者线程，在这里看一下HandlerThread的源码。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTepsCEdZwVLB1fibYxF4RKttibspqmCrg2AcrsyiaibXibSUkn92aWOf86yA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)　　![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTKkbVSAAU3nkPr7Uybk9pBznvdejYPMZ6uwLAyNJ006t6EMXY6ib8ViaA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

​    看过上篇文章 Android的消息机制——Handler的工作过程就很容易理解这个HandlerThread了。还记的我们在上篇文章的最后，新建了一个包含Looper的子线程。而这个HandlerThread也就是一个包含Looper的子线程。所以当我们需要创建一个包含Looper的线程时直接使用HandlerThread即可。对于HandlerThread有以下几点需要说明一下。 

  　　1. 在构造方法中设置线程优先级的时候，使用的Process是android.os包中的而不是java.lang包内的。 
        　　2. 如果在Looper开启消息循环之前我们进行一些设置，我们可以继承HandlerThread并且重写onLooperPrepared方法。 
              　　3. 通过getLooper方法我们获取HandlerThread的Looper对象时，有可能Looper还未创建完成。所以在getLooper中未创建Looper是进行了线程等待操作，在创建完Looper以后在返回Looper对象。

**IntentService**

　　下面我们再看一下IntentService。

![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTKvgBvpPOQ2jF5pxJO2cQ0bJnm55xSO7K4EW6m62Zavjadb2hB2JNzw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
![img](http://mmbiz.qpic.cn/mmbiz/ibuh47bPhianYgmJ0lbibDDuMmxjwQMlxSTxhw7cqTxFtMs3Y6QvTmRUAjHpDZQFzfVHqEVqowTS0g1RBP1WkxzXg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

　　我们看一下这个IntentService的构造是不是很简单。在这里主要看一下onCreate和onStart方法即可。在onCreate中，我们开启了一个HandlerThread线程，之后获取HandlerThread线程中的Looper，并通过这个Looper创建了一个Handler。然后在onStart方法中通过这个Handler将intent与startId作为Message的参数进行发送到消息队列中，然后交由Handler中的handleMessage中进行处理。由于在onStart方法是在主线程内运行的，而Handler是通过工作者线程HandlerThread中的Looper创建的。所以也就是在主线程中发送消息，在工作者接收到消息后便可以进行一些耗时的操作。 
　　我们在看一下handleMessage中的操作，在handleMessage中调用onHandleIntent方法，他是一个抽象方法，所以在我们的Service中复写onHandleIntent方法并且将耗时的操作写在onHandleIntent方法内即可。当执行完onHandleIntent后通过stopSelf来停止服务，这样就不用我们手动停止服务了。所以也就回答了我们上面那个为什么要使用startService而不用onBind来开启一个IntentService。

**总结**

　　从我们的示例和源码分析中可以看出来。对于通过IntentService来执行任务，他是串行的。也就是说只有在上一个任务执行完以后才会执行下一个任务。因为Handler中将消息插入消息队列，而队列又是先进先出的数据结构。所以只有在上个任务执行完成以后才能够获取到下一个任务进行操作。在这里也就说明了对于高并发的任务同过IntentService是不合适.

## 【ContentProvider专题】

##### [1] ContentProvider是什么？

　　**ContentProvider（内容提供者）是Android的四大组件之一**，管理android以结构化方式存放的数据，以相对安全的方式封装数据（表）并且提供简易的处理机制和统一的访问接口供**其他程序**调用。Android的数据存储方式总共有五种，分别是：**Shared Preferences、网络存储、文件存储、外储存储、SQLite**。但一般这些存储都只是在单独的一个应用程序之中达到一个数据的共享，有时候**我们需要操作其他应用程序的一些数据，就会用到ContentProvider**。而且Android为常见的一些数据提供了默认的ContentProvider（包括音频、视频、图片和通讯录等）。

　　但注意**ContentProvider它也只是一个中间人**，真正操作的数据源可能是数据库，也可以是文件、xml或网络等其他存储方式。

##### [2] URL

　　URL（统一资源标识符）代表要操作的数据，可以用来标识每个ContentProvider，这样你就可以通过指定的URI找到想要的ContentProvider, 从中获取或修改数据。在Android中URI的格式如下图所示：

[![这里写图片描述](https://camo.githubusercontent.com/1e138aeb9ce10fa4b788b18659fae3d8d29da73a/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630353035313534333232303435)](https://camo.githubusercontent.com/1e138aeb9ce10fa4b788b18659fae3d8d29da73a/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630353035313534333232303435)　

　　

- Ａ： schema，已经由Android所规定为：content://．　 　　　
- Ｂ：主机名（Authority），是URI的授权部分，是唯一标识符，用来定位ContentProvider。

> Ｃ部分和D部分：是每个ContentProvider内部的路径部分

- Ｃ：指向一个对象集合，一般用表的名字，如果没有指定D部分，则返回全部记录。

- Ｄ：指向特定的记录，这里表示操作user表id为7的记录。如果要操作user表中id为7的记录的name字段， D部分变为       **/7/name**即可。

> URI模式匹配通配符
>
> *：匹配的任意长度的任何有效字符的字符串。
>
> ＃：匹配的任意长度的数字字符的字符串。
>
> 如：
>
> content://com.example.app.provider/* 匹配provider的任何内容url
>
> content://com.example.app.provider/table3/# 匹配table3的所有行

**2.１MIME**

　　MIME是指定某个扩展名的文件用一种应用程序来打开，就像你用浏览器查看PDF格式的文件，浏览器会选择合适的应用来打开一样。Android中的工作方式跟HTTP类似，ContentProvider会根据URI来返回MIME类型，ContentProvider会返回一个包含两部分的字符串。MIME类型一般包含两部分，如：

> text/html text/css text/xml application/pdf

　　分为类型和子类型，Android遵循类似的约定来定义MIME类型，每个内容类型的Android MIME类型有两种形式：多条记录（集合）和单条记录。

　　集合记录：

```
vnd.android.cursor.dir/自定义
```

　　单条记录：

```
vnd.android.cursor.item/自定义
```

　　vnd表示这些类型和子类型具有非标准的、供应商特定的形式。Android中类型已经固定好了，不能更改，只能区别是集合还是单条具体记录，子类型可以按照格式自己填写。在使用Intent时，会用到MIME，根据Mimetype打开符合条件的活动。

　　下面分别介绍Android系统提供了两个用于操作Uri的工具类：ContentUris和UriMatcher。

**2.２ ContentUris**

　　ContetnUris包含一个便利的函数withAppendedId()来向URI追加一个id。

```
Uri uri = Uri.parse("content://cn.scu.myprovider/user")
Uri resultUri = ContentUris.withAppendedId(uri, 7); 

//生成后的Uri为：content://cn.scu.myprovider/user/7
```

　　同时提供parseId(uri)方法用于从URL中获取ID:

```
Uri uri = Uri.parse("content://cn.scu.myprovider/user/7")
long personid = ContentUris.parseId(uri);
//获取的结果为:7
```

**2.３UriMatcher**

　　UriMatcher本质上是一个文本过滤器，用在contentProvider中帮助我们过滤，分辨出查询者想要查询哪个数据表。

　　举例说明：

- 第一步，初始化：

```
UriMatcher matcher = new UriMatcher(UriMatcher.NO_MATCH);
//常量UriMatcher.NO_MATCH表示不匹配任何路径的返回码
```

- 第二步，注册需要的Uri：

```
//USER 和 USER_ID是两个int型数据
matcher.addURI("cn.scu.myprovider", "user", USER);
matcher.addURI("cn.scu.myprovider", "user/#",USER_ID);
//如果match()方法匹配content://cn.scu.myprovider/user路径，返回匹配码为USER
```

- 第三部，与已经注册的Uri进行匹配:

```
/* 
     * 如果操作集合，则必须以vnd.android.cursor.dir开头 
     * 如果操作非集合，则必须以vnd.android.cursor.item开头 
     * */  
    @Override  
    public String getType(Uri uri) {  
    Uri uri = Uri.parse("content://" + "cn.scu.myprovider" + "/user");  
        switch(matcher.match(uri)){  
        case USER:  
            return "vnd.android.cursor.dir/user";  
        case USER_ID:  
            return "vnd.android.cursor.item/user";  
        }  
    } 
```

##### [3] ContentProvider的主要方法

> public boolean onCreate()

　　ContentProvider创建后或打开系统后其它应用第一次访问该ContentProvider时调用。

> public Uri insert(Uri uri, ContentValues values)

　　外部应用向ContentProvider中添加数据。

> public int delete(Uri uri, String selection, String[] selectionArgs)

　　外部应用从ContentProvider删除数据。

> public int update(Uri uri, ContentValues values, String selection, String[] selectionArgs)：

　　外部应用更新ContentProvider中的数据。

> public Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder)　

　　供外部应用从ContentProvider中获取数据。 　

> public String getType(Uri uri)

　　该方法用于返回当前Url所代表数据的MIME类型。

##### [4] ContentResolver

　　ContentResolver通过URI来查询ContentProvider中提供的数据。除了URI以 外，还必须知道需要获取的数据段的名称，以及此数据段的数据类型。如果你需要获取一个特定的记录，你就必须知道当前记录的ID，也就是URI中D部分。

　　ContentResolver 类提供了与ContentProvider类相同签名的四个方法：

> public Uri insert(Uri uri, ContentValues values)　//添加

> public int delete(Uri uri, String selection, String[] selectionArgs)　//删除
>
> public int update(Uri uri, ContentValues values, String selection, String[] selectionArgs)　//更新
>
> public Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder)//获取

实例代码：

```
ContentResolver resolver =  getContentResolver();
Uri uri = Uri.parse("content://cn.scu.myprovider/user");

//添加一条记录
ContentValues values = new ContentValues();
values.put("name", "fanrunqi");
values.put("age", 24);
resolver.insert(uri, values);  

//获取user表中所有记录
Cursor cursor = resolver.query(uri, null, null, null, "userid desc");
while(cursor.moveToNext()){
   //操作
}

//把id为1的记录的name字段值更改新为finch
ContentValues updateValues = new ContentValues();
updateValues.put("name", "finch");
Uri updateIdUri = ContentUris.withAppendedId(uri, 1);
resolver.update(updateIdUri, updateValues, null, null);

//删除id为2的记录
Uri deleteIdUri = ContentUris.withAppendedId(uri, 2);
resolver.delete(deleteIdUri, null, null);
```

##### [5] ContentObserver

　　　 ContentObserver(内容观察者)，目的是观察特定Uri引起的数据库的变化，继而做一些相应的处理，它类似于数据库技术中的触发器(Trigger)，当ContentObserver所观察的Uri发生变化时，便会触发它.

```
下面是使用内容观察者监听短信的例子：
public class MainActivity extends Activity {
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
         
//注册观察者Observser    
this.getContentResolver().registerContentObserver(Uri.parse("content://sms"),true,new SMSObserver(new Handler()));
 
    }
 
    private final class SMSObserver extends ContentObserver {
 
        public SMSObserver(Handler handler) {
            super(handler);
 
        }
 
     
        @Override
        public void onChange(boolean selfChange) {
 
 Cursor cursor = MainActivity.this.getContentResolver().query(
Uri.parse("content://sms/inbox"), null, null, null, null);
 
            while (cursor.moveToNext()) {
                StringBuilder sb = new StringBuilder();
 
                sb.append("address=").append(
                        cursor.getString(cursor.getColumnIndex("address")));
 
                sb.append(";subject=").append(
                        cursor.getString(cursor.getColumnIndex("subject")));
 
                sb.append(";body=").append(
                        cursor.getString(cursor.getColumnIndex("body")));
 
                sb.append(";time=").append(
                        cursor.getLong(cursor.getColumnIndex("date")));
 
                System.out.println("--------has Receivered SMS::" + sb.toString());
 
                 
            }
 
        }
 
    }
}
```

同时可以在ContentProvider发生数据变化时调用 getContentResolver().notifyChange(uri, null)来通知注册在此URI上的访问者。

　　

```
public class UserContentProvider extends ContentProvider {
   public Uri insert(Uri uri, ContentValues values) {
      db.insert("user", "userid", values);
      getContext().getContentResolver().notifyChange(uri, null);
   }
}
```

##### [6] 实例说明

　　数据源是SQLite, 用ContentResolver操作ContentProvider。

![img](https://camo.githubusercontent.com/1302cfe3a60f9edf38daa5202d006ea98ae7d9af/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630353035313935313433303939)

Constant.java（储存一些常量）

```
public class Constant {  
      
    public static final String TABLE_NAME = "user";  
      
    public static final String COLUMN_ID = "_id";  
    public static final String COLUMN_NAME = "name";  
       
       
    public static final String AUTOHORITY = "cn.scu.myprovider";  
    public static final int ITEM = 1;  
    public static final int ITEM_ID = 2;  
       
    public static final String CONTENT_TYPE = "vnd.android.cursor.dir/user";  
    public static final String CONTENT_ITEM_TYPE = "vnd.android.cursor.item/user";  
       
    public static final Uri CONTENT_URI = Uri.parse("content://" + AUTOHORITY + "/user");  
}  
```

DBHelper.java(操作数据库)

```
public class DBHelper extends SQLiteOpenHelper {  
  
    private static final String DATABASE_NAME = "finch.db";    
    private static final int DATABASE_VERSION = 1;    
  
    public DBHelper(Context context) {  
        super(context, DATABASE_NAME, null, DATABASE_VERSION);  
    }  
  
    @Override  
    public void onCreate(SQLiteDatabase db)  throws SQLException {  
        //创建表格  
        db.execSQL("CREATE TABLE IF NOT EXISTS "+ Constant.TABLE_NAME + "("+ Constant.COLUMN_ID +" INTEGER PRIMARY KEY AUTOINCREMENT," + Constant.COLUMN_NAME +" VARCHAR NOT NULL);");  
    }  
  
    @Override  
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion)  throws SQLException {  
        //删除并创建表格  
        db.execSQL("DROP TABLE IF EXISTS "+ Constant.TABLE_NAME+";");  
        onCreate(db);  
    }  
}  
```

　MyProvider.java(自定义的ContentProvider)　

```
public class MyProvider extends ContentProvider {    
    
    DBHelper mDbHelper = null;    
    SQLiteDatabase db = null;    
    
    private static final UriMatcher mMatcher;    
    static{    
        mMatcher = new UriMatcher(UriMatcher.NO_MATCH);    
        mMatcher.addURI(Constant.AUTOHORITY,Constant.TABLE_NAME, Constant.ITEM);    
        mMatcher.addURI(Constant.AUTOHORITY, Constant.TABLE_NAME+"/#", Constant.ITEM_ID);    
    }    
    
  
    @Override    
    public String getType(Uri uri) {    
        switch (mMatcher.match(uri)) {    
        case Constant.ITEM:    
            return Constant.CONTENT_TYPE;    
        case Constant.ITEM_ID:    
            return Constant.CONTENT_ITEM_TYPE;    
        default:    
            throw new IllegalArgumentException("Unknown URI"+uri);    
        }    
    }    
    
    @Override    
    public Uri insert(Uri uri, ContentValues values) {    
        // TODO Auto-generated method stub    
        long rowId;    
        if(mMatcher.match(uri)!=Constant.ITEM){    
            throw new IllegalArgumentException("Unknown URI"+uri);    
        }    
        rowId = db.insert(Constant.TABLE_NAME,null,values);    
        if(rowId>0){    
            Uri noteUri=ContentUris.withAppendedId(Constant.CONTENT_URI, rowId);    
            getContext().getContentResolver().notifyChange(noteUri, null);    
            return noteUri;    
        }    
    
        throw new SQLException("Failed to insert row into " + uri);    
    }    
    
    @Override    
    public boolean onCreate() {    
        // TODO Auto-generated method stub    
        mDbHelper = new DBHelper(getContext());    
    
        db = mDbHelper.getReadableDatabase();    
    
        return true;    
    }    
    
    @Override    
    public Cursor query(Uri uri, String[] projection, String selection,    
            String[] selectionArgs, String sortOrder) {    
        // TODO Auto-generated method stub    
        Cursor c = null;    
        switch (mMatcher.match(uri)) {    
        case Constant.ITEM:    
            c =  db.query(Constant.TABLE_NAME, projection, selection, selectionArgs, null, null, sortOrder);    
            break;    
        case Constant.ITEM_ID:    
            c = db.query(Constant.TABLE_NAME, projection,Constant.COLUMN_ID + "="+uri.getLastPathSegment(), selectionArgs, null, null, sortOrder);    
            break;    
        default:    
            throw new IllegalArgumentException("Unknown URI"+uri);    
        }    
    
        c.setNotificationUri(getContext().getContentResolver(), uri);    
        return c;    
    }    
    
    @Override    
    public int update(Uri uri, ContentValues values, String selection,    
            String[] selectionArgs) {    
        // TODO Auto-generated method stub    
        return 0;    
    }

	@Override
	public int delete(Uri uri, String selection, String[] selectionArgs) {
		// TODO Auto-generated method stub
		return 0;
	}    
    
}    
```

MainActivity.java(ContentResolver操作)

```
public class MainActivity extends Activity {
    private ContentResolver mContentResolver = null; 
    private Cursor cursor = null;  
         @Override
        protected void onCreate(Bundle savedInstanceState) {
        	// TODO Auto-generated method stub
        	super.onCreate(savedInstanceState);
        	setContentView(R.layout.activity_main);
        	
        	   TextView tv = (TextView) findViewById(R.id.tv);
				
        		mContentResolver = getContentResolver();  
        		tv.setText("添加初始数据 ");
                for (int i = 0; i < 10; i++) {  
                    ContentValues values = new ContentValues();  
                    values.put(Constant.COLUMN_NAME, "fanrunqi"+i);  
                    mContentResolver.insert(Constant.CONTENT_URI, values);  
                } 
                
            	tv.setText("查询数据 ");
                cursor = mContentResolver.query(Constant.CONTENT_URI, new String[]{Constant.COLUMN_ID,Constant.COLUMN_NAME}, null, null, null);  
                if (cursor.moveToFirst()) {
                	String s = cursor.getString(cursor.getColumnIndex(Constant.COLUMN_NAME));
                	tv.setText("第一个数据： "+s);
                }
        }
         
}  
```

最后在manifest申明

```
<provider android:name="MyProvider" android:authorities="cn.scu.myprovider" />
```

## 【BroadcastReceiver专题】

##### [1] BroadcastReceiver的定义

广播是一种广泛运用的在应用程序之间传输信息的机制，主要用来监听系统或者应用发出的广播信息，然后根据广播信息作为相应的逻辑处理，也可以用来传输少量、频率低的数据。

在实现开机启动服务和网络状态改变、电量变化、短信和来电时通过接收系统的广播让应用程序作出相应的处理。

BroadcastReceiver **自身并不实现图形用户界面**，但是当它收到某个通知后， BroadcastReceiver 可以通过启动 Service 、启动 Activity 或是 NotificationMananger 提醒用户。

##### [2] BroadcastReceiver使用注意

　　当系统或应用发出广播时，将会扫描系统中的所有广播接收者，通过action匹配将广播发送给相应的接收者，接收者收到广播后将会产生一个广播接收者的实例，执行其中的onReceiver()这个方法；特别需要注意的是这个实例的生命周期只有10秒，如果10秒内没执行结束onReceiver()，系统将会报错。

在onReceiver()执行完毕之后，该实例将会被销毁，所以不要在onReceiver()中执行耗时操作，也不要在里面创建子线程处理业务（因为可能子线程没处理完，接收者就被回收了，那么子线程也会跟着被回收掉）；正确的处理方法就是通过in调用activity或者service处理业务。

##### [3] BroadcastReceiver的注册

　　BroadcastReceiver的注册方式有且只有两种，一种是**静态注册**（推荐使用），另外一种是**动态注册**，广播接收者在注册后就开始监听系统或者应用之间发送的广播消息。

**接收短信广播示例**：

定义自己的BroadcastReceiver 类

```
public class MyBroadcastReceiver extends BroadcastReceiver {
 
// action 名称
String SMS_RECEIVED = "android.provider.Telephony.SMS_RECEIVED" ;
 
    public void onReceive(Context context, Intent intent) {
 
       if (intent.getAction().equals( SMS_RECEIVED )) {
           // 一个receiver可以接收多个action的，即可以有多个intent-filter，需要在onReceive里面对intent.getAction(action name)进行判断。
       }
    }
}
```

**静态方式**

　　在AndroidManifest.xml的application里面定义receiver并设置要接收的action。

```
< receiver android:name = ".MyBroadcastReceiver" > 

 < intent-filter android:priority = "777" >             
<action android:name = "android.provider.Telephony.SMS_RECEIVED" />
</ intent-filter > 

</ receiver >
```

　　这里的priority取值是-1000到1000，值越大优先级越高，同时注意加上系统接收短信的限权。

```
< uses-permission android:name ="android.permission.RECEIVE_SMS" />
```

　　静态注册的广播接收者是一个常驻在系统中的全局监听器，当你在应用中配置了一个静态的BroadcastReceiver，安装了应用后而无论应用是否处于运行状态，广播接收者都是已经常驻在系统中了。同时应用里的所有receiver都在清单文件里面，方便查看。要销毁掉静态注册的广播接收者，可以通过调用PackageManager将Receiver禁用。

**动态方式**

　　在Activity中声明BroadcastReceiver的扩展对象，在onResume中注册，onPause中卸载. 　　　

```
public class MainActivity extends Activity {
	MyBroadcastReceiver receiver;
	@Override
	 protected void onResume() {
		// 动态注册广播 (代码执行到这才会开始监听广播消息，并对广播消息作为相应的处理)
		receiver = new MyBroadcastReceiver();
		IntentFilter intentFilter = new IntentFilter( "android.provider.Telephony.SMS_RECEIVED" );
		registerReceiver( receiver , intentFilter);	
		super.onResume();
	}
	@Override
	protected void onPause() {  
		// 撤销注册 (撤销注册后广播接收者将不会再监听系统的广播消息)
		unregisterReceiver(receiver);
		super.onPause();
	}
}
```

**静态注册和动态注册的区别**

　　1、静态注册的广播接收者一经安装就常驻在系统之中，不需要重新启动唤醒接收者；动态注册的广播接收者随着应用的生命周期，由registerReceiver开始监听，由unregisterReceiver撤销监听，如果应用退出后，没有撤销已经注册的接收者应用应用将会报错。

　　2、当广播接收者通过intent启动一个activity或者service时，如果intent中无法匹配到相应的组件。动态注册的广播接收者将会导致应用报错 而静态注册的广播接收者将不会有任何报错，因为自从应用安装完成后，广播接收者跟应用已经脱离了关系。　

##### [4] 发送BroadcastReceiver

**发送广播主要有两种类型：**

**普通广播**：应用在需要通知各个广播接收者的情况下使用，如开机启动

使用方法：sendBroadcast()

```
Intent intent = new Intent("android.provider.Telephony.SMS_RECEIVED"); 
//通过intent传递少量数据
intent.putExtra("data", "finch"); 
// 发送普通广播
sendBroadcast(Intent); 
```

　　普通广播是完全异步的，可以在同一时刻（逻辑上）被所有接收者接收到，所有满足条件的BroadcastReceiver 都会随机地执行其 onReceive() 方法。

 　　同级别接收是先后是随机的；级别低的收到广播；

 　　消息传递的效率比较高，并且无法中断广播的传播。

**有序广播**：应用在需要有特定拦截的场景下使用，如黑名单短信、电话拦截。　

使用方法：

　`sendOrderedBroadcast(intent, receiverPermission);`

　`receiverPermission` ：一个接收器必须持以接收您的广播。如果为 null ，不经许可的要求（一般都为null）。

```
//发送有序广播
 sendOrderedBroadcast(intent, null);
```

　　在有序广播中，我们可以在前一个广播接收者将处理好的数据传送给后面的广播接收者，也可以调用abortBroadcast()来终结广播的传播。

```
public void onReceive(Context arg0, Intent intent) {
　　//获取上一个广播的bundle数据
　　Bundle bundle = getResultExtras(true);//true：前一个广播没有结果时创建新的Bundle；false：不创建Bundle
　　bundle.putString("key", "777");
　　//将bundle数据放入广播中传给下一个广播接收者
　　setResultExtras(bundle);　
　　
　　//终止广播传给下一个广播接收者
　　abortBroadcast();
}
```

　　高级别的广播收到该广播后，可以决定把该广播是否截断掉。同级别接收是先后是随机的，如果先接收到的把广播截断了，同级别的例外的接收者是无法收到该广播。 　　

异步广播

使用方法：`sendStickyBroadcast()` ：

　　发出的Intent当接收Activity（动态注册）重新处于onResume状态之后就能重新接受到其Intent.（the Intent will be held to be re-broadcast to future receivers）。就是说sendStickyBroadcast发出的最后一个Intent会被保留，下次当Activity处于活跃的时候又会接受到它。

发这个广播需要权限：

```
<uses-permission android:name="android.permission.BROADCAST_STICKY" />
```

卸载该广播：

```
removeStickyBroadcast(intent);
```

　　在卸载之前该intent会保留，接收者在可接收状态都能获得。

**异步有序广播**

　　使用方法：`sendStickyOrderedBroadcast(intent, resultReceiver, scheduler, initialCode, initialData, initialExtras)`：

　　这个方法具有有序广播的特性也有异步广播的特性； 　　同时需要限权：

```
 <uses-permission android:name="android.permission.BROADCAST_STICKY" /> 
```

##### [5] 总结

- 静态广播接收的处理器是由PackageManagerService负责，当手机启动或者新安装了应用的时候，PackageManagerService会扫描手机中所有已安装的APP应用，将AndroidManifest.xml中有关注册广播的信息解析出来，存储至一个全局静态变量当中。
- 动态广播接收的处理器是由ActivityManagerService负责，当APP的服务或者进程起来之后，执行了注册广播接收的代码逻辑，即进行加载，最后会存储在一个另外的全局静态变量中。需要注意的是：

　　 1、 这个并非是一成不变的，当程序被杀死之后，已注册的动态广播接收器也会被移出全局变量，直到下次程序启动，再进行动态广播的注册，当然这里面的顺序也已经变更了一次。

　　 2、这里也并没完整的进行广播的排序，只记录的注册的先后顺序，并未有结合优先级的处理。

- 广播发出的时候，广播接收者接收的顺序如下：

　　１．当广播为**普通广播**时，有如下的接收顺序：

无视优先级

动态优先于静态 

同优先级的动态广播接收器，**先注册的大于后注册的**

同优先级的静态广播接收器，**先扫描的大于后扫描的**　

　　２．如果广播为**有序广播**，那么会将动态广播处理器和静态广播处理器合并在一起处理广播的消息，最终确定广播接收的顺序：

优先级高的先接收　 　　

同优先级的动静态广播接收器，**动态优先于静态** 　　

同优先级的动态广播接收器，**先注册的大于后注册的** 　　

同优先级的静态广播接收器，**先扫描的大于后扫描的**　

##### [6]一些常用的系统广播的action 和permission

- 开机启动

```
<action android:name="android.intent.action.BOOT_COMPLETED"/> 
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />  
```

- 网络状态

```
<action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>  
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> 
```

　　　网络是否可用的方法：

```
  public static boolean isNetworkAvailable(Context context) {  
        ConnectivityManager mgr = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);  
        NetworkInfo[] info = mgr.getAllNetworkInfo();  
        if (info != null) {  
            for (int i = 0; i < info.length; i++) {  
      if (info[i].getState() == NetworkInfo.State.CONNECTED) {  
                    return true;  
                }  
            }  
        }  
        return false;  
    } 
```

- 电量变化

```
<action android:name="android.intent.action.BATTERY_CHANGED"/>  
```

BroadcastReceiver 的onReceive方法：

```
public void onReceive(Context context, Intent intent) {  
        int currLevel = intent.getIntExtra(BatteryManager.EXTRA_LEVEL, 0);  //当前电量  　
        
        int total = intent.getIntExtra(BatteryManager.EXTRA_SCALE, 1);    //总电量  
        int percent = currLevel * 100 / total;  
        Log.i(TAG, "battery: " + percent + "%");  
    }  
```

## 【安卓面试题总结专题】

https://www.jianshu.com/p/46774f2f51b1

#### 1.内存泄露总结

> 当某些对象不再被程序所使用，但是这些对象仍然被某些对象所引用着，进而导致垃圾收集器不能及时释放它们。很多情况下是长生命周期引用着短生命周期的对象（而且对象比较大）不释放。
>
> **造成内存泄露的原因有：**
>
> 1.**静态集合类引起的内存泄露**
>
> 像HashMap、Vector等的使用最容易出现内存泄露，这些静态变量的生命周期和应用程序一致，他们所引用的所有的对象Object也不能被释放，因为他们也将一直被Vector等引用着。
>
> 2.当集合里面的对象属性被修改后，再调用remove()方法时不起作用。
>
> 3.释放对象的时候没有删除监听器
>
> 4.没有关闭连接，例如数据库连接（dataSourse.getConnection()），网络连接(socket)和io连接
>
> 5.**内部类和外部模块的引用**
>
> 6.**单例模式**，不正确使用单例模式是引起内存泄漏的一个常见问题，单例对象在初始化后将在JVM的整个生命周期中存在（以静态变量的方式），如果单例对象持有外部的引用，那么这个对象将不能被JVM正常回收，导致内存泄漏。
>
> 7.**Handler 造成的内存泄漏**（由于Handler是非静态内部类所以其持有当前Activity的隐式引用，如果Handler没有被释放，其所持有的外部引用也就是Activity也不可能被释放）

#### 2.内存溢出（OOM）

> 避免OOM有以下几种方向：
>
> **防止内存泄露**
>
> 避免OOM就是要剩余足够堆内存供应用使用，要想内存足够呢，首先就需要避免应用存在内存泄漏的情况，内存泄漏后，可使用的内存空间减少，自然就会更容易产生OOM。
>
> **减小对象的内存占用**
>
> 1.使用更加轻量的数据结构，例如，可以考虑使用ArrayMap/SparseArray而不是HashMap等传统数据结构
>
> 2.减小Bitmap对象的内存占用
>
> **内存对象的重复利用**
>
> 1.复用系统自带的资源
>
> 2.注意在ListView/GridView等出现大量重复子组件的视图里对ConvertView的复用
>
> 3.Bitmap对象的复用
>
> 4.代码中会需要使用到大量的字符串拼接的操作，这种时候有必要考虑使用StringBuilder来替代频繁的“+”

#### 3..避免加载图片导致OOM

> **1. 压缩图片**
>
> 在展示高分辨率图片的时候，最好先将图片进行压缩。压缩后的图片大小应该和用来展示它的控件大小相近，在一个很小的ImageView上显示一张超大的图片不会带来任何视觉上的好处，但却会占用我们相当多宝贵的内存，而且在性能上还可能会带来负面影响。
>
> **2. 使用图片缓存技术**
>
> 内存缓存技术对那些大量占用应用程序宝贵内存的图片提供了快速访问的方法。其中最核心的类是**LruCache** (此类在android-support-v4的包中提供) 。这个类非常适合用来缓存图片，它的主要算法原理是把最近使用的对象用强引用存储在 LinkedHashMap 中，并且把最近最少使用的对象在缓存值达到预设定值之前从内存中移除。
>
> **3. 及时回收bitmap内存**
>
> 虽然android系统有自己的gc机制，但是bitmap分为java和C两部分，这个bitmap对象是由java部分分配的，不用的时候系统就会自动回收了，但是那个对应的C可用的内存区域，虚拟机时不能直接回收的，这个只能调用底层的功能释放，所以需要调用recycle()方法来释放C部分内存。
>
> **4. 捕获异常**
>
> 因为bitmap是吃内存大户，为了避免应用在分配bitmap内存的时候出现OutOfMemory异常以后Crash掉，对异常进行捕获，如果发生了OOM后，应用不会崩溃，而是得到一个默认的bitmap图。

#### 4.ANR异常总结：

> **1、ANR错误一般有三种类型**
>
>    1.KeyDispatchTimeout(5 seconds) --主要是类型按键或触摸事件在特定时间内（5s）无响应
>
>    2.BroadcastTimeout(10 seconds) --BroadcastReceiver在特定时间内（10s）无法处理完成
>
>    3.ServiceTimeout(20 secends) --小概率事件 Service在特定的时间内无法处理完成
>
> **2、哪些操作会导致ANR 在主线程执行以下操作：**
>
>    1.高耗时的操作，如图像变换
>
>    2.磁盘读写，数据库读写操作
>
>    3.大量的创建新对象
>
> **3、如何避免**
>
>    1.UI线程尽量只做跟UI相关的工作
>
>    2.耗时的操作(比如数据库操作，I/O，连接网络或者别的有可能阻塞UI线程的操作)把它放在单独的线程处理
>
>    3.尽量用Handler来处理UIThread和别的Thread之间的交互

#### 5.Binder机制

> ​    **Binder是一种Android实现跨进程通信（IPC）的方式。**在一个进程空间中，分为用户空间和内核空间：进程间，用户空间的数据不可共享，内核空间的数据可以共享，为了保证安全性和独立性，一个进程不能直接访问另一个进程，而Binder就是充当连接两个进程（内核空间）的通道。Binder跨进程机制模型基于Client-Server模式。**Binder框架定义了四个角色：Server,Client,ServiceManager以及Binder驱动**：
>
> >**Client/Server结构bai(C/S结构)是大家熟知的客户机和服务器结构**。它是软件du系统体系结构，zhi通过它可以充分利用两端dao硬件环境的优势，将任务合理分配到Client端和Server端来实现，降低了系统的通讯开销。
> >
> >目前大多数应用软件系统都是Client/Server形式的两层结构，由于现在的软件应用系统正在向分布式的Web应用发展，Web和Client/Server 应用都可以进行同样的业务处理，应用不同的模块共享逻辑组件；
> >
> >因此，内部的和外部的用户都可以访问新的和现有的应用系统，通过现有应用系统中的逻辑可以扩展出新的应用系统。这也就是目前应用系统的发展方向。
>
>    **Server：**提供服务的进程
>
>    **Client：**使用服务的进程
>
>    **ServiceManager：**管理Service注册与查询
>
>    **Binder驱动：**一种虚拟设备驱动，是连接Server进程、Client进程和ServiceManager的桥梁，具  体作用为：1.传递进程间的数据2.实现线程控制
>
> ​    Binder驱动和Service Manager进程 属于 Android基础架构（即系统已经实现好了）；而Client 进程 和 Server 进程 属于Android应用层（需要开发者自己实现），所以，在进行跨进程通信时，开发者只需自定义Client & Server 进程 并 显式使用3个步骤（1.注册服务，获取服务，使用服务），最终借助 Android的基本架构功能就可完成进程间通信。
>
> **Binder的优点：**
>
> 对比 Linux （Android基于Linux）上的其他进程通信方式（管道/消息队列/共享内存/信号量/Socket），Binder 机制的优点有：
>
> **高效**
>
> 1.Binder数据拷贝只需要一次，而管道、消息队列、Socket都需要2次
>
> 2.通过驱动在内核空间拷贝数据，不需要额外的同步处理
>
> **安全性高**
>
> Binder 机制为每个进程分配了 UID/PID 来作为鉴别身份的标示，并且在 Binder 通信时会根据 UID/PID 进行有效性检测
>
> 1.传统的进程通信方式对于通信双方的身份并没有做出严格的验证
>
> 2.如，Socket通信 ip地址是客户端手动填入，容易出现伪造
>
> **使用简单**
>
> 1.采用Client/Server 架构
>
> 2.实现 面向对象 的调用方式，即在使用Binder时就和调用一个本地对象实例一样
>
> Binder请求的线程管理
>
> Server进程会创建很多线程来处理Binder请求，管理Binder模型的线程是采用Binder驱动的线程池，并由Binder驱动自身进行管理，而不是由Server进程来管理的。一个进程的Binder线程数默认最大是16，超过的请求会被阻塞等待空闲的Binder线程。所以，在进程间通信时处理并发问题时，如使用ContentProvider时，它的CRUD（创建、检索、更新和删除）方法只能同时有16个线程同时工作。

#### 6.AIDL

> ​    **AIDL（Android Interface Definition Language,AIDL）是Android的一种接口描述语言**;编译器可以通过aidl文件生成一段代码，通过预先定义的接口达到两个进程内部通信进程的目的（对于小白来说，AIDL的作用是让你可以在自己的APP里绑定一个其他APP的service，这样你的APP可以和其他APP交互）。
>
> **创建AIDL的步骤：**
>
> 1.创建一个aidl文件
>
> 2.在aidl文件中定义一个我们要提供的接口
>
> 3.新建一个service，在service里面建一个内部类，继承刚才创建的AIDL的stub类，并实现接口的方法，在onbind方法中返回内部类的实例。
>
> **使用AIDL的步骤：**
>
> 1.将aidl文件拷贝到src目录下，同时注意添加到的包名要求跟原来工程的包名严格一致
>
> 2.通过隐式意图绑定service
>
> 3.在onServiceConnected方法中通过Interface.stub.asinterface(service)获取Interface对象
>
> 4.通过interface对象调用方法
>
>    AIDL其实就是通过Binder实现的，因为在我们定义好aidl文件后，studio就帮我们生成了相关的Binder类。事实上我们在使用AIDL时候继承的Stub类，就是studio帮我们生成的Binder类。

#### 7.Handler

>   Handler是线程通信机制，Handler相关的有四个类：
>
>   **Message：**消息分为硬件产生的消息(如按钮、触摸)和软件生成的消息；
>
>   **MessageQueue：**消息队列的主要功能向消息池投递消息(MessageQueue.enqueueMessage)和取走消息池的消息(MessageQueue.next)；
>
>   **Handler：**消息辅助类，主要功能向消息池发送各种消息事件(Handler.sendMessage)和处理相应消息事件(Handler.handleMessage)；
>
>    **Looper：**不断循环执行(Looper.loop)，按分发机制将消息分发给目标处理者。
>
>   在主线程使用handler很简单，只需在主线程创建一个handler对象，重写handlerMessage()方法，在子线程通过在主线程创建的handler对象发送Message，在handleMessage（）方法中接受这个Message对象进行处理。通过handler很容易的从子线程切换回主线程了。当我们在子线程使用Handler的时候要手动调用Looper.prepare()创建一个Looper对象，之所以主线程不用，是系统启动的时候帮我们自动调用了Looper.prepare()方法。
>
>   **在同一线程中android.Handler和android.MessaegQueue的数量对应关系是怎样的？**
>
>   N(Handler)：1(MessageQueue)
>
>   在同一线程中肯定会调用一个 Loop.prepare() ，其中就生成一个 MessageQueue .而代码中可以 new 出多个 Handler 发送各自的 Message 到这个 MessageQueue 中，最后调用msg.target.dispatch 中这个target来捕获自己发送的massge，所以明显是 N 个 Handler 对应一个 MessageQueue。

#### 8.Async(A森克)Task

> AsyncTask是Android提供的一个助手类，它对Thread和Handler进行了封装，方便我们使用。在使用AsyncTask时，我们无需关注Thread和Handler，AsyncTask内部会对其进行管理。
>
> **AsyncTask有四个重要的回调方法，分别是：onPreExecute、doInBackground、onProgressUpdate和onPostExecute。**这四个方法会在AsyncTask的不同时期进行自动调用，我们只需要实现这几个方法的内部逻辑即可。
>
> **onPreExecute:**该方法是运行在主线程中的。在AsyncTask执行了execute（）方法后就会在UI线程上执行该方法，
>
> 该方法在task正真执行前运行，我们通常可以在该方法中显示一个进度条，从而告知用户后台任务即将开始。
>
> **doInBackground：**该方法是运行在单独的工作线程中的，。该方法会在onPreExecute()方法执行完成后立即执行，
>
> 该方法用于在工作线程中执行耗时操作，我们在该方法中编写我们需要在后台线程中运行的逻辑代码。
>
> **onProgressUpdate：**该方法是在主线程中被调用，当我们在doInBackground中调用publishProgress（）方法后，就会在UI线程上回调该方法。
>
> **onPostExecute：**该方法是在主线程中被调用。当doInBackground方法执行完毕后，就表示任务完成了，doInBackground方法的返回值
>
> 就会作为参数在主线程中传入到onPostExecute方法中，这样就可以在主线程中根据任务的执行结果更新UI。

#### 9.IntentService

> ​    IntentService是继承并处理异步请求的一个类，在IntentService内有一个工作线程来处理耗时操作，启动IntentService的方式和启动传统的Service一样，同时，当任务执行完后，IntentService会自动停止，而不需要我们手动去控制或stopSelf()。
>
> ​    我们使用IntentService最起码有两个好处：一方面不需要自己去new Thread了；另一方面不需要考虑在什么时候关闭该Service。

#### 10.Android dvm的进程和Linux的进程, 应用程序的进程是否为同一个概念 

> DVM指dalivk的虚拟机。每一个Android应用程序都在它自己的进程中运行，都拥有一个独立的Dalvik虚拟机实例。而每一个DVM都是在Linux 中的一个进程，所以说可以认为是同一个概念。

#### 11.Android的几种进程

> **1.前台进程：**即与用户正在交互的Activity或者Activity用到的Service等，如果系统内存不足时前台进程是最后被杀死的
>
> **2.可见进程：**可以是处于暂停状态(onPause)的Activity或者绑定在其上的Service，即被用户可见，但由于失去了焦点而不能与用户交互
>
> **3.服务进程：**其中运行着使用startService方法启动的Service，虽然不被用户可见，但是却是用户关心的，例如用户正在非音乐界面听的音乐或者正在非下载页面自己下载的文件等；当系统要空间运行前两者进程时才会被终止
>
> **4.后台进程：**其中运行着执行onStop方法而停止的程序，但是却不是用户当前关心的，例如后台挂着的QQ，这样的进程系统一旦没了有内存就首先被杀死
>
> **5.空进程：**不包含任何应用程序的程序组件的进程，这样的进程系统是一般不会让他存在的
>
> **如何避免后台进程被杀死：**
>
> 1.调用startForegound，让你的Service所在的线程成为前台进程
>
> 2.Service的onStartCommond返回START_STICKY或START_REDELIVER_INTENT
>
> 3.Service的onDestroy里面重新启动自己

#### 12.为什么使用服务而不是线程  

>    进程中运行着线程，Android应用程序刚启动都会开启一个进程给这个程序来使用。Android一个应用程序把所有的界面关闭时, 进程这时还没有被销毁,现在处于的是空进程状态,Thread运行在空进程中, 很容易的被销毁了。服务不容易被销毁, 如果非法状态下被销毁了, 系统会在内存够用时,重新启动。
>
>   Android系统会尽量保持拥有service的进程运行，只要在该service已经被启动(start)或者客户端连接(bindService)到它。当内存不足时，还会保持，拥有service的进程具有较高的优先级。

#### 13.线程安全问题

>    当多个线程同时访问临界资源（一个对象，对象中的属性，一个文件，一个数据库等）时，就可能会产生线程安全问题。基本上所有的并发模式在解决线程安全问题上，都采用“序列化访问临界资源”的方案，即在同一时刻，只能有一个线程访问临界资源，也称同步互斥访问。通常来说，是在访问临界资源的代码前面加上一个锁，当访问完临界资源后释放锁，让其他线程继续访问。
>
>    在Java中，提供了两种方式来实现同步互斥访问：**synchronized和Lock**。
>
>    所谓死锁，就是两个线程都在等待对方先完成，造成程序的停滞，一般程序的死锁都是在程序运行时出现的。

#### 14.线程的状态变化

>  要想实现多线程，必须在主线程中创建新的线程对象。任何线程一般具有5种状态，即创建，就绪，运行，阻塞，终止。下面分别介绍一下这几种状态：
>
> **创建状态**
>
> 在程序中用构造方法创建了一个线程对象后，新的线程对象便处于新建状态，此时它已经有了相应的内存空间和其他资源，但还处于不可运行状态。新建一个线程对象可采用Thread 类的构造方法来实现，例如 “Thread thread=new Thread()”。
>
> **就绪状态**
>
> 新建线程对象后，调用该线程的 start() 方法就可以启动线程。当线程启动时，线程进入就绪状态。此时，线程将进入线程队列排队，等待 CPU 服务，这表明它已经具备了运行条件。
>
> **运行状态**
>
> 当就绪状态被调用并获得处理器资源时，线程就进入了运行状态。此时，自动调用该线程对象的 run() 方法。run() 方法定义该线程的操作和功能。
>
> **阻塞状态**
>
> 一个正在执行的线程在某些特殊情况下，如被人为挂起或需要执行耗时的输入/输出操作，会让 CPU 暂时中止自己的执行，进入阻塞状态。在可执行状态下，如果调用sleep(),suspend(),wait() 等方法，线程都将进入阻塞状态，发生阻塞时线程不能进入排队队列，只有当引起阻塞的原因被消除后，线程才可以转入就绪状态。
>
> **死亡状态**
>
> 线程调用 stop() 方法时或 run() 方法执行结束后，即处于死亡状态。处于死亡状态的线程不具有继续运行的能力。

#### 15.Android架构



![img](https:////upload-images.jianshu.io/upload_images/9087029-c0662f8aa3987a04.png?imageMogr2/auto-orient/strip|imageView2/2/w/465/format/webp)

> **1.Linux内核(Linux Kernel)**底层Linux核心的工作,安全管理、内存管理、进程管理、电源管理、硬件驱动
>
> **2.核心类库(Libraries)**
>
> 核心类库中包含了系统库及Android运行环境。系统库这一层主要是通过C/C++库来为Android系统提供主要的特性支持。
>
> Libraries：c代码库
>
>   OpenGL：图形快速显示，游戏开发
>
>    webkit：浏览器内核
>
>    Android Runtime
>
>   Dalvik VM：虚拟机，android代码运行在此虚拟机
>
>   运行时调用Libraries C代码库
>
> **3.应用程序层(Application Framework)**
>
> Application Framework中间层，java代码，调用底层c代码
>
> **4.应用层**
>
> Applications原生的应用程序：浏览器、桌面、联系人等
>
> **相比以前的架构，多了一个HAL（硬件抽象层）**

#### 16.Android四大布局

> ​    Android常见的四大布局为线性布局（LinearLayout）、相对布局（Relativelayout）、帧布局（FrameLayout）、表格布局（TableLayout）。有的地方介绍是五大布局，因为还有一种是绝对布局（AbsoluteLayout）就是通过坐标的宽高来控制控件的位置，此布局方式已经被弃用。
>
>  **FrameLayout(帧布局)：**
>
> 显示特点：所有的子控件默认显示在FrameLayout的左上角，会重叠在一起显示。
>
> **LinearLayout(线性布局)：**
>
> 显示特点：每一个LinearLayout里面又可分为垂直布局（android:orientation="vertical"）和水平布局（android:orientation="horizontal" ）android:orientation="horizontal"(横向)。
>
> **RelativeLayout(相对布局):**
>
> 显示特点：和LinearLayout布局相似，所有子控件默认显示在RelativeLayout的左上角，主要属性有：相对于某一个元素android:layout_below android:layout_toLeftOf相对于父元素的地方android:layout_alignParentLeft、android:layout_alignParentRigh
>
> **TableLayout(表格布局):**
>
> 在表格布局中，整个页面就相当于一张大的表格，控件就放在每个Cell中

#### 17.四大存储方式

> 在Android系统中我们常用的数据存储方式有4种。1、**存储手机内存中（ROM）**2、**存储在SD卡中**3、**存储在SharedPreferences中**4、**存储在SQLite数据库中**（ContentProvider存储数据属于程序间数据库共享）
>
> 所有的文件都是默认存储到/data/data//files目录下的
>
> sharedpreferences文件都是存放在/data/data//shared_prefs/目录下的
>
> 获得sharedpreferences的3种方法：1.context类中的getsharedpreferences（）方法2.Activity类中的getpreferences（）方法，使用这个方法时自动将当前活动的类名作为sharedpreferences的文件名3.PreferenceManager类中的getDefaultSharedPreferences（）方法，自动使用当前应用程序的包名作为前缀来命名sharedpreferences文件。
>
>  **如何将SQLite数据库(dictionary.db文件)与apk文件一起发布**
>
> 可以将dictionary.db文件复制到Eclipse Android工程中的res aw目录中。所有在res aw目录中的文件不会被压缩，这样可以直接提取该目录中的文件。可以将dictionary.db文件复制到res aw目录中
>
>  **如何将打开res aw目录中的数据库文件?**
>
> 在Android中不能直接打开res aw目录中的数据库文件，而需要在程序第一次启动时将该文件复制到手机内存或SD卡的某个目录中，然后再打开该数据库文件。
>
> 复制的基本方法是使用getResources().openRawResource方法获得res aw目录中资源的 InputStream对象，然后将该InputStream对象中的数据写入其他的目录中相应文件中。在Android SDK中可以使用SQLiteDatabase.openOrCreateDatabase方法来打开任意目录中的SQLite数据库文件。

#### 18.Activity三种状态七个生命周期

> 1、当它在屏幕前台时,响应用户操作的Activity, 它是激活或运行状态
>
> 2、当它上面有另外一个Activity，使它失去了焦点但仍然对用户可见时,它处于暂停状态。
>
> 3、当它完全被另一个Activity覆盖时则处于停止状态。
>
> void onCreate() 设置布局以及进行初始化操作
>
> void onStart() 可见, 但不可交互
>
> void onRestart() 调用onStart()
>
> void onResume() 可见, 可交互
>
> void onPause() 部分可见, 不可交互
>
> void onStop() 完全不可见
>
> void onDestroy() 销毁

#### 19. Activity在屏幕旋转时的生命周期

> ​    不设置Activity的android:configChanges时，切屏会重新调用各个生命周期，切横屏时会执行一次，切竖屏时会执行两次；设置Activity的android:configChanges="orientation"时，切屏还是会重新调用各个生命周期，切横、竖屏时只会执行一次；设置Activity的android:configChanges="orientation|keyboardHidden"时，切屏不会重新调用各个生命周期，只会执行onConfigurationChanged方法。

#### 20.任务栈

> (1) 程序打开时就创建了一个任务栈,用于存储当前程序的activity,所有的activity属于一个任务栈。
>
> (2) 一个任务栈包含了一个activity的集合,去有序的选择哪一个activity和用户进行交互:只有在任务栈栈顶的activity才可以跟用户进行交互。
>
> (3) 任务栈可以移动到后台, 并且保留了每一个activity的状态.并且有序的给用户列出它们的任务, 而且还不丢失它们状态信息。
>
> (4) 退出应用程序时：当把所有的任务栈中所有的activity清除出栈时,任务栈会被销毁,程序退出。
>
> 任务栈的缺点：
>
> (1) 每开启一次页面都会在任务栈中添加一个Activity,而只有任务栈中的Activity全部清除出栈时，任务栈被销毁，程序才会退出,这样就造成了用，户体验差, 需要点击多次返回才可以把程序退出了。
>
> (2) 每开启一次页面都会在任务栈中添加一个Activity还会造成数据冗余,重复数据太多, 会导致内存溢出的问题(OOM)。
>
> 为了解决任务栈产生的问题，Android为Activity设计了启动模式。

#### 21.Activity的四种启动模式

> **standard：默认模式**，可以不用写配置。在这个模式下，都会默认创建一个新的实例。
>
> **singleTop**：可以有多个实例，但是不允许多个相同Activity叠加。即，如果Activity在栈顶的时候，启动相同的Activity，不会创建新的实例，而会调用其onNewIntent方法。
>
> **singleTask**：只有一个实例。在同一个应用程序中启动他的时候，若Activity不存在，则会在当前task创建一个新的实例，若存在，则会把task中在其之上的其它Activity destory掉并调用它的**onNewIntent**方法。
>
> **singleInstance**：只有一个实例，并且这个实例独立运行在一个task中，这个task只有这个实例，不允许有别的Activity存在。
>
> 如何决定所属task
>
> ​    “standard”和”singleTop”的activity的目标task，和收到的Intent的发送者在同一个task内，除非intent包括参数FLAG_ACTIVITY_NEW_TASK。 如果提供了FLAG_ACTIVITY_NEW_TASK参数，会启动到别的task里。
>
> ​    “singleTask”和”singleInstance”总是把activity作为一个task的根元素，他们不会被启动到一个其他task里。

#### 22..Activity之间的跳转方式

>  **显式跳转：**在可以引用到那个类,并且可以引用到那个类的字节码时可以使用。一般用于自己程序的内部。显式跳转不可以跳转到其他程序的页面中。
>
> **隐式跳转：**可以在当前程序跳转到另一个程序的页面。隐式跳转不需要引用到那个类,但是必须得知道那个界面的动作(action)和信息(category)。
>
> **隐式意图注意点:**
>
> 1.在清单文件中定义时需要定义才能被隐式意图启动
>
> 2.中至少配置一个和一个，否则无法被启动,如果category为默认，使用intent时可以不用设置category（当不设置category时，自动添加一个默认的category）
>
> 3.Intent对象中设置的action、category、data在必须全部包含才能启动
>
> 4.中的、、都可以配置多个，Intent对象中不用全部匹配，每样匹配一个即可启动
>
> 5.如果一个意图可以匹配多个Activity，Android系统会提示选择
>
> 6.data中还可以设置type属性，那么激活时，也就必须setType()

#### 23.Activity数据传递的三种情况

> **1.向下一个活动传递数据**
>
> **2.向上一个活动传递数据**
>
> ①首先如果我们想从下一个活动中获取返回的数据的话，我们需要用startActivityForResult()来开启活动
>
> ②在新的Activity中添加返回数据的逻辑
>
> ③由于我们是使用startActivityForResult()方法来开启第二个活动的，所以在第二个活动销毁之后会调用上一个活动的onActivityResult()方法，因此需要我们在第一个活动中重写这个方法来得到返回的数据。
>
> **3.活动被回收，被重新创建了，需要接收上次被回收时的数据**
>
> Activity中还提供了一个onSaveInstanceState()回调方法，这个方法可以保证在活动被回收之前一定会调用，因此我们可以通过这个方法来解决活动被回收时数据得不到保存的问题。
>
> ①重写**onSaveInstanceState()**保存数据
>
> ②再次开启时从onSaveInstanceState中得到数据

#### 24.如何将一个Activity设置成窗口的样式。

> 中配置：android :theme="@android:style/Theme.Dialog"
>
> 另外android:theme="@android:style/Theme.Translucent" 是设置透明

#### 25.如何退出Activity？如何安全退出已调用多个Activity的Application？

> 对于单一Activity的应用来说，退出很简单，直接finish()即可。当然，也可以用killProcess()和System.exit()这样的方法。
>
> 对于多个activity：
>
> 1.抛异常强制退出
>
> 2.每打开一个Activity，就加到ArrayList中记录下来，在需要退出时，循环ArrayList关闭每一个Activity即可。
>
> 3.发送特定广播
>
> 4.递归退出，在打开新的Activity时使用startActivityForResult，然后自己加标志，在onActivityResult中处理，递归关闭。

#### 26.自定义View  

>  **View的绘制有三个过程，measure，layout，draw。自定义View我们大部分只需要重写**onMeasure(),onDraw()方法，当然了还得至少重写两个View的构造函数。
>
> Measure()中我们注意的主要有两个类 ViewGroup.LayoutParams （View 自身的布局参数），
>
>    MeasureSpecs 类（父视图对子视图的测量要求），MeasureSpecs为32位int值，高两位为mode（测量模式），低30位为size（具体测量大小）。
>
> 测量模式有三种：
>
> EXACTLY（精准的）：当前的尺寸就是当前View应该取的尺寸
>
> AT_MOST：当前尺寸是当前View能取的最大尺寸
>
> UNSPECIFIED：父容器没有对当前View有任何限制，当前View可以任意取尺寸
>
> 而测量模式跟我们的布局时的wrap_content、match_parent以及写成固定的尺寸有什么对应关系呢？
>
> match_parent—>EXACTLY。怎么理解呢？match_parent就是要利用父View给我们提供的所有剩余空间，而父View剩余空间是确定的，也就是这个测量模式的整数里面存放的尺寸。
>
> wrap（ruap）_content—>AT_MOST。怎么理解：就是我们想要将大小设置为包裹我们的view内容，那么尺寸大小就是父View给我们作为参考的尺寸，只要不超过这个尺寸就可以啦，具体尺寸就根据我们的需求去设定。
>
> 固定尺寸（如100dp）—>EXACTLY。用户自己指定了尺寸大小，我们就不用再去干涉了，当然是以指定的大小为主啦。
>
> draw()：根据Canvas（画布）自动渲染View（包括其所有子View）
>
>   绘制内容是根据画布的规定绘制在屏幕上的，画布只是规定了绘制内容时的规则；内容的位置由坐标决定，而坐标是相对于画布而言的。

#### 27.Android事件分发机制



![img](https:////upload-images.jianshu.io/upload_images/9087029-20aa80481829ed14.png?imageMogr2/auto-orient/strip|imageView2/2/w/625/format/webp)

> 当一个事件点击后，系统需要将这个事件传递给一个具体的View去处理，这个事件的传递过程就是分发过程。
>
>  一个事件产生后，传递顺序是：Activity（Window） -> ViewGroup -> View
>
>  **事件分发由三个方法协作完成：**
>
>    dispatchTouchEvent() :分发传递点击事件
>
>    onInterceptTouchEvent():判断是否拦截了某个事件(只存在于ViewGroup,普通的View是没有这个 方法)
>
>    onTouchEvent():处理点击事件
>
> **事件分发流程:**
>
> onTouch(）和onClick()的优先级
>
> onTouch()的执行高于onClick()，每当控件被点击时:
>
> 如果在回调onTouch()里返回false,就会让dispatchTouchEvent方法返回false,那么就会执行onTouchEvent();如果回调了setOnClickListener()来给控件注册点击事件的话，最后会在performClick()方法里回调onClick()。
>
> 如果在onTouch()里返回true，就会让dispatchTouchEvent()方法放回true，那么将不会执行onTouchEvent（），既onClick()也不会执行。

#### 28.ListView的四种优化方式

> **1.convertView的复用**
>
>   这也是最简单的一种优化方式，就是在Adapter类的getView方法中通过判断convertView是否为null，是的话就需要在创建一个视图出来，然后给视图设置数据，最后将这个视图返回给底层，呈现给用户；如果不为null的话，其他新的view可以通过复用的方式使用已经消失的条目view，重新设置上数据然后展现出来。
>
> **2.ViewHolder的使用**
>
>   第一种优化方式有个缺点，就是每次在findviewById，重新找到控件，然后对控件进行赋值，这样会减慢加载的速度，其实我们可以创建一个内部类ViewHolder，里面的成员变量和view中所包含的组件个数、类型相同，在convertview为null的时候，把findviewbyId找到的控件赋给ViewHolder中对应的变量，就相当于先把它们装进一个容器，下次要用的时候，直接从容器中获取，这样是不是比findviewbyId效率要高一点。
>
> **3.使用分段加载**
>
>    有些情况下我们需要加载网络中的数据，显示到ListView，而往往此时都是数据量比较多的一种情况，如果数据有1000条，没有优化过的ListView都是会一次性把数据全部加载出来的，很显然需要一段时间才能加载出来，我们不可能让用户面对着空白的屏幕等好几分钟，那么这时我们可以使用分段加载，比如先设置每次加载数据10条，当用户滑动ListView到底部的时候，我们再加载20条数据出来，然后使用Adapter刷新ListView，这样用户只需要等待10条数据的加载时间，这样也可以缓解一次性加载大量数据而导致OOM崩溃的情况。
>
> **4.使用分页加载**
>
>   上面第三种方式其实也不能完全解决OOM崩溃的情况，因为虽然我们在分段中一次只增加10条数据到List集合中，然后再刷新到ListView中去，假如有10万条数据，如果我们顺利读到最后这个List集合中还是会累积海量条数的数据，还是可能会造成OOM崩溃的情况，这时候我们就需要用到分页，比如说我们将这10万条数据分为1000页，每一页100条数据，每一页加载时都覆盖掉上一页中List集合中的内容，然后每一页内再使用分批加载，这样用户的体验就会相对好一些。

#### 29.动画分类

> 动画分类：
>
> View动画包括：平移、旋转、缩放、透明度，View动画是一种渐近式动画
>
> 帧动画：图片切换动画
>
> 属性动画：通过动态改变对象的属性达到动画效果
>
> 帧动画：
>
> View动画，继承自Animation，四个动画效果实现类：
>
> AlphaAnimation透明度渐变；
>
> ScaleAnimation尺寸渐变；
>
> TranslateAnimation坐标变化；
>
> RotateAnimation旋转变换

#### 30.Fragment的生命周期是怎么样的，跟Activity有什么关系？

Fragment必须是依存于Activity而存在的，因此Activity的生命周期会直接影响到Fragment的生命周期。



![img](https:////upload-images.jianshu.io/upload_images/9087029-05950c216ada18ac.png?imageMogr2/auto-orient/strip|imageView2/2/w/281/format/webp)

#### 31..Service

> Service是一个专门在后台处理长时间任务的Android组件，它没有UI。它有两种启动方式，startService和bindService。
>
> 这两种启动方式的区别？
>
> startService只是启动Service，启动它的组件（如Activity）和Service并没有关联，只有当Service调用stopSelf或者其他组件调用stopService服务才会终止。
>
> bindService方法启动Service，其他组件可以通过回调获取Service的代理对象和Service交互，而这两方也进行了绑定，当启动方销毁时，Service也会自动进行unBind操作，当发现所有绑定都进行了unBind时才会销毁Service。
>
> Service的onCreate回调函数可以做耗时的操作吗？
>
> 不能，android中的四大组件都是在主线程中调用的，不能做耗时操作，如果需要耗时操作需要开启子线程。

#### 32.Service生命周期

**只使用startService启动服务的生命周期**



![img](https:////upload-images.jianshu.io/upload_images/9087029-b3600dabb5f6ae9e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

**只使用BindService绑定服务的生命周期**



![img](https:////upload-images.jianshu.io/upload_images/9087029-32c92a12e147e318.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

**同时使用startService()启动服务、BindService()绑定服务的生命周期**



![img](https:////upload-images.jianshu.io/upload_images/9087029-18f941fbe4f34fa2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

#### 33.为什么在Service中创建子线程而不是Activity中

> 这是因为Activity很难对Thread进行控制，当Activity被销毁之后，就没有任何其它的办法可以再重新获取到之前创建的子线程的实例。而且在一个Activity中创建的子线程，另一个Activity无法对其进行操作。但是Service就不同了，所有的Activity都可以与Service进行关联，然后可以很方便地操作其中的方法，即使Activity被销毁了，之后只要重新与Service建立关联，就又能够获取到原有的Service中Binder的实例。因此，使用Service来处理后台任务，Activity就可以放心地finish，完全不需要担心无法对后台任务进行控制的情况。

#### 34.目前能否保证service不被杀死

> 1.Service设置成START_STICKY
>
> kill 后会被重启（等待5秒左右），重传Intent，保持与重启前一样
>
> 2.提升service进程优先级
>
> Android中的进程是托管的，当系统进程空间紧张的时候，会依照优先级自动进行进程的回收当service运行在低内存的环境时，将会kill掉一些存在的进程。因此进程的优先级将会很重要，可以在startForeground()使用startForeground()将service放到前台状态。这样在低内存时被kill的几率会低一些。
>
> 【结论】如果在极度极度低内存的压力下，该service还是会被kill掉，并且不一定会restart()
>
> 3.onDestroy方法里重启serviceservice +broadcast 方式
>
> 就是当service走onDestory()的时候，发送一个自定义的广播，当收到广播的时候，重新启动service，也可以直接在onDestroy()里startService
>
> 【结论】当使用类似口口管家等第三方应用或是在setting里-应用-强制停止时，APP进程可能就直接被干掉了，onDestroy方法都进不来，所以还是无法保证

#### 35.广播两种注册的区别

> 代码注册，它不是常驻型广播，也就是说广播跟随程序的生命周期，一旦代码所在进程被杀死，广播接收者就失效。清单文件注册是常驻型，也就是说当应用程序关闭后，如果有信息广播来，程序也会被系统调用自动运行。一旦应用程序被部署到手机，广播接收者就会生效，高版本的模拟器（3.2以上）中的接收者，需要启动过一次才能接收到广播。

#### 36.广播为什么不能开启子线程

> 广播接收者也是运行在主线程中，所以在广播接收者的onReceive方法内不能有耗时的操作，需要放在子线程中做，但是onReceive的生命周期很短，有可能广播接收者结束，子线程还没有结束，这时广播接收者所在进程很有可能被杀掉，这样子线程就会出问题，所以耗时操作最好放到service服务中。

#### 37.无序广播和有序广播的特点

> **无序广播**
>
> 1.无序，无优先级，不可中断，不可传递数据。
>
> 2.广播时可设置接收者权限，仅当接收者含有权限才能接收。接收者的也可设置发送方权限，只接收含有权限应用的广播Receiver节点增加属性permission。
>
> 3.发送广播时，通过intent.setFlags(intent.flag_include_stopped_pakeages)，包含从未启动过的程序，这样设置，可以让从未启动的接收者也收到广播。
>
> **有序广播**
>
> 1.接收者可以在中定义android:priority定义优先级，数字越大优先级越高，优先级的取值范围是: 1000(最高) ~ -1000(最低)谷歌规定最大是1000，但是他的类型其实是int。系统默认优先级是0，那么想在系统程序之前接收到广播，那么就设置大于0的数，相同优先级下,接收的顺序要看在清单文件中声明注册的顺序。
>
> 2.有序广播可以被拦截或添加数据，优先级高的接收者可以拦截优先级低的，使用abortBroadcast方法拦截， 添加数据：通过bundle传递。前面的接收者可以将数据通过setResultExtras(Bundle)方法存放进结果对象，然后传给下一个接收者，下一个接收者通过代码：Bundle bundle =getResultExtras(true))可以获取上一个接收者存入在结果对象中的数据。

#### 38.广播的优先级对无序广播生效吗？

> **生效的，对于无序广播来说，BroadcastReceiver的执行顺序如下：**
>
> \1. 所有的动态注册的BroadcastRecevier，会被一起执行，他们执行的顺序是不固定的，由Android的进程调度决定。
>
> \2. 当动态注册的BroadcastRecevier被执行完以后，会按照优先级，依次执行静态注册的BroadcastReceiver。
>
> 如果广播是无序的，那么所有的registeredReceivers都会一次性被处理，因为所有的动态注册的广播，他们的进程都是活着的，直接让他们去处理就好了。但是这一条对于静态注册的广播不适用。这是因为静态注册的广播，我们无法知道他到底进程是否存活，而如果都不是活着的，需要先把进程拉起来，一次性拉起很多进程，这是性能上无法忍受的。所以静态注册的广播，不能像动态注册的广播那样一次性执行。发送无须广播时候，静态注册的Recevier的执行是这样的，按照receivers队列，依次检查队列里面的Receiver是否存活，如果是活着的，则执行该Recevierd的OnReceiver回调，如果进程尚不存在，则首先创建进程，然后执行BroadcastReceiver的OnRecevier 回调，当一个BroadcastReceiver执行完，再去执行receivers队列里的下一个BroadcastReceiver。而receivers队列是按照优先级排列的。

#### 39.请介绍下ContentProvider是如何实现数据共享的。

> 如果想要访问内容提供器中共享的数据，就一定要借助ContentResolver类，可以通过Context中的getContentResolver（）方法获取到该类的实例。ContentResolver中提供了一系列的方法用于对数据进行CRUD操作，其中insert（）方法用于添加数据，update（）方法用于更新数据，delete（）方法用于删除数据，query（）方法用于查询数据。
>
>    内容URI给内容提供器中的数据建立了唯一标识符，它主要由两部分组成：authority和patch。authority是用于对不同的应用程序做区分的，一般为了避免冲突，都会采用程序包名的方式来进行命名。patch是用于对同一应用程序中不同的表做区分的，通常会添加到authority后面。

#### 40.内容提供者如何保证隐私数据不会泄露

> 因为所有的CRUD操作都一定要匹配到UriMatcher相应的内容URI格式才能进行的，而我们当然不可能向UriMatcher中添加隐私数据的URI，所以这部分数据根本无法被外部程序访问到。

#### 41.说说ContentProvider、ContentResolver、ContentObserver 之间的关系；

> ContentProvider是Android的四大组件之一，可见它在Android中的作用非同小可。它主要的作用是：实现各个应用程序之间的（跨应用）数据共享，比如联系人应用中就使用了ContentProvider,你在自己的应用中可以读取和修改联系人的数据，不过需要获得相应的权限。其实它也只是一个中间人，真正的数据源是文件或者SQLite等。
>
> 一个应用实现ContentProvider来提供内容给别的应用来操作， 通过ContentResolver来操作别的应用数据，当然在自己的应用中也可以。
>
> ContentObserver——内容观察者，目的是观察(捕捉)特定Uri引起的数据库的变化，继而做一些相应的处理，它类似于数据库技术中的触发器(Trigger)，当ContentObserver所观察的Uri发生变化时，便会触发它。触发器分为表触发器、行触发器，相应地ContentObserver也分为“表“ContentObserver、“行”ContentObserver，当然这是与它所监听的Uri MIME Type有关的。



作者：YoungTa0
链接：https://www.jianshu.com/p/46774f2f51b1
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。