# ViewBuilder

ViewBuilder 视图构建

Apple官方有一个解释：

Allowing those closure to provide multiple child views

允许闭包中提供多个子视图

如果不使用@ViewBuilder的时候只可以传递一个View在闭包里，使用@ViewBuilder可以传递多个View到闭包中。

- 示例

```
struct ExampleView<Content: View>: View {

    @ViewBuilder var content: () -> Content

    var body: some View {
        content()
    }

}

@main
struct MainApp: App {

  var body: some Scene {
      WindowGroup {
          ExampleView {
              Text("Hello world")
          }
      }
  }
}
```

![](http://m.qpic.cn/psc?/V53N7OG413cvz52OliN03DvKaZ42EFAJ/TmEUgtj9EK6.7V8ajmQrEJA**rCz*ljiFBpgg0HY5fmkaAskrF3r*WS.8KGer4kPGNr7*TkQz3.XCxo2DfuNdKVwux1JWBJ.sGcgpHeDk1U!/b&bo=PgGyAgAAAAADF70!&rf=viewer_4)

* 在UIKit中UIView是一个Class，而在SwiftUI中，View是一个Protocol

# 再看看ViewBuilder

```
@available(iOS 13.0, macOS 10.15, tvOS 13.0, watchOS 6.0, *)
@resultBuilder public struct ViewBuilder {

    /// Builds an empty view from a block containing no statements.
    public static func buildBlock() -> EmptyView

    /// Passes a single view written as a child view through unmodified.
    ///
    /// An example of a single view written as a child view is
    /// `{ Text("Hello") }`.
    public static func buildBlock<Content>(_ content: Content) -> Content where Content : View
}
```
可以看出ViewBuilder是一个struct

# ResultBuilder

* @resultBuilder是一个自定义的类型（之前是叫@_functionBuilder），添加了相关语法，用以自然地、声明的方式来创建嵌套的数据，比如链表和树。使用resultBuilder的代码可以包含原始的Swift语法，比如if和for以方便掌控条件数据或者重复的数据。

* 一个类、结构体使用@resultBuilder注解时，必须至少包含一个buildBlock方法，并且这个方法是static静态的。这个方法可以接收0个或者多个参数，在函数内部就确定了参数组成形式。

- 示例

```
@resultBuilder
struct StringBuilder {
    static func buildBlock(_ s1: String, _ s2: String) -> String {
            s1 + s2
    }
}

func welcome(@StringBuilder showText: () -> String) -> String {
    showText()
}

@main
struct MainApp: App {

    var body: some Scene {
        WindowGroup {
            ExampleView {
                Text(welcome {
                    "hello "
                    "world"
                })
            }
        }
    }
}
```

![](http://m.qpic.cn/psc?/V53N7OG413cvz52OliN03DvKaZ42EFAJ/TmEUgtj9EK6.7V8ajmQrEJA**rCz*ljiFBpgg0HY5fmkaAskrF3r*WS.8KGer4kPGNr7*TkQz3.XCxo2DfuNdKVwux1JWBJ.sGcgpHeDk1U!/b&bo=PgGyAgAAAAADF70!&rf=viewer_4)
