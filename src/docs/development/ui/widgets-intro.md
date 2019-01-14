---
title: Introduction to widgets
---

Flutter widgets are built using a modern react-style framework, which takes
inspiration from [React](https://reactjs.org). The central idea is
that you build your UI out of widgets. Widgets describe what their view
should look like given their current configuration and state. When a widget's
state changes, the widget rebuilds its description, which the framework diffs
against the previous description in order to determine the minimal changes
needed in the underlying render tree to transition from one state to the next.
(Flutter小部件使用现代的反应式框架构建，它的灵感来自React。其核心思想是用小部件构建UI。小部件描述了给定当前配置和状态下视图的外观。当小部件的状态发生变化时，小部件将重新构建其描述，框架将其与前一个描述区别开来，以确定从一个状态过渡到下一个状态所需的底层呈现树中的最小更改。)

<aside id="note" class="alert alert-info" markdown="1">
**Note:** If you would like to become better acquainted with Flutter by diving
into some code, check out
[Building Layouts in Flutter](/docs/development/ui/layout) and
[Adding Interactivity to Your Flutter App](/docs/development/ui/interactive).
(注意：如果你想通过深入学习一些代码来更好地了解 Flutter，可以在Flutter 中查看构建布局，并在 Flutter 应用程序中添加交互性。)
</aside>

## Hello World

The minimal Flutter app simply calls the [runApp()][] function with a widget:
(最小的 Flutter 应用程序使用一个小部件简单地调用runApp()函数：)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

The [runApp()][] function takes the given
[Widget]({{api}}/widgets/Widget-class.html) and makes it the root of the
widget tree. In this example, the widget tree consists of two widgets, the
[Center]({{api}}/widgets/Center-class.html) widget and its child, the
[Text]({{api}}/widgets/Text-class.html) widget. The framework forces the root
widget to cover the screen, which means the text "Hello, world" ends up centered
on screen. The text direction needs to be specified in this instance; when the
MaterialApp widget is used, this is taken care of for you, as demonstrated
later.
([runApp()][] 函数的作用是：获取给定的 [Widget]() 小部件，并使其成为窗口小部件树的根。在本例中，小部件树由两个小部件组成，一个是 [Center]() 小部件，另一个是其子部件 [Text]() 小部件。框架强制根小部件覆盖屏幕，这意味着文本 “Hello, world” 以屏幕为中心结束。需要在此实例中指定文本方向；当使用 MaterialApp 小部件时，这将为您处理好，稍后将对此进行演示。)

When writing an app, you'll commonly author new widgets that are subclasses of
either [StatelessWidget]({{api}}/widgets/StatelessWidget-class.html) or
[StatefulWidget]({{api}}/widgets/StatefulWidget-class.html), depending on
whether your widget manages any state. A widget's main job is to implement a
[build]({{api}}/widgets/StatelessWidget/build.html) function, which describes
the widget in terms of other, lower-level widgets. The framework builds those
widgets in turn until the process bottoms out in widgets that represent the
underlying [RenderObject]({{api}}/rendering/RenderObject-class.html), which
computes and describes the geometry of the widget.
(在编写应用程序时，您通常会编写新的小部件，它们是 [StatelessWidget]() 或 [StatefulWidget]() 的子类，这取决于小部件是否管理任何状态。小部件的主要工作是实现构建函数，该函数根据其他更低级的小部件描述小部件。框架依次构建这些小部件，直到流程在表示底层 [RenderObject]() 的小部件中结束，[RenderObject]() 计算和描述小部件的几何形状。)

## Basic widgets

Flutter comes with a suite of powerful basic widgets, of which the following are
very commonly used:
(Flutter 附带了一套功能强大的基本小部件，其中最常用的有:)

 * [Text]({{api}}/widgets/Text-class.html): The
   [Text]({{api}}/widgets/Text-class.html) widget lets you create a run of
   styled text within your application.
   ([Text]()：[Text]() 小部件允许您在应用程序中创建样式文本。)

 * [Row]({{api}}/widgets/Row-class.html),
   [Column]({{api}}/widgets/Column-class.html): These flex widgets let you
   create flexible layouts in both the horizontal
   ([Row]({{api}}/widgets/Row-class.html)) and vertical
   ([Column]({{api}}/widgets/Column-class.html)) directions. Its design is
   based on the web's flexbox layout model.
   ([Row]()，[Column]()：这些 flex 小部件允许您在水平([Row]())和垂直([Column]())方向上创建灵活的布局。它的设计是基于网络的 flexbox 布局模型。)

 * [Stack]({{api}}/widgets/Stack-class.html): Instead of being linearly
   oriented (either horizontally or vertically), a
   [Stack]({{api}}/widgets/Stack-class.html) widget lets you stack widgets on
   top of each other in paint order. You can then use the
   [Positioned]({{api}}/widgets/Positioned-class.html) widget on children of a
   [Stack]({{api}}/widgets/Stack-class.html) to position them relative to the
   top, right, bottom, or left edge of the stack. Stacks are based on the web's
   absolute positioning layout model.
   ([Stack]()：[Stack]() 小部件不是线性的(水平的或垂直的)，它允许您按照绘制顺序将小部件堆叠在一起。然后，可以使用堆栈的子节点上的定位小部件将它们相对于堆栈的顶部、右侧、底部或左侧边缘进行定位。栈是基于 Web 的绝对定位布局模型。)

 * [Container]({{api}}/widgets/Container-class.html): The
   [Container]({{api}}/widgets/Container-class.html) widget lets you create a
   rectangular visual element. A container can be decorated with a
   [BoxDecoration]({{api}}/painting/BoxDecoration-class.html), such as a
   background, a border, or a shadow. A
   [Container]({{api}}/widgets/Container-class.html) can also have margins,
   padding, and constraints applied to its size. In addition, a
   [Container]({{api}}/widgets/Container-class.html) can be transformed in
   three dimensional space using a matrix.
   ([Container]()：[Container]()小部件允许您创建一个矩形的可视元素。容器可以用方框装饰，如背景、边框或阴影。容器还可以对其大小应用空白、填充和约束。此外，容器可以使用矩阵在三维空间中进行转换。)

Below are some simple widgets that combine these and other widgets:
(下面是一些简单的小部件，结合了这些和其他小部件：)

```dart
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  MyAppBar({this.title});

  // Fields in a Widget subclass are always marked "final".

  final Widget title;

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 56.0, // in logical pixels
      padding: const EdgeInsets.symmetric(horizontal: 8.0),
      decoration: BoxDecoration(color: Colors.blue[500]),
      // Row is a horizontal, linear layout.
      child: Row(
        // <Widget> is the type of items in the list.
        children: <Widget>[
          IconButton(
            icon: Icon(Icons.menu),
            tooltip: 'Navigation menu',
            onPressed: null, // null disables the button
          ),
          // Expanded expands its child to fill the available space.
          Expanded(
            child: title,
          ),
          IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Material is a conceptual piece of paper on which the UI appears.
    return Material(
      // Column is a vertical, linear layout.
      child: Column(
        children: <Widget>[
          MyAppBar(
            title: Text(
              'Example title',
              style: Theme.of(context).primaryTextTheme.title,
            ),
          ),
          Expanded(
            child: Center(
              child: Text('Hello, world!'),
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    title: 'My app', // used by the OS task switcher
    home: MyScaffold(),
  ));
}
```

Be sure to have a `uses-material-design: true` entry in the `flutter`
section of your `pubspec.yaml` file. It allows you to use the predefined
set of [Material icons](https://design.google.com/icons/).
(确保在您的 pubspec.yaml 的文件中 flutter 部分有一个 `uses-material-design: true` 条目。它允许您使用预定义的 [Material icons]()。)

```yaml
name: my_app
flutter:
  uses-material-design: true
```

Many widgets need to be inside of a
[MaterialApp]({{api}}/material/MaterialApp-class.html) to display properly, in
order to inherit theme data. Therefore, we run the application with a
[MaterialApp]({{api}}/material/MaterialApp-class.html).
(为了继承主题数据，许多小部件需要位于 [MaterialApp]() 中才能正确显示。因此，我们使用 [MaterialApp]() 运行应用程序。)

The `MyAppBar` widget creates a
[Container]({{api}}/widgets/Container-class.html) with a height of 56
device-independent pixels with an internal padding of 8 pixels, both on the left
and the right. Inside the container, `MyAppBar` uses a
[Row]({{api}}/widgets/Row-class.html) layout to organize its children. The
middle child, the `title` widget, is marked as
[Expanded]({{api}}/widgets/Expanded-class.html), which means it expands to
fill any remaining available space that hasn't been consumed by the other
children. You can have multiple
[Expanded]({{api}}/widgets/Expanded-class.html) children and determine the
ratio in which they consume the available space using the
[flex]({{api}}/widgets/Expanded-class.html#flex) argument to
[Expanded]({{api}}/widgets/Expanded-class.html).
(MyAppBar 小部件创建一个高度为56个与设备无关的像素的容器，其内部填充为8个像素，包括左侧和右侧。在容器内部，MyAppBar使用行布局来组织其子元素。中间的子部件 title 被标记为展开的，这意味着它展开以填充其他子部件未使用的任何剩余可用空间。您可以有多个展开的子节点，并使用要展开的 flex 参数确定它们消耗可用空间的比例。)

The `MyScaffold` widget organizes its children in a vertical column. At the top
of the column it places an instance of `MyAppBar`, passing the app bar a
[Text]({{api}}/widgets/Text-class.html) widget to use as its title. Passing
widgets as arguments to other widgets is a powerful technique that lets you
create generic widgets that can be reused in a wide variety of ways. Finally,
`MyScaffold` uses an [Expanded]({{api}}/widgets/Expanded-class.html) to fill
the remaining space with its body, which consists of a centered message.
(MyScaffold 小部件将其子部件组织在垂直列中。在列的顶部，它放置一个 MyAppBar 实例，将一个文本小部件作为标题传递给应用程序栏。将小部件作为参数传递给其他小部件是一项强大的技术，它允许您创建可以多种方式重用的通用小部件。最后，MyScaffold 使用展开后的消息体填充剩余空间，该消息体由一个居中消息组成。)

More information: [Layouts](/docs/development/ui/widgets/layout)

## Using Material Components

Flutter provides a number of widgets that help you build apps that follow
Material Design. A Material app starts with the
[MaterialApp]({{api}}/material/MaterialApp-class.html) widget, which builds a
number of useful widgets at the root of your app, including a
[Navigator]({{api}}/widgets/Navigator-class.html), which manages a stack of
widgets identified by strings, also known as "routes". The
[Navigator]({{api}}/widgets/Navigator-class.html) lets you transition smoothly
between screens of your application. Using the
[MaterialApp]({{api}}/material/MaterialApp-class.html) widget is entirely
optional but a good practice.
(Flutter 提供了许多小部件，可以帮助您构建遵循材料设计的应用程序。Material 应用程序从 MaterialApp 小部件开始，该小部件在应用程序的根目录中构建许多有用的小部件，包括一个导航器，它管理由字符串标识的小部件堆栈，也称为“路由”。导航器允许您在应用程序的屏幕之间平稳地转换。使用 MaterialApp 小部件完全是可选的，但这是一个很好的实践。)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    title: 'Flutter Tutorial',
    home: TutorialHome(),
  ));
}

