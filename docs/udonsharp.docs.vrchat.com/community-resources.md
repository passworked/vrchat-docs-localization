---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

<!-- zhlint disabled -->

# Community Resources（社区资源）

## Tutorials and info（教程与资料）

### はつぇさん的博客
- [U# 入门 ①](https://hatuxes.hatenablog.jp/entry/2020/04/05/013310)
- [U# 入门 ②](https://hatuxes.hatenablog.jp/entry/2020/04/05/013323)
- [U# 入门 ③](https://hatuxes.hatenablog.jp/entry/2020/04/05/013336)
- [U# 入门 额外篇](https://hatuxes.hatenablog.jp/entry/2020/04/05/013348)

### やぎりさん的博客
- [UdonSharp 笔记（撰写中，持续更新）](https://yagiri000.hatenablog.com/entry/2020/04/04/162312)

### Vowgan 的教程视频

这些视频前半部分讲解图形编程（Udon Graph），后半部分讲解 UdonSharp。
- [VRChat Udon 教程 | 基础按钮](https://www.youtube.com/watch?v=GWv3zloRWY4)
- [VRChat Udon 教程 | 上下文按钮](https://www.youtube.com/watch?v=01a5qO60qlo)
- [VRChat Udon 教程 | 跳跃与玩家属性修改](https://www.youtube.com/watch?v=OventaglGCY)

## Tools（工具）

### orels1 的 UdonToolKit
提供一系列实用的工具性行为（utility behaviours）以及更高级的 attribute 系统，用于为 U# 脚本制作自定义 Inspector。

https://github.com/orels1/UdonToolkit/

### cannorin 的 extern search
由于节点注册表很久未更新，这个工具现在已经有些过时。  
这是一个网页工具，可用来搜索 Udon 目前可用的函数。

https://7colou.red/UdonExternSearch/

### CyanEmu
CyanEmu 是一个 VRChat 客户端模拟器，可让你在 Unity 中直接测试和调试 Udon（以及 SDK2）世界。  
它提供桌面玩家控制器，可执行交互、抓取、坐下、回出生点等模拟操作。

https://github.com/CyanLaser/CyanEmu

### Phasedragon 的输入表（Input Table）

该表列出了 VRChat 当前绑定的所有输入，并说明它们在不同 VR 控制器上的行为方式。  
返回 true/false 的输入可通过 `Input.GetButton()` 获取；  
返回 -1~1 或 0~1 的输入可通过 `Input.GetAxis()` 或 `Input.GetAxisRaw()` 获取。

https://docs.google.com/spreadsheets/d/1_iF0NjJniTnQn-knCjb5nLh6rlLfW_QKM19wtSW_S9w/edit#gid=1150012376

如果你想测试不在表中的控制器，可以访问此输入测试世界：

https://vrchat.com/home/world/wrld_f8d5f7e4-185c-4b82-8ecb-8ae0c7953085

### Shatoo 的 Udon 编辑器调试器
提供一个 UI，可用来调用内置事件并传入参数。

https://shatoo.booth.pm/items/1958756

### Jordo 的触觉反馈测试世界（Haptics Testing World）
提供三个滑块用于调整触觉强度，并可以立即测试效果，方便之后在代码中应用。

https://vrchat.com/home/launch?worldId=wrld_7f010f63-7a82-4668-b1a5-412b57fb08f5&instanceId=0
