# iOS Navigation Demo

## 简介

本 Demo 展示 UINavigationController 的用法，实现页面之间的导航跳转。UINavigationController 是 iOS 中最常用的导航控件，几乎每个应用都会用到。

## 基本原理

UINavigationController 是 UIKit 框架中管理视图控制器层次结构的容器控件，其核心机制包括：

1. **导航栈**：维护一个视图控制器栈结构，支持 push（入栈）和 pop（出栈）
2. **根视图控制器**：栈底的第一个视图控制器
3. **导航栏**：自动显示顶部导航条，显示标题和返回按钮
4. **动画效果**：页面切换时有系统默认的滑动动画

## 教程

### 1. 创建导航控制器

```swift
let rootVC = FirstViewController()
let navController = UINavigationController(rootViewController: rootVC)
window?.rootViewController = navController
```

### 2. 设置导航栏标题

```swift
// 在视图控制器中设置
title = "第一页"

// 或使用导航项
navigationItem.title = "自定义标题"
```

### 3. 页面跳转 - Push

```swift
// 跳转到下一页
let secondVC = SecondViewController()
navigationController?.pushViewController(secondVC, animated: true)
```

### 4. 页面返回 - Pop

```swift
// 返回上一个页面
navigationController?.popViewController(animated: true)

// 返回到根视图控制器
navigationController?.popToRootViewController(animated: true)
```

### 5. 导航栏样式设置

```swift
// 导航栏背景色
navigationController?.navigationBar.prefersLargeTitles = true

// 导航项
navigationItem.rightBarButtonItem = UIBarButtonItem(title: "编辑", style: .plain, target: self, action: #selector(editTapped))
```

## 关键代码详解

本 Demo 创建了两个视图控制器，实现页面间的导航跳转：

### FirstViewController

```swift
class FirstViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .systemBlue
        title = "第一页"
        setupUI()
    }
```

**关键点**：
- `view.backgroundColor = .systemBlue`：设置页面背景色为蓝色
- `title = "第一页"`：设置导航栏标题

### 跳转实现

```swift
@objc private func goToSecond() {
    let secondVC = SecondViewController()
    navigationController?.pushViewController(secondVC, animated: true)
}
```

**代码解析**：
- 创建目标视图控制器实例
- 使用 `pushViewController` 方法将新页面压入栈中
- `animated: true` 启用滑动动画效果

### 按钮创建

```swift
let button = UIButton(type: .system)
button.setTitle("跳转到第二页", for: .normal)
button.setTitleColor(.white, for: .normal)
button.titleLabel?.font = .systemFont(ofSize: 20)
button.translatesAutoresizingMaskIntoConstraints = false
button.addTarget(self, action: #selector(goToSecond), for: .touchUpInside)
```

**说明**：
- 设置按钮文字为白色以在蓝色背景上显示清晰
- 字体大小设为 20pt
- 使用目标-动作模式处理点击事件

### SecondViewController

```swift
class SecondViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .systemGreen
        title = "第二页"
    }
}
```

**说明**：
- 绿色背景区别于第一页
- 标题自动显示在导航栏上
- 不需要额外设置返回按钮，导航控制器会自动添加

### 导航控制器的工作原理

1. **初始化时**：导航控制器创建时会自动添加返回按钮到第二个及后续页面
2. **点击返回**：用户点击返回按钮时，自动调用 `popViewController`
3. **栈管理**：导航控制器维护一个视图控制器栈，push 增加栈深度，pop 减少栈深度

## 运行效果

1. 应用启动后显示蓝色背景的第一页，导航栏标题为"第一页"
2. 屏幕中央显示"跳转到第二页"按钮
3. 点击按钮后，页面从右向左滑动切换到绿色背景的第二页
4. 第二页导航栏自动显示返回按钮
5. 点击返回按钮，页面从左向右滑回第一页