class TutorialHome extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Scaffold is a layout for the major Material Components.
    return Scaffold(
      appBar: AppBar(
        leading: IconButton(
          icon: Icon(Icons.menu),
          tooltip: 'Navigation menu',
          onPressed: null,
        ),
        title: Text('Example title'),
        actions: <Widget>[
          IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
      // body is the majority of the screen.
      body: Center(
        child: Text('Hello, world!'),
      ),
      floatingActionButton: FloatingActionButton(
        tooltip: 'Add', // used by assistive technologies
        child: Icon(Icons.add),
        onPressed: null,
      ),
    );
  }
}
```

Now that we've switched from `MyAppBar` and `MyScaffold` to the
[AppBar]({{api}}/material/AppBar-class.html) and
[Scaffold]({{api}}/material/Scaffold-class.html) widgets from `material.dart`,
our app is starting to look at bit more Material. For example, the app bar has a
shadow and the title text inherits the correct styling automatically. We've also
added a floating action button for good measure.
(现在我们已经从 MyAppBar 和 MyScaffold 切换到 material.dart 中的 AppBar 和 Scaffold 小部件，我们的应用程序开始关注更多的 Material 。例如，应用程序栏有一个阴影，标题文本自动继承正确的样式。我们还添加了一个浮动的动作按钮，以便更好地测量。)

Notice that we're again passing widgets as arguments to other widgets. The
[Scaffold]({{api}}/material/Scaffold-class.html) widget takes a number of
different widgets as named arguments, each of which are placed in the Scaffold
layout in the appropriate place. Similarly, the
[AppBar]({{api}}/material/AppBar-class.html) widget lets us pass in widgets
for the [leading]({{api}}/material/AppBar-class.html#leading) and the
[actions]({{api}}/material/AppBar-class.html#actions) of the
[title]({{api}}/material/AppBar-class.html#title) widget. This pattern recurs
throughout the framework and is something you might consider when designing your
own widgets.
(注意，我们再次将小部件作为参数传递给其他小部件。Scaffold 小部件接受许多不同的小部件作为命名参数，每个小部件都放置在适当的位置的 Scaffold 布局中。类似地，AppBar 小部件允许我们传入小部件作为标题小部件的开头和操作。这种模式在整个框架中反复出现，您可以在设计自己的小部件时考虑这种模式。)

More information: [Material components](/docs/development/ui/widgets/material)

## Handling gestures

Most applications include some form of user interaction with the system. The
first step in building an interactive application is to detect
input gestures. Let's see how that works by creating a simple button:
(大多数应用程序都包含某种形式的用户与系统的交互。构建交互式应用程序的第一步是检测输入手势。让我们看看如何通过创建一个简单的按钮：)

```dart
class MyButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        print('MyButton was tapped!');
      },
      child: Container(
        height: 36.0,
        padding: const EdgeInsets.all(8.0),
        margin: const EdgeInsets.symmetric(horizontal: 8.0),
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(5.0),
          color: Colors.lightGreen[500],
        ),
        child: Center(
          child: Text('Engage'),
        ),
      ),
    );
  }
}
```

The [GestureDetector]({{api}}/widgets/GestureDetector-class.html) widget
doesn't have a visual representation but instead detects gestures made by the
user. When the user taps the
[Container]({{api}}/widgets/Container-class.html), the
[GestureDetector]({{api}}/widgets/GestureDetector-class.html) calls its
[onTap]({{api}}/widgets/GestureDetector-class.html#onTap) callback, in this
case printing a message to the console. You can use
[GestureDetector]({{api}}/widgets/GestureDetector-class.html) to detect a
variety of input gestures, including taps, drags, and scales.
(GestureDetector 小部件没有可视化表示，而是检测用户所做的手势。当用户点击容器时，GestureDetector调用它的onTap回调，在本例中是将消息打印到控制台。您可以使用手势redetector来检测各种输入手势，包括轻击、拖动和缩放。)

Many widgets use a
[GestureDetector]({{api}}/widgets/GestureDetector-class.html) to provide
optional callbacks for other widgets. For example, the
[IconButton]({{api}}/material/IconButton-class.html),
[RaisedButton]({{api}}/material/RaisedButton-class.html), and
[FloatingActionButton]({{api}}/material/FloatingActionButton-class.html)
widgets have [onPressed]({{api}}/material/RaisedButton-class.html#onPressed)
callbacks that are triggered when the user taps the widget.
(许多小部件使用手势 redetector 来为其他小部件提供可选的回调。例如，IconButton、RaisedButton 和 FloatingActionButton 小部件都有 onPressed 回调函数，这些回调函数在用户单击小部件时触发。)

More information: [Gestures in Flutter](/docs/development/ui/advanced/gestures)

## Changing widgets in response to input

Thus far, we've used only stateless widgets. Stateless widgets receive arguments
from their parent widget, which they store in
[final](https://www.dartlang.org/guides/language/language-tour#final-and-const)
member variables. When a widget is asked to
[build]({{api}}/widgets/StatelessWidget/build.html), it uses these stored
values to derive new arguments for the widgets it creates.
(到目前为止，我们只使用了 Stateless 的小部件。 Stateless 小部件从其父小部件接收参数，这些参数存储在 final 成员变量中。当要求 build 小部件时，它使用这些存储值为它创建的小部件派生新参数。)

In order to build more complex experiences&mdash;for example, to react in more
interesting ways to user input&mdash;applications typically carry some state.
Flutter uses StatefulWidgets to capture this idea. StatefulWidgets are special
widgets that know how to generate State objects, which are then used to hold
state. Consider this basic example, using the
[RaisedButton]({{api}}/material/RaisedButton-class.html) mentioned earlier:
(为了构建更复杂的体验(例如，以更有趣的方式对用户输入作出反应)，应用程序通常带有某种状态。Flutter 使用 StatefulWidgets 捕捉这个想法。 StatefulWidgets 是一种特殊的小部件，它知道如何生成状态对象，然后用来保存状态。考虑这个基本示例，使用前面提到的 RaisedButton :)

```dart
class Counter extends StatefulWidget {
  // This class is the configuration for the state. It holds the
  // values (in this case nothing) provided by the parent and used by the build
  // method of the State. Fields in a Widget subclass are always marked "final".

  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      // This call to setState tells the Flutter framework that
      // something has changed in this State, which causes it to rerun
      // the build method below so that the display can reflect the
      // updated values. If we changed _counter without calling
      // setState(), then the build method would not be called again,
      // and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance
    // as done by the _increment method above.
    // The Flutter framework has been optimized to make rerunning
    // build methods fast, so that you can just rebuild anything that
    // needs updating rather than having to individually change
    // instances of widgets.
    return Row(
      children: <Widget>[
        RaisedButton(
          onPressed: _increment,
          child: Text('Increment'),
        ),
        Text('Count: $_counter'),
      ],
    );
  }
}
```

You might wonder why StatefulWidget and State are separate objects. In Flutter,
these two types of objects have different life cycles. Widgets are temporary
objects, used to construct a presentation of the application in its current
state. State objects on the other hand are persistent between calls to
[build()]({{api}}/widgets/State/build.html), allowing them to remember
information.
(您可能想知道为什么 StatefulWidget 和 State 是独立的对象。在 Flutter 中，这两种类型的对象具有不同的生命周期。小部件是临时对象，用于构造应用程序当前状态的表示。另一方面，State 对象在调用 build() 时是持久的，允许它们记住信息。)

The example above accepts user input and directly uses the result in its
build method.  In more complex applications, different parts of the widget
hierarchy might be responsible for different concerns; for example, one
widget might present a complex user interface with the goal of gathering
specific information, such as a date or location, while another widget might
use that information to change the overall presentation.
(上面的示例接受用户输入，并在其构建方法中直接使用结果。在更复杂的应用程序中，小部件层次结构的不同部分可能负责不同的关注点;例如，一个小部件可能显示一个复杂的用户界面，其目标是收集特定的信息，例如日期或位置，而另一个小部件可能使用这些信息来更改整个表示。)

In Flutter, change notifications flow "up" the widget hierarchy by way of
callbacks, while current state flows "down" to the stateless widgets that do
presentation. The common parent that redirects this flow is the State.
The following slightly more complex example shows how this works in practice:
(在 Flutter 中，更改通知通过回调的方式在小部件层次结构中“向上”流动，而当前状态“向下”流动到进行表示的无状态小部件。重定向此流的公共父流程是状态。下面这个稍微复杂一点的例子展示了它在实践中是如何工作的:)


```dart
class CounterDisplay extends StatelessWidget {
  CounterDisplay({this.count});

