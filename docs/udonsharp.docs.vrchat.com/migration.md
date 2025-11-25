---
UpstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# 迁移

UdonSharp 0.x（.unitypackage 版本）已被弃用，不再支持。  
新版本可以通过 [Creator Companion](https://vcc.docs.vrchat.com) 轻松获取，同时它会帮助你保持更新。  
我们推荐使用 [Creator Companion 迁移你的项目](https://vcc.docs.vrchat.com/vpm/migrating)。  
如果你希望手动迁移，请阅读 [手动迁移](#manual-migration)。

## UdonSharp 1.0 的新功能
* **更多 C# 功能** 可在 UdonSharp 脚本中使用：
	* `static` 方法
	* 泛型 `static` 方法
	* `params`、`out`、`ref` 和默认参数
	* 扩展方法
	* 继承、虚方法和抽象类
	* 部分类（Partial class）
	* 枚举（Enum）
- **多选编辑**：可在 Unity Inspector 中同时编辑多个 UdonSharp 脚本
- **Prefab 变体**、**实例化** 及 **嵌套** 现已完全支持
- **编辑器脚本** 已重构并简化
- **编译器修复** 与 **优化**
- 修复了各种 **bug**、边缘情况以及其他问题

## 已知问题

### 嵌套 Prefab

**问题**：UdonSharp 以前总是警告不要使用嵌套 Prefab，现在在某些情况下会彻底失效。

**表现**：错误信息类似 `Cannot upgrade scene behaviour 'SomethingOrOther' since its prefab must be upgraded`

**解决方法**：先在 0.x UdonSharp 项目中解包 Prefab。  
你也可以打开 "Udon Sharp" 菜单，选择 "Force Upgrade"。

### 不属于 U# Assembly

**问题**：带有自己 Assembly Definition 的库，也需要创建对应的 U# Assembly Definition。

**表现**：错误信息类似 `[UdonSharp] Script 'Assets/MyScript.cs' does not belong to a U# assembly, have you made a U# assembly definition for the assembly the script is a part of?`

**解决方法**：
1. 在 Project 窗口中找到脚本所在目录或父目录中以 `.asmdef` 结尾的文件。
2. 在该目录右键选择 `Create > U# Assembly Definition`。
3. 选择新建的 U# asmdef，在 Inspector 中将 “Source Assembly” 设置为其他 Assembly Definition 文件。
4. 完成后可能需要重启 Unity。

### Newtonsoft.Json.Dll

**问题**：某些包自带 JSON 库副本，而 VRCSDK 也会引入该库，导致库重复。

**表现**：控制台出现与该库相关的错误。例如：
`System.TypeInitializationException: the type initializer for blah blah blah...Assets/SketchfabForUnity/Dependencies/Libraries/Newtonsoft.Json.dll`

**解决方法**：删除 Assets 文件夹中所有 Newtonsoft.Json.dll 副本，VRCSDK 会通过 Package Manager 为需要的包提供该库。

### 其他破坏性更改
- U# 行为名称必须与 .cs 文件名匹配
- 重复的 Program Asset 不可引用相同的 `.cs` 文件
- Program Asset 必须指向脚本，不可为空
- 编辑器脚本机制已更改：数据由 UdonSharpBehaviour 的 C# 代理拥有，对应的 UdonBehaviour 在运行时前为空
- station 和 player join 事件的过时重载不可再使用

## 手动迁移

若不使用 Creator Companion 升级低于 1.0 的 UdonSharp 项目，请按以下步骤操作：

1. 备份项目。
2. 删除项目 `Assets` 文件夹中的 VRCSDK、Udon、UdonSharp 以及 Gizmos/UdonSharp 文件夹。
3. 下载并安装 [Unity Package 版本的 World SDK](https://vrchat.com/download/sdk3-worlds)。
4. 下载并安装 [Unity Package 版本的 UdonSharp SDK](https://github.com/vrchat-community/UdonSharp/releases/download/1.1.7/com.vrchat.udonsharp-1.1.7.unitypackage)。
