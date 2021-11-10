# React-Native底层原理

- 参考
  - https://zhuanlan.zhihu.com/p/41920417

## React-Native框架构成

React-Native框架内部已经提供了很多内置组件，如图所示。
如View、Text等基本组件，用于一些功能布局的Button、Picker等，用于列表展示的各种List组件和对应和对应iOS平台还有Android平台的特定组件、API等。
同时也提供了供编写与原生太平交互的接口。
![](https://pic2.zhimg.com/80/v2-2bf84ece7deae66b28515b442240cd7d_720w.jpg)

## React-Native工作原理

![](https://pic4.zhimg.com/80/v2-990aa3a1c34a8e1b956baaa00b4ca9db_720w.jpg)
React-Native渲染在React框架中，JSX源码通过React框架最终渲染到了浏览器的真实DOM中，而在React-Native框架中，JSX源码通过React-Native框架编译后，通过对应平台的Bridge实现了与原生框架的通信。如果我们在程序中调用了React-Native提供的API，那么React-Native框架通过Bridge调用原生框架中的方法。因为React-Native的底层为React框架，所以如果是UI层的变更，那么就映射为虚拟DOM后进行的diff算法，diff算法计算出变动后的JSON映射文件，最终由Native层将此JSON文件映射渲染到原生APP的页面元素上，最终实现了在项目中只需控制state以及props的变更来引起iOS与Android平台的UI变更。编写React-Native最终会打包成一个main.bundle.js文件供App加载，此文件可以在App设备本地，也可以存放于服务器上供App更新（热更新）。

## React-Native与原生平台进行通信

在与原生框架通信中，React-Native采用了JavaScriptCore作为JS VM，中间的JSON文件与Bridge进行通信。而如果在使用Chrome浏览器进行调试时，那么所有的JavaScript代码都将运行在Chrome的V8引擎中，与原生代码通过WebSocket进行通信。
![](https://pic4.zhimg.com/80/v2-60eb566b812a49fa945e802abe8dd453_720w.jpg)
* JS VM是一个面向JavaScript开发领域的基础框架。

# 组件间通信

React-Native开发最基本的元素就是组件，React-Native与React一样，也会涉及到组件之间的通信，用于数据在组件间传递。

## 父子组件的通信

在React-Native中，父组件向子组件传递值，可以通过props的形式。在下例中，父组件通过调用子组件并赋值子组件的name为React，子组件通过this.props.name获取父组件传递的name的字符串值React。
```
/**
* 章节: 03-04
* 父子组件通信，在父组件中调用子组件
* FilePath: /03-04/parent-2-child.js
* @Parry
*/

<ChildComponent name='React'/>

/**
* 章节: 03-04
* 子组件实现，通过 props 获取父页面传递的值
* FilePath: /03-04/parent-2-child.js
* @Parry
*/

class ChildComponent extends Component {
    render() {
        return (
          <Text>Hello {this.props.name}!</Text>
        );
    }
}
```

## 子父组件的通信

待续