  final int count;

  @override
  Widget build(BuildContext context) {
    return Text('Count: $count');
  }
}

class CounterIncrementor extends StatelessWidget {
  CounterIncrementor({this.onPressed});

  final VoidCallback onPressed;

  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: onPressed,
      child: Text('Increment'),
    );
  }
}

class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      ++_counter;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(children: <Widget>[
      CounterIncrementor(onPressed: _increment),
      CounterDisplay(count: _counter),
    ]);
  }
}
```

Notice how we created two new stateless widgets, cleanly separating
the concerns of _displaying_ the counter (CounterDisplay) and _changing_
the counter (CounterIncrementor).
(注意我们是如何创建两个新的无状态小部件的，它们干净地分隔了显示计数器( CounterDisplay )和更改计数器( CounterIncrementor )的关注点。)
Although the net result is the same as the previous example, the separation of
responsibility allows greater complexity to be encapsulated in the individual
widgets, while maintaining simplicity in the parent.
(尽管最终的结果与前面的示例相同，但是职责分离允许将更大的复杂性封装到各个小部件中，同时在父部件中保持简单性。)

More information:

- [StatefulWidget]({{api}}/widgets/StatefulWidget-class.html)
- [State.setState]({{api}}/widgets/State/setState.html)

## Bringing it all together

What follows is a more complete example that brings together the concepts
introduced above: A hypothetical shopping application displays various
products offered for sale, and maintains a shopping cart for
intended purchases. Start by defining the presentation class,
`ShoppingListItem`:
(下面是一个更完整的示例，它综合了上面介绍的概念:一个假设的购物应用程序显示提供给销售的各种产品，并维护一个用于购买的购物车。首先定义presentation类ShoppingListItem:)

```dart
class Product {
  const Product({this.name});
  final String name;
}

