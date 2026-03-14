# iOS Navigation Demo

## 简介

展示 UINavigationController 的用法：页面导航。

## 启动和使用

在 Xcode 中打开 `ios-navigation-demo.xcodeproj`，运行即可。

## 教程

### 创建导航控制器

```swift
let rootVC = FirstViewController()
let navController = UINavigationController(rootViewController: rootVC)
window?.rootViewController = navController
```

### 页面跳转

```swift
navigationController?.pushViewController(secondVC, animated: true)
navigationController?.popViewController(animated: true)
```
