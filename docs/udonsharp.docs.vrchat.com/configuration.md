---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# 配置

所有这些设置都可以在 `编辑 > 项目设置 > Udon Sharp` 中找到。

![Udon Sharp 设置](/udonsharp.docs.vrchat.com/images/udon-sharp-settings.png)

# Udon Sharp

### 修改时自动编译
启用后，当文件被修改并保存时，脚本会自动编译。

### 编译所有脚本
每当检测到 U# 脚本有变化时，会编译所有脚本。

### 聚焦时编译
仅在编辑器获得焦点且脚本有改动时才会编译。

### 脚本模板覆盖
你可以定义自己的自定义模板，用于创建 U# 脚本时。  
方法是将一个脚本拖入 `Script template override` 字段，这个模板将被用于创建新的 U# 脚本。

`<TemplateClassName>` 可以用来根据文件名设置类名。

**默认模板**
```cs
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

public class <TemplateClassName> : UdonSharpBehaviour
{
    void Start()
    {
        
    }
}
```

# 调试

### 调试构建

启用或禁用 `Inline Code` 和 `Listen for client exceptions`

### 内联代码（Inline Code）

在生成的汇编代码中包含 C# 内联代码。

### 监听客户端异常（Listen for client exceptions）

此选项会监听 VRChat 客户端输出日志中的异常，然后尝试将其与项目中的脚本匹配。

[点击这里了解更多设置方法](https://github.com/vrchat-community/UdonSharp/wiki/class-exposure-tree)