typedef void CartChangedCallback(Product product, bool inCart);

class ShoppingListItem extends StatelessWidget {
  ShoppingListItem({Product product, this.inCart, this.onCartChanged})
      : product = product,
        super(key: ObjectKey(product));

  final Product product;
  final bool inCart;
  final CartChangedCallback onCartChanged;

  Color _getColor(BuildContext context) {
    // The theme depends on the BuildContext because different parts of the tree
    // can have different themes.  The BuildContext indicates where the build is
    // taking place and therefore which theme to use.

    return inCart ? Colors.black54 : Theme.of(context).primaryColor;
  }

  TextStyle _getTextStyle(BuildContext context) {
    if (!inCart) return null;

    return TextStyle(
      color: Colors.black54,
      decoration: TextDecoration.lineThrough,
    );
  }

  @override
  Widget build(BuildContext context) {
    return ListTile(
      onTap: () {
        onCartChanged(product, !inCart);
      },
      leading: CircleAvatar(
        backgroundColor: _getColor(context),
        child: Text(product.name[0]),
      ),
      title: Text(product.name, style: _getTextStyle(context)),
    );
  }
}
```

The `ShoppingListItem` widget follows a common pattern for stateless widgets. It
stores the values it receives in its constructor in
[final](https://www.dartlang.org/guides/language/language-tour#final-and-const)
member variables, which it then uses during its
[build]({{api}}/widgets/StatelessWidget/build.html) function. For example, the
`inCart` boolean toggles between two visual appearances: one that uses the
primary color from the current theme, and another that uses gray.
(ShoppingListItem 小部件遵循 无状态 小部件的常见模式。它将在构造函数中接收的值存储在 final 成员变量中，然后在构建函数中使用这些值。例如，inCart 布尔值在两个视觉外观之间切换: 一个使用当前主题的主色，另一个使用灰色。)

When the user taps the list item, the widget doesn't modify its `inCart` value
directly. Instead, the widget calls the `onCartChanged` function it received
from its parent widget. This pattern lets you store state higher in the widget
hierarchy, which causes the state to persist for longer periods of time. In the
extreme, the state stored on the widget passed to
[runApp()][] persists for the lifetime of the
application.
(当用户点击列表项时，小部件不会直接修改其 inCart 值。相反，小部件调用从其父小部件接收到的 onCartChanged 函数。此模式允许您在小部件层次结构中存储更高的状态，这将导致状态持续更长的时间。在极端情况下，传递给 [runApp()]() 的小部件上存储的状态将持续到应用程序的整个生命周期。)

When the parent receives the `onCartChanged` callback, the parent updates its
internal state, which triggers the parent to rebuild and create a new instance
of `ShoppingListItem` with the new `inCart` value. Although the parent creates a
new instance of `ShoppingListItem` when it rebuilds, that operation is cheap
because the framework compares the newly built widgets with the previously built
widgets and applies only the differences to the underlying
[RenderObject]({{api}}/rendering/RenderObject-class.html).
(当父类接收 onCartChanged 回调时，父类更新其内部状态，这将触发父类使用新的 inCart 值重新构建并创建 ShoppingListItem 的新实例。尽管父组件在重新构建时创建了 ShoppingListItem 的新实例，但该操作的成本很低，因为框架将新构建的小部件与以前构建的小部件进行比较，并且只将差异应用于底层的 RenderObject。)

Here's an example parent widget that stores mutable state:
(下面是一个存储可变状态的父小部件示例)

<!--
class Product {
  const Product({this.name});
  final String name;
}

class ShoppingListItem extends StatelessWidget {
  ShoppingListItem({Product product, bool inCart, Function onCartChanged});
  @override
  Widget build(BuildContext context) => null;
}
-->
```dart
class ShoppingList extends StatefulWidget {
  ShoppingList({Key key, this.products}) : super(key: key);

