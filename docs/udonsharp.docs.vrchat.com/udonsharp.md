---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# UdonSharp

# 属性

UdonSharp 中支持的所有属性

|                                                                                 | 属性                                                                                  |                                                                                      |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [Header](https://docs.unity3d.com/ScriptReference/HeaderAttribute.html)         | [HideInInspector](https://docs.unity3d.com/ScriptReference/HideInInspector.html)      | [NonSerialized](https://docs.microsoft.com/dotnet/api/system.nonserializedattribute) |
| [SerializeField](https://docs.unity3d.com/ScriptReference/SerializeField.html)  | [Space](https://docs.unity3d.com/ScriptReference/SpaceAttribute.html)                 | [Tooltip](https://docs.unity3d.com/ScriptReference/TooltipAttribute.html)            |
| [ColorUsage](https://docs.unity3d.com/ScriptReference/ColorUsageAttribute.html) | [GradientUsage](https://docs.unity3d.com/ScriptReference/GradientUsageAttribute.html) | [TextArea](https://docs.unity3d.com/ScriptReference/TextAreaAttribute.html)          |
| [UdonSynced](#udonsynced)                                                       | [DefaultExecutionOrder](#defaultexecutionorder)                                       | [UdonBehaviourSyncMode](#udonbehavioursyncmode)                                      |
| [RecursiveMethod](#recursivemethod)                                             | [FieldChangeCallback](#fieldchangecallback)                                           |

## UdonSynced
`[UdonSynced]` / `[UdonSynced(UdonSyncMode)]`

*查看 [同步变量](/udonsharp.docs.vrchat.com/vrchat-api#synced-variables) 获取可同步的变量。*

### 示例
```cs
public class Example : UdonSharpBehaviour 
{
    [UdonSynced]
    public bool synchronizedBoolean;

    [UdonSynced(UdonSyncMode.Linear)]
    // 此 float 将以线性方式插值
    public float synchronizedFloat;
}
```

### UdonSyncMode

`UdonSharp.UdonSyncMode`

| 名称        | 描述         |
| --------- | ---------- |
| NotSynced | 未同步        |
| None      | 无插值（默认）    |
| Linear    | 线性插值       |
| Smooth    | *某种平滑同步方式* |

## UdonBehaviourSyncMode

`[UdonBehaviourSyncMode]` / `[UdonBehaviourSyncMode(BehaviourSyncMode)]`

强制使用指定的同步模式，并在适当情况下对同步变量执行额外验证。

### 示例

```cs
[UdonBehaviourSyncMode(BehaviourSyncMode.Manual)]
public class Example : UdonSharpBehaviour 
{ 
}
```

### BehaviourSyncMode

`UdonSharp.BehaviourSyncMode`

| 名称             | 描述                                                                         |
| -------------- | -------------------------------------------------------------------------- |
| Any            | 不强制同步模式，用户可自行选择同步类型。当未指定属性时为默认值。                                           |
| None           | 不同步任何变量，并隐藏 UI 中的同步模式选择下拉框。此行为下 SendCustomNetworkEvent 无法使用。               |
| Continuous     | 同步变量会以非常频繁的速率自动更新，但为了节省带宽可能并非总是可靠。                                         |
| Manual         | 同步变量由用户手动更新，更新频率较低，但确保在请求时更新可靠。                                            |
| NoVariableSync | 强制该行为上无同步变量，隐藏同步模式选择下拉框，同时允许在使用 Manual 或 Continuous 同步的 GameObject 上使用该行为。 |

## DefaultExecutionOrder

指定 Update、LateUpdate 和 FixedUpdate 的执行顺序，相对于其他 UdonSharpBehaviour 的顺序。默认值为 0，数值越小，更新越早。数值可以为负。

### 示例

```cs
[DefaultExecutionOrder(0)]
public class Example : UdonSharpBehaviour 
{ 
}
```

## RecursiveMethod

`[RecursiveMethod]`

标记一个方法可以递归调用。被标记的方法可以安全地在同一行为中调用自身。该属性会增加性能开销，因此仅在确实需要递归调用的方法上使用。

### 示例

```cs
[RecursiveMethod]
int Factorial(int input)
{
    if (input == 1)
        return 1;

    return input * Factorial(input - 1);
}
```

## FieldChangeCallback

`[FieldChangeCallback(string)]`

用于在字段上设置，以便接收 Udon 变量变化事件。此属性接受一个字符串参数，该参数指向行为中的属性名。当此属性设置在字段上时，通过网络同步或 SetProgramVariable 修改字段会调用目标属性的 setter，而不是直接修改字段。通常属性会在 setter 中设置该字段。

### 示例

```cs
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

[UdonBehaviourSyncMode(BehaviourSyncMode.Manual)]
public class ExampleOfFieldChangeCallback: UdonSharpBehaviour
{
    public GameObject toggleObject;

    [UdonSynced, FieldChangeCallback(nameof(SyncedToggle))]
    private bool _syncedToggle;

    public bool SyncedToggle
    {
        set
        {
            Debug.Log("toggling the object...");
            _syncedToggle = value;
            toggleObject.SetActive(value);
        }
        get => _syncedToggle;
    }

    public override void Interact()
    {
        Networking.SetOwner(Networking.LocalPlayer, gameObject);
        SyncedToggle = !SyncedToggle;
        RequestSerialization();
    }
}
```

注意，上例中 Interact 执行的是 `SyncedToggle = !SyncedToggle;` 而不是 `_syncedToggle = !_syncedToggle`。后者无法触发 FieldChangeCallback。FieldChangeCallback 只会在 SetProgramVariable 或网络同步更新同步变量时触发属性的 setter。不要直接在同一 UdonBehaviour 内部修改字段，应始终使用属性或显式使用 SetProgramVariable。UdonSharp 会故意在尝试从行为外部设置 `_syncedToggle` 时编译失败。