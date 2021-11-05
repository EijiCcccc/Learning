# ViewBuilder

ViewBuilder 视图构建

Apple官方有一个解释：

Allowing those closure to provide multiple child views

允许闭包中提供多个子视图

如果不使用@ViewBuilder的时候只可以传递一个View在闭包里，使用@ViewBuilder可以传递多个View到闭包中。

示例：

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

# ViewBuilder底层解析
