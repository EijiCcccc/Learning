# State

- 先来看看官方的解释

```
/// A property wrapper type that can read and write a value managed by SwiftUI.
///
/// SwiftUI manages the storage of any property you declare as a state. When the
/// state value changes, the view invalidates its appearance and recomputes the
/// body. Use the state as the single source of truth for a given view.
///
/// A ``State`` instance isn't the value itself; it's a means of reading and
/// writing the value. To access a state's underlying value, use its variable
/// name, which returns the ``State/wrappedValue`` property value.
///
/// You should only access a state property from inside the view's body, or from
/// methods called by it. For this reason, declare your state properties as
/// private, to prevent clients of your view from accessing them. It is safe to
/// mutate state properties from any thread.
///
/// To pass a state property to another view in the view hierarchy, use the
/// variable name with the `$` prefix operator. This retrieves a binding of the
/// state property from its ``State/projectedValue`` property. For example, in
/// the following code example `PlayerView` passes its state property
/// `isPlaying` to `PlayButton` using `$isPlaying`:
///
///     struct PlayerView: View {
///         var episode: Episode
///         @State private var isPlaying: Bool = false
///
///         var body: some View {
///             VStack {
///                 Text(episode.title)
///                 Text(episode.showTitle)
///                 PlayButton(isPlaying: $isPlaying)
///             }
///         }
///     }
```

一种属性包装器类型，可以读取和写入 SwiftUI 管理的值。

SwiftUI会管理任何使用@State声明的属性，当State值发生变化，SwiftUI会使关联的UI失效并重新计算。

State实例不是值本身，只是一种阅读方式，State提供了读取和写入Value值。要访问状态的基础值，请使用变量name，他返回State/wrappedValue的属性值

- State/wrappedValue 与 @propertyWrapper是息息相关的

要将状态属性传递给视图层次结构中的另一个视图，请使用带有$前缀运算符的变量名。这将检索状态属性来自于State/projectedValue属性

- 如果没有带有$就在SwiftUI中使用的话，编译器会报错，并且提示'insert $'

# 代码层面

```
@available(iOS 13.0, macOS 10.15, tvOS 13.0, watchOS 6.0, *)
@frozen @propertyWrapper public struct State<Value> : DynamicProperty {

    /// Creates the state with an initial wrapped value.
    ///
    /// You don't call this initializer directly. Instead, declare a property
    /// with the `@State` attribute, and provide an initial value; for example,
    /// `@State private var isPlaying: Bool = false`.
    ///
    /// - Parameter wrappedValue: An initial wrappedValue for a state.
    public init(wrappedValue value: Value)

    /// Creates the state with an initial value.
    ///
    /// - Parameter value: An initial value of the state.
    public init(initialValue value: Value)

    /// The underlying value referenced by the state variable.
    ///
    /// This property provides primary access to the value's data. However, you
    /// don't access `wrappedValue` directly. Instead, you use the property
    /// variable created with the `@State` attribute. For example, in the
    /// following code example the button's actions toggles the value of
    /// `showingProfile`, which toggles `wrappedValue`:
    ///
    ///     @State private var showingProfile = false
    ///
    ///     var profileButton: some View {
    ///         Button(action: { self.showingProfile.toggle() }) {
    ///             Image(systemName: "person.crop.circle")
    ///                 .imageScale(.large)
    ///                 .accessibilityLabel(Text("User Profile"))
    ///                 .padding()
    ///         }
    ///     }
    ///
    /// When a mutable binding value changes, the new value is immediately
    /// available. However, updates to a view displaying the value happens
    /// asynchronously, so the view may not show the change immediately.
    public var wrappedValue: Value { get nonmutating set }

    /// A binding to the state value.
    ///
    /// Use the projected value to pass a binding value down a view hierarchy.
    /// To get the `projectedValue`, prefix the property variable with `$`. For
    /// example, in the following code example `PlayerView` projects a binding
    /// of the state property `isPlaying` to the `PlayButton` view using
    /// `$isPlaying`.
    ///
    ///     struct PlayerView: View {
    ///         var episode: Episode
    ///         @State private var isPlaying: Bool = false
    ///
    ///         var body: some View {
    ///             VStack {
    ///                 Text(episode.title)
    ///                 Text(episode.showTitle)
    ///                 PlayButton(isPlaying: $isPlaying)
    ///             }
    ///         }
    ///     }
    public var projectedValue: Binding<Value> { get }
}
```

State是一个结构体，继承了DynamicProperty，有两个注解

- @frozen
- @propertyWrapper

并且实现的propertyWrapper所需要的方法，那具体State是怎么工作的呢。

待续
