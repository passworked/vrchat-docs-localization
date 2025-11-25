---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# 常见问题

### 问题列表
* [UdonSharp 支持 X 功能吗？](#udonsharp-支持-x-功能吗)
* [Prefab 是否完全支持？](#prefab-是否完全支持)
* [我可以访问玩家摄像头吗？](#我可以访问玩家摄像头吗)
* [一个 GameObject 上可以有多个 UdonSharp Udon Behaviour 吗？](#一个-gameobject-上可以有多个-udonsharp-udon-behavior-吗)
* [我从零开始，需要使用 C# 教程。UdonSharp 中 C# 的哪些常用特性无法使用？](#我从零开始-需要使用-c-教程-udonsharp-中-c-的哪些常用特性无法使用)

---

### UdonSharp 支持 X 功能吗？
如果 Udon 支持该功能，UdonSharp 也同样支持。

_参考 [Class exposure tree](https://github.com/Merlin-san/UdonSharp/wiki/class-exposure-tree)_

### Prefab 是否完全支持？
你可以在 Udon 和 U# 中使用 Prefab，但由于 Unity 的限制，对 Prefab 的序列化字段修改不会正确传播到其实例上。

### 我可以访问玩家摄像头吗？
不可以直接访问玩家摄像头。不过，你可以获取玩家头部的位置和旋转。

参考 [VRCPlayerApi.GetTrackingData](https://github.com/Merlin-san/UdonSharp/wiki/vrchat-api#vrchatplayerapi)

```cs
Vector3 headPos = localPlayer.GetTrackingData(TrackingData.Head).position;
````

### 一个 GameObject 上可以有多个 UdonSharp Udon Behaviour 吗？

可以。

### 我从零开始，需要使用 C# 教程。UdonSharp 中 C# 的哪些常用特性无法使用？

如果你正在学习 UdonSharp 并且不熟悉 C#，你可能会遇到一些在 Udon 和 UdonSharp 中无法使用的常用技巧，包括但不限于：

* Unity 未定义的枚举（Enums）
* 泛型类 (`Class<T>`) 和方法
* 继承（Inheritance）
* 接口（Interfaces）
* 方法重载（Method overloads）
* 属性（Properties）

更多无法使用的 C# 特性，请参考 UdonSharp [readme](https://github.com/Merlin-san/UdonSharp/blob/master/README.md#c-features-supported)。