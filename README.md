[合集 \- energy(2\)](https://github.com)[1\.energy 发布 v2\.4\.511\-04](https://github.com/energye/p/18526896):[樱花宇宙官网](https://yzygzn.com)2\.系统托盘创建11\-08收起
@"von"\#p7
你好，如果你说的是仅使用托盘不显示窗口情况有多种使用方式和实现。
以下提及两种使用


1. 在windows下使用`lcl+cef`网页托盘，在这种情况下主窗口是需要创建和初始化，目前energy初始化时有一些必要的功能，因此 `lcl+cef` 网页托盘需要这些功能。
实际这种效果，如果你对框架有深层次了解完全可以抛开主窗口，而自己实现单独仅使用网页托盘。
当前解决办法：主窗口初始化时设置它的 x 和 y 坐标到屏幕之外创建完之后隐藏掉它，例如窗口大小是 800x600, x\=\-800, y\=\-600。
2. 纯原生lcl系统托盘，在 `cef.BrowserWindow.SetBrowserInit` 回调函数内设置主窗口隐藏 `lcl.Application.SetShowMainForm(false)`
这时如果退出应用默认的`close`或`CloseBrowserWindow`函数将不起作用。需要调用`lcl.Application.Terminate()`退出应用


在windows下如果自己实现`lcl+cef`托盘，且仅有托盘功能。
把主窗口做为托盘页面。此时你可能需要根据需求设置窗口的默认隐藏。
然后创建lcl原生托盘，在托盘功能事件里管理主窗口，控制托盘显示和隐藏等等，可以参考 `lclcef` 托盘实现源码。


