---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# Setup

**要求**
- [Unity 2019.4.31f1](https://unity3d.com/get-unity/download/archive)
- [VRCSDK3 + Udon](https://vrchat.com/home/download)

**安装**

你可以通过以下方式获取 UdonSharp：  
使用 [VRChat Creator Companion](https://vcc.docs.vrchat.com/)（简称 VCC）、它的 [CLI](https://vcc.docs.vrchat.com/vpm/cli/) 或者使用一个 [项目模板](https://github.com/vrchat-community/template-udonsharp)。

## 使用 VCC 创建一个新的 UdonSharp 项目：
- 安装最新版本的 [Creator Companion](https://vrchat.com/home/download)。
- 在主界面中选择 “New”，然后选择 “UdonSharp”，并选择一个目录。
- 点击 “Open Project”。就是这么简单！

## 通过源码管理创建新的 UdonSharp 项目：
- 访问 [UdonSharp Project Template 仓库](https://github.com/vrchat-community/template-udonsharp)。
- 点击 “Use this template”。
- 使用你喜欢的 Git 客户端将项目克隆到本地。
- 直接用 Unity 打开项目，或者将其添加到 VCC 以便之后轻松访问和更新。

## 将 UdonSharp 添加到现有的 Udon 项目：
- 将项目添加到 VCC，如果需要会自动迁移。
- 在项目列表界面选择此项目。
- 在包列表上方的 Repo 下拉菜单中，确保选择 “Curated”。
![image](/udonsharp.docs.vrchat.com/images/repos-official-curated.png)
- 在列表中找到 UdonSharp 并点击 “Add”。

## 使用 CLI 创建或添加 UdonSharp
[CLI](https://vcc.docs.vrchat.com/vpm/cli/) 是一个面向高级用户的工具，也是目前在非 Windows 系统上管理 VPM 项目的最佳方式。
- [使用模板创建新项目](https://vcc.docs.vrchat.com/vpm/cli/#new)
- [向项目添加包](https://vcc.docs.vrchat.com/vpm/cli/#add-package)

**开始使用**

1. 在场景中新建一个物体
2. 为物体添加 Udon Behaviour 组件
3. 在 "New Program" 按钮下方点击下拉框并选择 "Udon C# Program Asset"
4. 点击 New Program 按钮，这会为你创建一个新的 UdonSharp 程序资源
5. 点击 Create Script 按钮，并选择保存位置与脚本名称
6. 系统会创建一个可立即开始使用的模板脚本，用你喜欢的编辑器打开并开始编写代码

**从资源管理器中创建资产**

除了从 UdonBehaviour 上创建资产，你也可以：
1. 在项目资源管理器中右键
2. 选择 Create > U# script
3. 点击 U# script，这会打开创建文件对话框
4. 输入脚本名称并点击保存
5. 系统会在同一目录创建一个 .cs 脚本文件以及一个已配置好的 UdonSharp 程序资源