  final List<Product> products;

  // The framework calls createState the first time a widget appears at a given
  // location in the tree. If the parent rebuilds and uses the same type of
  // widget (with the same key), the framework re-uses the State object
  // instead of creating a new State object.

  @override
  _ShoppingListState createState() => _ShoppingListState();
}

class _ShoppingListState extends State<ShoppingList> {
  Set<Product> _shoppingCart = Set<Product>();

  void _handleCartChanged(Product product, bool inCart) {
    setState(() {
      // When a user changes what's in the cart, we need to change _shoppingCart
      // inside a setState call to trigger a rebuild. The framework then calls
      // build, below, which updates the visual appearance of the app.

      if (inCart)
        _shoppingCart.add(product);
      else
        _shoppingCart.remove(product);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Shopping List'),
      ),
      body: ListView(
        padding: EdgeInsets.symmetric(vertical: 8.0),
        children: widget.products.map((Product product) {
          return ShoppingListItem(
            product: product,
            inCart: _shoppingCart.contains(product),
            onCartChanged: _handleCartChanged,
          );
        }).toList(),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    title: 'Shopping App',
    home: ShoppingList(
      products: <Product>[
        Product(name: 'Eggs'),
        Product(name: 'Flour'),
        Product(name: 'Chocolate chips'),
      ],
    ),
  ));
}
```

The `ShoppingList` class extends
[StatefulWidget]({{api}}/widgets/StatefulWidget-class.html), which means this
widget stores mutable state. When the `ShoppingList` widget is first inserted
into the tree, the framework calls the
[createState]({{api}}/widgets/StatefulWidget-class.html#createState) function
to create a fresh instance of `_ShoppingListState` to associate with that
location in the tree. (Notice that subclasses of
[State]({{api}}/widgets/State-class.html) are typically named with leading
underscores to indicate that they are private implementation details.) When this
widget's parent rebuilds, the parent creates a new instance of `ShoppingList`,
but the framework reuses the `_ShoppingListState` instance that is already in
the tree rather than calling
[createState]({{api}}/widgets/StatefulWidget-class.html#createState) again.
(ShoppingList 类扩展了 StatefulWidget ，这意味着这个小部件存储可变状态。当 ShoppingList 小部件首次插入到树中时，框架调用 createState 函数来创建 _ShoppingListState 的新实例，以与树中的那个位置相关联。(注意State的子类通常使用前导下划线命名，以表明它们是私有实现细节)。当这个小部件的父组件重新构建时，父组件会创建一个新的 ShoppingList 实例，但是框架会重用树中的 _ShoppingListState 实例，而不是再次调用 createState 。)

To access properties of the current `ShoppingList`, the `_ShoppingListState` can
use its [widget]({{api}}/widgets/State-class.html#widget) property. If the
parent rebuilds and creates a new `ShoppingList`, the `_ShoppingListState`
rebuilds with the new [widget]({{api}}/widgets/State-class.html#widget) value.
If you wish to be notified when the
[widget]({{api}}/widgets/State-class.html#widget) property changes, you can
override the
[didUpdateWidget]({{api}}/widgets/State-class.html#didUpdateWidget) function,
which is passed `oldWidget` to let you compare the old widget with the current
[widget]({{api}}/widgets/State-class.html#widget).
(要访问当前 ShoppingList 的属性，_ShoppingListState 可以使用其小部件属性。如果父组件重新构建并创建新的 ShoppingList ， _ShoppingListState 将使用新的小部件值重新构建。如果希望在小部件属性发生更改时得到通知，可以覆盖 didUpdateWidget 函数，该函数传递给 oldWidget ，使您可以将旧小部件与当前小部件进行比较。)

When handling the `onCartChanged` callback, the `_ShoppingListState` mutates its
internal state by either adding or removing a product from `_shoppingCart`. To
signal to the framework that it changed its internal state, it wraps those calls
in a [setState]({{api}}/widgets/State-class.html#setState) call. Calling
[setState]({{api}}/widgets/State-class.html#setState) marks this widget as
dirty and schedules it to be rebuilt the next time your app needs to update the
screen. If you forget to call
[setState]({{api}}/widgets/State-class.html#setState) when modifying the
internal state of a widget, the framework won't know your widget is dirty and
might not call the widget's
[build]({{api}}/widgets/StatelessWidget/build.html) function, which means the
user interface might not update to reflect the changed state.
(在处理 onCartChanged 回调时，_ShoppingListState 通过从 _shoppingCart 中添加或删除产品来改变其内部状态。为了向框架发出更改其内部状态的信号，它将这些调用包装在一个 setState 调用中。调用 setState 会将此小部件标记为 dirty ，并将其安排在下一次应用程序需要更新屏幕时重新构建。如果您在修改小部件的内部状态时忘记调用 setState ，框架将不会知道您的小部件是脏的，并且可能不会调用小部件的构建函数，这意味着用户界面可能不会更新以反映更改后的状态。)

By managing state in this way, you don't need to write separate code for
creating and updating child widgets. Instead, you simply implement the build
function, which handles both situations.
(通过以这种方式管理状态，您不需要编写单独的代码来创建和更新子部件。相反，您只需实现构建函数，它将处理这两种情况。)

## Responding to widget lifecycle events

After calling
[createState]({{api}}/widgets/StatefulWidget-class.html#createState) on the
StatefulWidget, the framework inserts the new state object into the tree and
then calls [initState]({{api}}/widgets/State-class.html#initState) on the
state object. A subclass of [State]({{api}}/widgets/State-class.html) can
override [initState]({{api}}/widgets/State-class.html#initState) to do work
that needs to happen just once. For example, you can override
[initState]({{api}}/widgets/State-class.html#initState) to configure
animations or to subscribe to platform services. Implementations of
[initState]({{api}}/widgets/State-class.html#initState) are required to start
by calling [super.initState]({{api}}/widgets/State-class.html#initState).
(在 StatefulWidget 上调用 createState 之后，框架将新的状态对象插入树中，然后在状态对象上调用 initState 。State 的子类可以覆盖 initState 来执行只需要执行一次的工作。例如，您可以覆盖 initState 来配置动画或订阅平台服务。initState 的实现需要从调用 super.initState 开始。)

When a state object is no longer needed, the framework calls
[dispose]({{api}}/widgets/State-class.html#dispose) on the state object. You
can override the [dispose]({{api}}/widgets/State-class.html#dispose) function
to do cleanup work. For example, you can override
[dispose]({{api}}/widgets/State-class.html#dispose) to cancel timers or to
unsubscribe from platform services. Implementations of
[dispose]({{api}}/widgets/State-class.html#dispose) typically end by calling
[super.dispose]({{api}}/widgets/State-class.html#dispose).
(当不再需要状态对象时，框架调用该状态对象的 dispose 。您可以覆盖 dispose 函数来执行清理工作。例如，您可以覆盖 dispose 来取消计时器或从平台服务取消订阅。dispose 的实现通常以调用 super.dispose 结束。)

More information: [State]({{api}}/widgets/State-class.html)

## Keys

You can use keys to control which widgets the framework matches up with other
widgets when a widget rebuilds. By default, the framework matches widgets in the
current and previous build according to their
[runtimeType]({{api}}/widgets/Widget-class.html#runtimeType) and the order in
which they appear. With keys, the framework requires that the two widgets have
the same [key]({{api}}/widgets/Widget-class.html#key) as well as the same
[runtimeType]({{api}}/widgets/Widget-class.html#runtimeType).
(当小部件重新构建时，您可以使用键来控制框架与其他小部件匹配的小部件。默认情况下，框架根据当前和以前构建中的小部件的运行时类型和它们出现的顺序匹配它们。对于 key ，框架要求两个小部件具有相同的键和相同的运行时类型。)

Keys are most useful in widgets that build many instances of the same type of
widget. For example, the `ShoppingList` widget, which builds just enough
`ShoppingListItem` instances to fill its visible region:
(键在构建许多相同类型的小部件实例的小部件中最有用。例如，ShoppingList 小部件构建的 ShoppingListItem 实例刚好足以填充其可见区域)

 * Without keys, the first entry in the current build would always sync with the
   first entry in the previous build, even if, semantically, the first entry in
   the list just scrolled off screen and is no longer visible in the viewport.
   (如果没有键，当前构建中的第一个条目将始终与前一个构建中的第一个条目同步，即使从语义上讲，列表中的第一个条目刚刚从屏幕上滚动，并且在视图中不再可见。)

 * By assigning each entry in the list a "semantic" key, the infinite list can
   be more efficient because the framework syncs entries with matching
   semantic keys and therefore similar (or identical) visual appearances.
   Moreover, syncing the entries semantically means that state retained in
   stateful child widgets remains attached to the same semantic entry rather
   than the entry in the same numerical position in the viewport.
(通过为列表中的每个条目分配一个“语义”键，无限列表可以变得更高效，因为框架使用匹配的语义键同步条目，因此具有相似(或相同)的视觉外观。此外，从语义上同步条目意味着有状态子部件中保留的状态仍然附加到相同的语义条目，而不是视图中处于相同数值位置的条目。)

More information: [Key API]({{api}}/foundation/Key-class.html)

## Global Keys

You can use global keys to uniquely identify child widgets. Global keys must be
globally unique across the entire widget hierarchy, unlike local keys which need
only be unique among siblings. Because they are globally unique, a global key
can be used to retrieve the state associated with a widget.
(您可以使用全局键来惟一地标识子部件。全局键在整个小部件层次结构中必须是全局唯一的，不像本地键只需要在兄弟节点之间是唯一的。因为全局键是惟一的，所以可以使用全局键检索与小部件关联的状态。)

More information: [GlobalKey API]({{api}}/widgets/GlobalKey-class.html)

[runApp()]: {{api}}/widgets/runApp.html

