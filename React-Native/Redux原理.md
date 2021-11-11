# Redux原理
因为之前在公司开发React-Native项目中，为了解决数据同步相应的问题，使用了Redux框架，今天就来写一写Redux原理，加深一下自己对Redux的理解。

参考来自：https://www.jianshu.com/p/e984206553c2

# Redux设计理念
Redux是将整个应用状态存储到一个地方上称之为store，里面保存着一个状态树store tree，组件可以派发(dispatch)行为(action)给store，而不是直接通知其他组件，组件内部通过订阅store中的状态state来刷新自己的视图
![](https://upload-images.jianshu.io/upload_images/6548744-df461a22f59ef7da.png?imageMogr2/auto-orient/strip|imageView2/2/w/800)

# Redux三大原则
- 唯一数据源
- 保持只读状态
- 数据改变只能通过纯函数执行

## 唯一数据源
整个应用的state都被存储到一个状态树里面，并且这个状态树，只存在于唯一的store中。

## 保持只读性
state是只读的，唯一可以改变state的方式只能通过action，action是一个用于描述以发生时间的普通对象。

## 数据改变只能通过纯函数执行
使用纯函数来执行修改，为了描述action是如何改变state的，只需要编写reducer

# Redux概念解析
