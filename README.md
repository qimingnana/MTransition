MTransition
===========================
MTransition是一个Android上的页面切换动画库，它可以让一些复杂的、自定义的页面切换动画更加简单地实现出来，节省开发成本。

## 示例
![](/Introduction/1.gif)

`该交互设计来源于:https://dribbble.com/shots/2493845-ToFind-Transition-Test`

在上面的动图示例中，动画执行前后分别是两个不同的Activity。如下图：  
![](/Introduction/1.png "Activity1") ![](/Introduction/2.png "Activity2")

像这种跨Activity的切换动画是现有技术比较难实现的，并且还需要响应用户的跟手操作。MTransition非常适合这种情况。

作为开发者的你，只需要完成两个Activity的UI开发即可，中间的过渡动画交给MTransiton处理，MTransiton可以完美实现你需要的各种页面切换\过渡动画，节省你的开发时间。

更多示例请看本仓库代码或者[SlidingActivity](https://github.com/HJ-Money/SlidingActivity)

三、使用MTransition

MTransition适用于所有页面的切换动画，这里的页面不一定是Activity，也可以是Fragment、Window或者是同一个Activity的两个View，
但是页面必须是占满整个屏幕的，否则可能会出现效果不符合预期。

现假设我们需要实现一个从页面A(FromPage)到页面B(ToPage)的过渡动画，首先我们先完成页面A和页面B本身的UI开发，然后可以用MTransition完成过渡动画。
a、基础用法

step1、在页面A打开页面B之前创建MTransition，并设置页面A最外层的View给MTransition：
（代码。。。）

step2、在页面B创建之后，且在页面显示之前，设置页面B最外层的View给MTransition，同时告诉MTransition页面的View要做哪些动画，调整View顺序等：
（代码。。。）

step3、设置动画时长，然后start MTransition，一个过渡动画即完成
（代码。。。）

NOTE：1、如果页面A和B是Activity的话，因为Activity默认是有Activity的进场退场动画，所以需要在startActivity()和finish()之后调用以下代码：
（代码。。。）

2、在确定不再需要当前页面的MTransition时，请务必调用destoryTransition()来销毁MTransition，不然会内存泄漏：
（代码。。。）

b、进阶用法
b1、反向动画
在页面B返回页面A时，你很有可能需要刚才的过渡动画反向执行一次，这时候可以调用reverse()，执行一遍反向动画，当然你可以随时改变动画路径，
例如你可以改变动画时长、甚至完全换一个过渡动画；
（代码。。。）

b2、定格动画
你可以调用setProgress()让动画停留在你想要的地方，因此你可以利用这点实现跟手动画，具体请参考本仓库代码；
（代码。。。）

b3、自定义动画
MTransition已经提供了一堆基础的动画api，例如平移、旋转、缩放、透明度等。这些api已经可以满足大部分需求，但是如果你需要一些形变或者更加复杂的动画，
你就需要自定义动画。

step1、将你的自定义动画View实现ITransitional接口
（代码。。。）

step2、调用replaceBy()接口，将你的自定义动画View替换原本的View，让它在过渡动画过程中做动画
（代码。。。）

该方案可以结合Lottie或者其他动画库，实现一些非常酷炫的效果，具体请参考本仓库代码中的Demo5、6、7；
（示例动图）

四、其他说明
目前该库处在探索优化阶段，接下来一方面会去优化性能，尝试更优的实现方案，另一方面将往“解除页面必须占满屏幕的限制”方向进发，让MTransition可以服务
任意区域的过渡动画。