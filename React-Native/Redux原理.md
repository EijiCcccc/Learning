# Redux原理

因为之前在公司开发React-Native项目中，为了解决数据同步相应的问题，使用了Redux框架，今天就来写一写Redux原理，加深一下自己对Redux的理解。

参考来自：https://www.jianshu.com/p/e984206553c2

## Redux设计理念

Redux是将整个应用状态存储到一个地方上称之为store，里面保存着一个状态树store tree，组件可以派发(dispatch)行为(action)给store，而不是直接通知其他组件，组件内部通过订阅store中的状态state来刷新自己的视图
![](https://upload-images.jianshu.io/upload_images/6548744-df461a22f59ef7da.png?imageMogr2/auto-orient/strip|imageView2/2/w/800)
