---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# UdonSharp

## 一个将 C# 编译为 Udon 汇编的编译器

UdonSharp 是一个将 C# 编译为 Udon 汇编的编译器。UdonSharp 当前并未完全符合任何版本的 C# 语言规范，因此有许多功能尚未实现或无法正常工作。

## 已支持的 C# 功能
- 流程控制  
    - 支持：`if` `else` `while` `for` `do` `foreach` `switch` `return` `break` `continue` `三元运算符 (condition ? true : false)` `??`
- 隐式与显式类型转换
- 数组与数组索引器
- 所有内置算术运算符
- 条件短路（例如 `(true || CheckIfTrue())` 不会执行 CheckIfTrue()）
- `typeof()`
- 带有 out/ref 参数的外部方法（如许多 `Physics.Raycast()` 的变体）
- 用户自定义方法（带参数与返回值），支持 out/ref、扩展方法与 `params`
- 用户自定义属性
- 静态用户方法
- UdonSharpBehaviour 继承、虚方法等特性
- 带参数的 Unity/Udon 事件回调。例如，注册一个带 VRCPlayerApi 参数的 OnPlayerJoined 事件是有效的。
- 字符串插值
- 字段初始化器
- 交错数组（Jagged arrays）
- 引用其他自定义 UdonSharpBehaviour 类、访问字段、调用方法
- 通过 `[RecursiveMethod]` 属性支持递归方法调用

## 与常规 Unity C# 的差异
- 为获得最佳体验，请让脚本继承自 `UdonSharpBehaviour` 而不是 `MonoBehaviour`
- 如果你需要调用 `GetComponent<UdonBehaviour>()`，目前必须写成 `(UdonBehaviour)GetComponent(typeof(UdonBehaviour))`，因为泛型 GetComponent 版本暂未对 UdonBehaviour 暴露。对其他 Unity 组件类型则可以正常使用 `GetComponent<T>()`。
- Udon 当前只支持数组 `[]` 集合，因此 UdonSharp 目前也仅支持数组。看起来未来可能支持 `List<T>`，但现在还不行。
- 字段初始化器在编译期执行，如果初始化逻辑依赖场景中其他对象，你应在 Start 中处理。
- 使用 `UdonSynced` 属性标记你希望同步的字段。
- 由于 UdonVM 限制，数值类型转换会进行溢出检查。
- `.GetType()` 返回的变量内部类型可能不符合预期，因为 U# 会对一些类型做抽象以便在 Udon 中工作。例如，任何交错数组类型都会返回 `object[]`，而不是像 `int[][]` 这样的二维整型交错数组类型。

## 影响 U# 的 Udon Bug
- 结构体的可变方法不会修改结构体本身（例如调用 Vector3 的 Normalize() 无效）  
  https://vrchat.canny.io/vrchat-udon-closed-alpha-bugs/p/raysetorigin-and-raysetdirection-not-working

## 安装与配置

### 要求
- Unity 2019.4.31f1
- [VRCSDK3 + UdonSDK](https://vrchat.com/home/download)
- 最新版本的 UdonSharp（从 [release](https://github.com/vrchat-community/UdonSharp/releases/latest) 下载）

### 安装步骤
1. 阅读 Udon 的入门文档 /docs.vrchat.com/docs/getting-started-with-udon，其中包含基本安装步骤。
2. 安装入门文档中链接的最新版本 VRCSDK3。
3. 从 [这里](https://github.com/vrchat-community/UdonSharp/releases/latest) 获取 UdonSharp 最新版本并安装到你的项目中。

### 开始使用
1. 在场景中新建一个物体
2. 为该物体添加一个 `Udon Behaviour` 组件
3. 在 "New Program" 按钮下方点击下拉框并选择 "Udon C# Program Asset"
4. 点击 New Program 按钮，系统会为你创建一个新的 UdonSharp 程序资源
5. 点击 Create Script 按钮，选择保存目录和脚本名称
6. 系统会创建一个可供你开始编程的模板脚本，使用你的编辑器打开并开始编写代码

#### 在资源管理器中创建 U# 资源文件

除了从 UdonBehaviour 上创建资源外，你也可以：
1. 在项目资源管理器中右键
2. 选择 Create > U# script
3. 点击 U# script，这会打开创建文件对话框
4. 输入脚本名称并保存
5. 系统会在同一目录生成一个 .cs 脚本文件以及对应的 UdonSharp 程序资源

### 示例脚本

#### 旋转立方体示例

这个脚本会让它所在的物体每秒旋转 90 度

```cs
using UnityEngine;
using UdonSharp;

public class RotatingCubeBehaviour : UdonSharpBehaviour
{
    private void Update()
    {
        transform.Rotate(Vector3.up, 90f * Time.deltaTime);
    }
}
```

#### 其他示例

更多示例脚本请访问 wiki 的 [examples](https://github.com/Merlin-san/UdonSharp/wiki/examples) 页面、U# 附带的 Examples 文件夹，或 wiki 上的[社区资源页面](https://github.com/Merlin-san/UdonSharp/wiki/community-resources)。

## 鸣谢

* 贡献者请见 [CONTRIBUTORS.md](https://github.com/vrchat-community/UdonSharp/blob/master/CONTRIBUTORS.md)
* 开源项目 [Harmony](https://github.com/pardeike/Harmony) 帮助 UdonSharp 提供更优秀的编辑器体验

#

[![Discord](https://img.shields.io/badge/Discord-Merlin%27s%20Discord%20Server-blueviolet?logo=discord)](https://discord.gg/Ub2n8ZA)