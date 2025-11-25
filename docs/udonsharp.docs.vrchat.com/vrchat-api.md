---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# VRChat API

## API
### 方法
* [VRCInstantiate](#vrcinstantiate)

### 类
* [Utilities](#utilities)
* [VRCStation](#vrcstation)
* [Networking](#networking)
* [TrackingData](#trackingdata)
* [UdonBehaviour](#udonbehaviour)
* [VRCPlayerApi](#vrcplayerapi)
* [InputManager](#inputmanager)
* [SerializationResult](#inputmanager)
* [UdonInputEventArgs](#udoninputeventargs)
* [VRCUrl](#vrcurl)
* [VRCUrlInputField](#vrcurlinputfield)
* [VRCMirrorReflection](#vrcmirrorreflection)
* [VRCObjectPool](#vrcobjectpool)
* [VRCObjectSync](#vrcobjectsync)
* [VRCAvatarPedestal](#vrcavatarpedestal)
* [VRCPickup](#vrcpickup)
* [VRCPortalMarker](#vrcportalmarker)

### 枚举
* [EventTiming](#eventtiming)
* [Mobility](#mobility)
* [NetworkEventTarget](#networkeventtarget)
* [SpawnOrientation](#spawnorientation)
* [TrackingDataType](#trackingdatatype)
* [VRCInputMethod](#vrcinputmethod)
* [HandType](#handtype)
* [UdonInputEventType](#udoninputeventtype)
* [VideoError](#videoerror)
* [AutoHoldMode](#autoholdmode)
* [PickupOrientation](#pickuporientation)
* [PickupHand](#pickuphand)

## 支持的功能
* [Synced Variables](#synced-variables)

---

## 方法

### VRCInstantiate
| 静态 | 返回值                                                                 | 名称                                                                                             | 摘要                                                                                                                                            |
| :--: | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
|  ✔️   | [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) | VRCInstantiate([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) original) | 创建对象的本地非同步副本。更多信息请参见 [这里](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html)。 |



## 类

### Utilities
`static class VRC.SDKBase.Utilities`

方法
| 静态 | 返回值 | 名称                     | 摘要                                                                                                                                                                                                                                                     |
| :--: | ------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  ✔️   | bool   | IsValid(object obj)      | 如果指定对象有效且不是 null 引用，则返回 true，否则返回 false。通常用于检查玩家离开实例后的 [VRCPlayerApi](#vrcplayerapi) 对象，或已被销毁的 [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) 对象。 |
|  ✔️   | void   | ShuffleArray(int[] array) | 随机打乱数组中的每个元素。                                                                                                                                                                                                                              |

### VRCStation
`class VRC.SDK3.Components.VRCStation` / `class VRC.SDKBase.VRCStation`

属性
| 类型                                                                                                  | 名称                        | 摘要                                                                                                                                                            |
| ----------------------------------------------------------------------------------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Mobility](#mobility)                                                                                | PlayerMobility              | 决定玩家是否可以移动。默认值为 `VRCStation.Mobility.Immobilize`。                                                                                              |
| bool                                                                                                 | canUseStationFromStation    | 决定用户在坐在一个座位时是否可以切换到另一个座位。默认值为 `true`。                                                                                             |
| [RuntimeAnimatorController](https://docs.unity3d.com/ScriptReference/RuntimeAnimatorController.html) | animatorController          | 用于用自定义动画覆盖普通的坐下动画。                                                                                                                              |
| bool                                                                                                 | disableStationExit          | 如果用户无法通过常规方式离开座位，可以使用触发器让用户下座。                                                                                                     |
| bool                                                                                                 | seated                      | 这是用户应该坐的座位吗？默认值为 `true`。更多信息请参见 [这里](/creators.vrchat.com/worlds/components/vrc_station)。                                            |
| [Transform](https://docs.unity3d.com/ScriptReference/Transform.html)                                 | stationEnterPlayerLocation  | 用于定义用户坐下时应该传送到的位置的 Transform                                                                                                                   |
| [Transform](https://docs.unity3d.com/ScriptReference/Transform.html)                                 | stationExitPlayerLocation   | 用于定义用户下座时应该传送到的位置的 Transform                                                                                                                   |

方法
| 返回值 | 名称                                               | 摘要             |
| ------ | ------------------------------------------------- | ---------------- |
| void   | UseStation([VRCPlayerApi](#vrcplayerapi) player)  | 使用座位         |
| void   | ExitStation([VRCPlayerApi](#vrcplayerapi) player) | 离开座位         |

### Networking
`static class VRC.SDKBase.Networking`

属性
| 静态 | 类型                          | 名称             | 摘要                               |
| :--: | ----------------------------- | ---------------- | --------------------------------- |
|  ✔️   | bool                          | isMaster         | 返回本地玩家是否为实例的 Master  |
|  ✔️   | [VRCPlayerApi](#vrcplayerapi) | LocalPlayer      | 返回当前玩家                       |
|  ✔️   | bool                          | IsNetworkSettled | 返回网络是否准备就绪               |

方法
| 静态 | 返回值                                                           | 名称                                                                                                                       | 摘要                                                                                             |
| :--: | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
|  ✔️   | bool                                                              | IsOwner([VRCPlayerApi](#vrcplayerapi) player, [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)  | 返回指定玩家是否为对象的所有者                                                                    |
|  ✔️   | bool                                                              | IsOwner([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                        | 返回本地玩家是否为对象的所有者                                                                    |
|  ✔️   | [VRCPlayerApi](#vrcplayerapi)                                     | GetOwner([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                       | 返回指定对象的所有者                                                                              |
|  ✔️   | void                                                              | SetOwner([VRCPlayerApi](#vrcplayerapi) player, [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj) | 将指定玩家设置为对象的所有者                                                                     |
|  ✔️   | bool                                                              | IsObjectReady([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                  | 返回对象是否已准备好                                                                              |
|  ✔️   | void                                                              | Destroy([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                        | 销毁指定对象                                                                                      |
|  ✔️   | string                                                            | GetUniqueName([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                  | 获取对象的唯一名称                                                                                 |
|  ✔️   | [DateTime](https://docs.microsoft.com/dotnet/api/system.datetime) | GetNetworkDateTime()                                                                                                       | 获取网络日期时间                                                                                   |
|  ✔️   | double                                                            | GetServerTimeInSeconds()                                                                                                   | 返回当前服务器时间（秒）                                                                           |
|  ✔️   | int                                                               | GetServerTimeInMilliseconds()                                                                                              | 返回当前服务器时间（毫秒）                                                                         |
|  ✔️   | double                                                            | CalculateServerDeltaTime(double timeInSeconds, double previousTimeInSeconds)                                               | 计算由 `GetServerTimeInSeconds()` 返回的两个服务器时间戳之间的差值                                    |

### TrackingData
`struct VRC.SDKBase.VRCPlayerApi.TrackingData`

属性
| 类型                                                                   | 名称     | 摘要                                      |
| ---------------------------------------------------------------------- | -------- | ---------------------------------------- |
| [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html)       | position | 玩家跟踪点的位置                          |
| [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) | rotation | 玩家跟踪点的旋转                          |

### UdonBehaviour
`class VRC.Udon.UdonBehaviour`

UdonBehaviour 可通过 `GetComponent` 获取。  
当前 *不支持* `GetComponent<T>()`：
```cs
UdonBehaviour behaviour = (UdonBehaviour)GetComponent(typeof(UdonBehaviour));
```

属性

| 类型   | 名称                 | 摘要                                          |
| ---- | ------------------ | ------------------------------------------- |
| bool | DisableInteractive | 决定带有 Interact 事件的对象是否接受指针射线检测，并显示可交互轮廓和提示信息 |

方法

| 返回值                                                       | 名称                                                                                                           | 摘要                                           |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------------------- |
| void                                                      | SendCustomEvent(string eventName)                                                                            | 运行 Behaviour 上的公共方法                          |
| void                                                      | SendCustomNetworkEvent([NetworkEventTarget](#networkeventtarget) target, string eventName)                   | 通过网络运行 Behaviour 上的公共方法                      |
| void                                                      | SendCustomEventDelayedSeconds(string eventName, float delaySeconds, [EventTiming](#eventtiming) eventTiming) | 在指定秒数后执行 Behaviour 上的自定义事件                   |
| void                                                      | SendCustomEventDelayedFrames(string eventName, int delayFrames, [EventTiming](#eventtiming) eventTiming)     | 在指定帧延迟后执行 Behaviour 上的自定义事件                  |
| object                                                    | GetProgramVariable(string symbolName)                                                                        | 获取 Behaviour 中的变量                            |
| void                                                      | SetProgramVariable(string symbolName, object value)                                                          | 设置 Behaviour 中的变量                            |
| [Type](https://docs.microsoft.com/dotnet/api/system.type) | GetProgramVariableType(string symbolName)                                                                    | 获取 Behaviour 中指定变量的类型                        |
| void                                                      | RequestSerialization()                                                                                       | 触发同步变量的数据序列化并发送给远程客户端。通常用于手动同步模式下的 Behaviour |

### VRCPlayerApi

`class VRC.SDKBase.VRCPlayerApi`

属性

| 类型     | 名称          | 摘要               |
| ------ | ----------- | ---------------- |
| bool   | isLocal     | 判断玩家是本地还是远程      |
| string | displayName | 玩家显示名称           |
| bool   | isMaster    | 判断玩家是否为实例 Master |
| int    | playerId    | 玩家实例 ID          |

方法

|  静态 | 返回值                                                                    | 名称                                                                                                                                                                           | 摘要                                                          |
| :-: | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
|     | bool                                                                   | IsPlayerGrounded()                                                                                                                                                           | 判断玩家是否在地面上                                                  |
|  ✔️ | int                                                                    | GetPlayerId([VRCPlayerApi](#vrcplayerapi) player)                                                                                                                            | 获取玩家实例 ID                                                   |
|  ✔️ | [VRCPlayerApi](#vrcplayerapi)                                          | GetPlayerById(int playerId)                                                                                                                                                  | 根据 ID 获取玩家                                                  |
|  ✔️ | int                                                                    | GetPlayerCount()                                                                                                                                                             | 返回实例中的玩家数量                                                  |
|  ✔️ | [VRCPlayerApi[]](#vrcplayerapi)                                        | GetPlayers([VRCPlayerApi[]](#vrcplayerapi) players)                                                                                                                          | 填充并返回实例中当前玩家数组。数组必须至少预分配 `VRCPlayerApi.GetPlayerCount` 个元素。 |
|     | bool                                                                   | IsOwner([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj)                                                                                          | 判断玩家是否拥有带 UdonBehaviour 的对象                                 |
|     | [TrackingData](#trackingdata)                                          | GetTrackingData([TrackingDataType](#trackingdatatype) tt)                                                                                                                    | 返回指定类型的跟踪数据                                                 |
|     | [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html)       | GetBonePosition([HumanBodyBones](https://docs.unity3d.com/ScriptReference/HumanBodyBones.html) bone)                                                                         | 获取指定骨骼位置数据                                                  |
|     | [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) | GetBoneRotation([HumanBodyBones](https://docs.unity3d.com/ScriptReference/HumanBodyBones.html) bone)                                                                         | 获取指定骨骼旋转数据                                                  |
|     | void                                                                   | TeleportTo([Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html) teleportPos, [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) teleportRot) | 将玩家传送到指定位置和旋转                                               |
|     | void                                                                   | TeleportTo([Vector3] teleportPos, [Quaternion] teleportRot, [SpawnOrientation](#spawnorientation) teleportOrientation)                                                       | 将玩家传送到指定位置、旋转和生成方向                                          |
|     | void                                                                   | TeleportTo([Vector3] teleportPos, [Quaternion] teleportRot, [SpawnOrientation] teleportOrientation, bool lerpOnRemote)                                                       | 将玩家传送到指定位置、旋转、生成方向，并选择远程是否使用插值                              |
|     | void                                                                   | EnablePickup(bool enable)                                                                                                                                                    | 设置玩家是否可以使用拾取物 (*需测试*)                                       |
|     | void                                                                   | SetPlayerTag(string tagName, string tagValue)                                                                                                                                | 为玩家设置标签值，未分配标签返回 null，标签不同步到远程客户端                           |
|     | string                                                                 | GetPlayerTag(string tagName)                                                                                                                                                 | 获取玩家标签值，将值设置为 null 可清除标签                                    |
|     | void                                                                   | ClearPlayerTags()                                                                                                                                                            | 清除玩家标签                                                      |
|     | void                                                                   | SetRunSpeed(float speed)                                                                                                                                                     | 设置玩家跑速                                                      |
|     | void                                                                   | SetWalkSpeed(float speed)                                                                                                                                                    | 设置玩家行走速度                                                    |
|     | void                                                                   | SetJumpImpulse(float impulse)                                                                                                                                                | 设置玩家跳跃冲量                                                    |
|     | void                                                                   | SetGravityStrength(float strength)                                                                                                                                           | 设置玩家重力                                                      |
|     | void                                                                   | SetStrafeSpeed(float speed)                                                                                                                                                  | 设置玩家横向移动速度，默认 2.0f                                          |
|     | float                                                                  | GetRunSpeed()                                                                                                                                                                | 获取当前跑速                                                      |
|     | float                                                                  | GetWalkSpeed()                                                                                                                                                               | 获取当前行走速度                                                    |
|     | float                                                                  | GetJumpImpulse()                                                                                                                                                             | 获取当前跳跃冲量                                                    |
|     | float                                                                  | GetGravityStrength()                                                                                                                                                         | 获取当前重力值                                                     |
|     | float                                                                  | GetStrafeSpeed()                                                                                                                                                             | 获取玩家横向移动速度                                                  |
|     | bool                                                                   | IsUserInVR()                                                                                                                                                                 | 判断当前用户是否在 VR 模式                                             |
|     | void                                                                   | UseLegacyLocomotion()                                                                                                                                                        | 使用旧版移动系统                                                    |
|     | void                                                                   | Immobilize(bool immobile)                                                                                                                                                    | 禁止玩家移动                                                      |
|     | void                                                                   | UseAttachedStation()                                                                                                                                                         | 玩家坐在附加的座位上 (需要 VRC_Station 在同一对象上)                          |
|     | void                                                                   | SetVelocity([Vector3] velocity)                                                                                                                                              | 设置玩家速度                                                      |
|     | [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html)       | GetVelocity()                                                                                                                                                                | 获取玩家速度                                                      |
|     | [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html)       | GetPosition()                                                                                                                                                                | 获取玩家位置                                                      |
|     | [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) | GetRotation()                                                                                                                                                                | 获取玩家旋转                                                      |
|     | void                                                                   | SetVoiceGain(float gain)                                                                                                                                                     | 设置玩家语音增益 (dB)，范围 0-24                                       |
|     | void                                                                   | SetVoiceDistanceNear(float near)                                                                                                                                             | 设置音量开始衰减的近距离半径，建议保持为 0 以保证真实感和空间化                           |
|     | void                                                                   | SetVoiceDistanceFar(float far)                                                                                                                                               | 设置玩家语音听觉范围结束距离，默认 25m，可降至 0 实现静音                            |
|     | void                                                                   | SetVoiceVolumetricRadius(float radius)                                                                                                                                       | 设置玩家语音体积化半径，默认为 0                                           |
|     | void                                                                   | SetVoiceLowpass(bool enabled)                                                                                                                                                | 控制远距离语音是否使用低通滤波                                             |
|     | void                                                                   | SetAvatarAudioGain(float gain)                                                                                                                                               | 设置 Avatar 音频最大增益，默认 10 dB                                   |
|     | void                                                                   | SetAvatarAudioNearRadius(float distance)                                                                                                                                     | 设置 Avatar 音频近距离范围，默认 40m                                    |
|     | void                                                                   | SetAvatarAudioFarRadius(float distance)                                                                                                                                      | 设置 Avatar 音频远距离范围，默认 40m                                    |
|     | void                                                                   | SetAvatarAudioVolumetricRadius(float radius)                                                                                                                                 | 设置 Avatar 音频体积化半径，默认 40m                                    |
|     | void                                                                   | SetAvatarAudioForceSpatial(bool force)                                                                                                                                       | 强制启用 Avatar 音频空间化                                           |
|     | void                                                                   | SetAvatarAudioCustomCurve(bool allow)                                                                                                                                        | 设置 Avatar 音频是否可使用自定义曲线                                      |
|     | void                                                                   | PlayHapticEventInHand([PickupHand](#pickuphand) hand, float duration, float amplitude, float frequency)                                                                      | 在指定手柄上播放触觉反馈                                                |
|     | [VRCPickup](#vrcpickup)                                                | GetPickupInHand([PickupHand](#pickuphand) hand)                                                                                                                              | 获取指定手的拾取对象                                                  |



### InputManager
`static class VRC.SDKBase.InputManager`

方法
| 静态 | 返回值                           | 名称                                                                                                           | 摘要                                                                                                        |
| :--: | -------------------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
|  ✔️   | bool                              | IsUsingHandController()                                                                                        | 返回用户是否正在使用手部控制器                                                                               |
|  ✔️   | [VRCInputMethod](#vrcinputmethod) | GetLastUsedInputMethod()                                                                                       | 返回最后使用的输入方式，如果未找到返回 [`VRCInputMethod.Count`](#vrcinputmethod)                             |
|  ✔️   | void                              | EnableObjectHighlight([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj, bool enable) | 为指定对象启用或禁用高亮                                                                                   |
|  ✔️   | void                              | EnableObjectHighlight([Renderer](https://docs.unity3d.com/ScriptReference/Renderer.html) r, bool enable)       | 为指定渲染器启用或禁用高亮                                                                                 |

### SerializationResult
`struct VRC.Udon.Common`

OnPostSerialization 事件返回的结果。

构造函数
| 名称                                             | 摘要                                                         |
| ------------------------------------------------ | ----------------------------------------------------------- |
| SerializationResult(bool success, int byteCount) | 构造函数。注意该构造函数仅可在编辑器中调用。                |

属性
| 类型 | 名称      | 摘要                                           |
| ---- | --------- | --------------------------------------------- |
| bool | success   | 序列化是否成功                                |
| int  | byteCount | 序列化的字节数                                |

### UdonInputEventArgs
`struct VRC.Udon.Common.UdonInputEventArgs`

输入事件的上下文数据。

属性
| 类型                                      | 名称       | 摘要                                                                                   |
| ----------------------------------------- | ---------- | ------------------------------------------------------------------------------------- |
| [UdonInputEventType](#udoninputeventtype) | eventType  | 触发的输入事件类型                                                                    |
| bool                                      | boolValue  | 当触发 `InputJump`、`InputUse`、`InputGrab` 或 `InputDrop` 时的输入值                 |
| float                                     | floatValue | 当触发 `InputMoveHorizontal`、`InputMoveVertical`、`InputLookHorizontal` 或 `InputLookVertical` 时的输入值 |
| [HandType](#handtype)                     | handType   | 输入事件发生的手。桌面用户中，键盘为左手，鼠标为右手                                   |

### VRCUrl
`class VRC.SDKBase.VRCUrl`

VRCUrl 对象通常无法在运行时通过 Udon 构造，通常通过编辑器脚本或 [VRCUrlInputField](#vrcurlinputfield) 获取。

构造函数
| 名称               | 摘要                                                                                   |
| ------------------ | ------------------------------------------------------------------------------------- |
| VRCUrl(string url) | 构造函数，输入 URL。仅可在编辑器中调用。                                              |

属性
| 静态 | 类型              | 名称  | 摘要       |
| :--: | ----------------- | ----- | --------- |
|  ✔️   | [VRCUrl](#vrcurl) | Empty | 空 URL 对象 |

方法
| 返回值 | 名称 | 摘要                    |
| ------- | ---- | ---------------------- |
| string  | Get() | 获取 URL 当前值         |

### VRCUrlInputField
`class VRC.SDK3.Components.VRCUrlInputField`

UI 组件，供用户输入自定义 URL，并输出给 Udon 程序作为 [VRCUrl](#vrcurl)。

方法
| 返回值           | 名称                          | 摘要                                         |
| ----------------- | ----------------------------- | ------------------------------------------- |
| [VRCUrl](#vrcurl) | GetUrl()                      | 获取输入框当前 URL 值                         |
| void              | SetUrl([VRCUrl](#vrcurl) url) | 设置输入框显示的 URL                          |

### VRCMirrorReflection
`class VRC.SDK3.Components.VRCMirrorReflection` / `class VRC.SDKBase.VRC_MirrorReflection`

管理对象镜面表面的组件。

属性
| 类型                                                                 | 名称                   | 摘要                                                                                                                              |
| -------------------------------------------------------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| bool                                                                 | m_DisablePixelLights   | 禁用实时像素着色点光源和聚光灯，启用后将退回使用顶点光照                                                                      |
| bool                                                                 | TurnOffMirrorOcclusion | 禁用镜面遮挡剔除，如镜中物体闪烁可启用                                                                                           |
| [LayerMask](https://docs.unity3d.com/ScriptReference/LayerMask.html) | m_ReflectLayers        | 仅渲染选中层的对象，水层对象永远不渲染                                                                                           |

### VRCObjectPool
`class VRC.SDK3.Components.VRCObjectPool`

轻量级对象池，管理一组 GameObject 并同步它们的激活状态。  

- `TryToSpawn` 激活对象并返回，若无可用对象返回 null  
- `Return` 由对象池所有者调用，将对象返回池中并禁用  
- 对象激活时触发 `OnSpawn` 事件，UdonBehaviour 可监听  
- 后加入的玩家会自动同步对象状态

属性
| 类型                                                                     | 名称 | 摘要                       |
| ------------------------------------------------------------------------ | ---- | ------------------------- |
| [GameObject[]](https://docs.unity3d.com/ScriptReference/GameObject.html) | Pool | 对象池管理的对象数组        |

方法
| 返回值                                                                | 名称                                                                               | 摘要                                                        |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) | TryToSpawn()                                                                       | 返回池中未使用的对象，如无返回 null                           |
| void                                                                   | Return([GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html) obj) | 将指定对象放回池中，可供后续使用                              |

### VRCObjectSync
`class VRC.SDK3.Components.VRCObjectSync`

该组件会自动同步对象的 Transform（位置、旋转、缩放）以及 Rigidbody（物理）。

属性
| 类型 | 名称                            | 摘要                                                                                       |
| ---- | ------------------------------- | ----------------------------------------------------------------------------------------- |
| bool | AllowCollisionOwnershipTransfer | 当对象与另一玩家拥有的对象发生碰撞时，是否允许所有权转移                                   |

方法
| 返回值 | 名称                                                                                            | 摘要                                                                                                                                     |
| ------- | ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| void    | SetKinematic(bool value)                                                                        | 设置 Rigidbody 是否为 Kinematic。Kinematic 状态下会忽略力、碰撞和关节，通常用于同步控制。                                              |
| void    | SetGravity(bool value)                                                                          | 设置 Rigidbody 是否受重力影响，通常用于同步控制。                                                                                       |
| void    | FlagDiscontinuity()                                                                             | 当你希望瞬移对象时调用。本帧的变动会直接应用而不平滑过渡。                                                                               |
| void    | TeleportTo([Transform](https://docs.unity3d.com/ScriptReference/Transform.html) targetLocation) | 将对象移动到指定 Transform 位置。                                                                                                       |
| void    | Respawn()                                                                                       | 将对象移动回初始生成位置。                                                                                                               |

---

### VRCAvatarPedestal
`class VRC.SDK3.Components.VRCAvatarPedestal` / `class VRC.SDKBase.VRC_AvatarPedestal`

用于在世界中展示虚拟形象，并允许玩家切换至该虚拟形象。

属性
| 类型                                                                 | 名称               | 摘要                                                                 |
| -------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------- |
| string                                                               | blueprintId        | 展示虚拟形象的 Blueprint Id                                             |
| [Transform](https://docs.unity3d.com/ScriptReference/Transform.html) | Placement          | 虚拟形象显示位置的 Transform                                             |
| bool                                                                 | ChangeAvatarsOnUse | 若为 true，玩家使用台座时切换至此虚拟形象                                  |
| float                                                                | scale              | 虚拟形象大小，仅影响台座展示                                               |

方法
| 返回值 | 名称                                                   | 摘要                                                                                     |
| ------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| void    | SwitchAvatar(string id)                                | 更换台座虚拟形象 Blueprint Id，并更新所有玩家的视图                                         |
| void    | SetAvatarUse([VRCPlayerApi](#vrcplayerapi) instigator) | 让玩家切换至台座关联虚拟形象。`instigator` 必须是本地玩家（Networking.LocalPlayer）      |

---

### VRCPickup
`class VRC.SDK3.Components.VRCPickup` / `class VRC.SDKBase.VRC_Pickup`

允许对象被玩家拾取和持有。

属性
| 类型                                                                 | 名称                          | 摘要                                                                                                                   |
| -------------------------------------------------------------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [ForceMode](https://docs.unity3d.com/ScriptReference/ForceMode.html) | MomentumTransferMethod        | 定义碰撞力如何作用于被击中的 Rigidbody 对象，仅当 AllowCollisionTransfer 为 true 时生效                               |
| bool                                                                 | DisallowTheft                 | 是否允许其他玩家从他人手中夺取拾取物                                                                                 |
| [Transform](https://docs.unity3d.com/ScriptReference/Transform.html) | ExactGun                      | 若设置，持有位置使用 Exact Gun                                   |
| [Transform](https://docs.unity3d.com/ScriptReference/Transform.html) | ExactGrip                     | 若设置，持有位置使用 Exact Grip                                  |
| bool                                                                 | allowManipulationWhenEquipped | 当拾取物被持有时，玩家是否可以操作物体                                         |
| [PickupOrientation](#pickuporientation)                              | orientation                   | 持有姿态（Any / Grip / Gun）                                           |
| [AutoHoldMode](#autoholdmode)                                        | AutoHold                      | 拾取物松开抓取按钮后是否仍留在玩家手中                                  |
| string                                                               | InteractionText               | 持有拾取物时的提示文字                                                   |
| string                                                               | UseText                       | 鼠标悬停拾取物时的提示文字                                               |
| float                                                                | ThrowVelocityBoostMinSpeed    | 投掷时最小速度阈值                                                      |
| float                                                                | ThrowVelocityBoostScale       | 投掷速度倍率                                                            |
| bool                                                                 | pickupable                    | 是否可拾取                                                              |
| float                                                                | proximity                     | 玩家与拾取物最大交互距离                                                 |
| [VRCPlayerApi](#vrcplayerapi)                                        | currentPlayer                 | 当前持有拾取物的玩家                                                      |
| bool                                                                 | IsHeld                        | 拾取物是否被玩家持有                                                      |
| [PickupHand](#pickuphand)                                            | currentHand                   | 玩家持有拾取物的手                                                       |

方法
| 返回值 | 名称                                                                  | 摘要                                                                                  |
| ------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| void    | Drop()                                                                | 玩家丢弃拾取物                                                                       |
| void    | Drop([VRCPlayerApi](#vrcplayerapi) instigator)                        | 玩家丢弃拾取物，仅当 instigator 是当前持有玩家时生效                                  |
| void    | GenerateHapticEvent(float duration, float amplitude, float frequency) | 在玩家手柄上产生触觉反馈，默认 duration=0.25，amplitude=0.5，frequency=0.5          |
| void    | PlayHaptics()                                                         | 在玩家手柄上播放触觉反馈                                                              |

---

### VRCPortalMarker
`class VRC.SDK3.Components.VRCPortalMarker` / `class VRC.SDKBase.VRC_PortalMarker`

创建通往其他房间的传送门。

属性
| 类型   | 名称   | 摘要                      |
| ------ | ------ | ------------------------ |
| string | roomId | 目标房间的 Id             |

方法
| 返回值 | 名称            | 摘要                                  |
| ------- | --------------- | ------------------------------------ |
| void    | RefreshPortal() | 刷新玩家看到的传送门                  |

---

## Enums

### EventTiming
`enum VRC.Udon.Common.Enums.EventTiming`

| 名称        | 摘要                              |
| ----------- | -------------------------------- |
| Update      | 在 Update() 时触发事件             |
| LateUpdate  | 在 LateUpdate() 时触发事件         |
| FixedUpdate | 在 FixedUpdate() 时触发事件        |

### Mobility
`enum VRC.SDKBase.VRCStation.Mobility`

| 名称                 | 摘要                                  |
| -------------------- | ------------------------------------ |
| Mobile               | 允许玩家在座位上移动                  |
| Immobilize           | 禁止玩家移动                          |
| ImmobilizeForVehicle | 优化的 Immobilize，用于可移动座位       |

### NetworkEventTarget
`enum VRC.Udon.Common.Interfaces.NetworkEventTarget`

| 名称  | 摘要                     |
| ----- | ----------------------- |
| All   | 所有玩家                  |
| Owner | 对象所有者                |

### SpawnOrientation
`enum VRC.SDKBase.VRC_SceneDescriptor.SpawnOrientation`

| 名称                      | 摘要                                                |
| ------------------------- | -------------------------------------------------- |
| Default                   | 使用 VRChat 默认生成行为                               |
| AlignPlayerWithSpawnPoint | 玩家旋转与 Spawn Transform 对齐                       |
| AlignRoomWithSpawnPoint   | 玩家房间中心与 Spawn Transform 对齐                   |

### TrackingDataType
`enum VRC.SDKBase.VRCPlayerApi.TrackingDataType`

| 名称      | 摘要                       |
| --------- | ------------------------- |
| Head      | 玩家头部跟踪数据           |
| LeftHand  | 玩家左手跟踪数据           |
| RightHand | 玩家右手跟踪数据           |
| Origin    | 玩家空间原点数据           |

### VRCInputMethod
`enum VRC.SDKBase.VRCInputMethod`

| 名称       | 值 | 摘要                  |
| ---------- | --- | -------------------- |
| Keyboard   | 0   | 键盘                  |
| Mouse      | 1   | 鼠标                  |
| Controller | 2   | 控制器                |
| Gaze       | 3   | 注视                  |
| Vive       | 5   | Vive 控制器           |
| Oculus     | 6   | Oculus 控制器         |
| Count      | 7   | 最大输入方式数量       |

### HandType
`enum VRC.Udon.Common.HandType`

| 名称  | 摘要        |
| ----- | ---------- |
| RIGHT | 右手       |
| LEFT  | 左手       |

### UdonInputEventType
`enum VRC.Udon.Common.UdonInputEventType`

| 名称   | 摘要          |
| ------ | ------------- |
| BUTTON | 按键事件       |
| AXIS   | 轴事件         |

### VideoError
`enum VRC.SDK3.Components.Video.VideoError`

| 名称         | 摘要          |
| ------------ | ------------- |
| Unknown      | 未知错误       |
| InvalidURL   | URL 无效       |
| AccessDenied | 拒绝访问       |
| PlayerError  | 播放器错误     |
| RateLimited  | 请求过多       |

### AutoHoldMode
`enum VRC.SDK3.Components.VRCPickup.AutoHoldMode` / `enum VRC.SDKBase.VRC_Pickup.AutoHoldMode`

| 名称       | 摘要                                                                  |
| ---------- | -------------------------------------------------------------------- |
| AutoDetect | 自动检测适用行为                                                       |
| Yes        | 松开抓取按钮后，拾取物仍留在手中，直到按下并松开放下按钮               |
| No         | 松开抓取按钮后，拾取物立即释放                                       |

### PickupOrientation
`enum VRC.SDK3.Components.VRCPickup.PickupOrientation` / `enum VRC.SDKBase.VRC_Pickup.PickupOrientation`

| 名称 | 摘要             |
| ---- | ---------------- |
| Any  | 任意方向         |
| Grip | Grip 持握方向    |
| Gun  | 枪械持握方向     |

### PickupHand
`enum VRC.SDK3.Components.VRCPickup.PickupHand` / `enum VRC.SDKBase.VRC_Pickup.PickupHand`

| 名称  | 摘要      |
| ----- | -------- |
| None  | 无手     |
| Left  | 左手     |
| Right | 右手     |



# 支持的功能

## 同步变量 (Synced Variables)
这些变量可通过 `[UdonSynced](https://udonsharp.docs.vrchat.com/udonsharp/#udonsynced)` 属性在网络上同步。
::: info
下表中的 `size` 指**大致内存大小**。在网络传输中，这些数据会被序列化，可能会产生额外的数据开销。例如，`bool` 类型在同步时至少发送 1 字节（而不是 1 位），还会加上网络开销。  
要查看实际序列化的数据字节数，可以使用 [`OnPostSerialization`](https://creators.vrchat.com/worlds/udon/networking/network-components#onpostserialization) 事件中的 `byteCount` 属性。更多同步信息，请参考 [Udon 网络规格](https://creators.vrchat.com/worlds/udon/networking/network-details#data-and-specs)。
:::

**布尔类型 (Boolean types)**
| 类型 | 大小   |
| ---- | ------ |
| bool | 1 byte |

**整数类型 (Integral numeric types)**
| 类型   | 范围                                                   | 大小    |
| ------ | ----------------------------------------------------- | ------- |
| sbyte  | -128 to 127                                           | 1 byte  |
| byte   | 0 to 255                                              | 1 byte  |
| short  | -32,768 to 32,767                                     | 2 bytes |
| ushort | 0 to 65,535                                           | 2 bytes |
| int    | -2,147,483,648 to 2,147,483,647                       | 4 bytes |
| uint   | 0 to 4,294,967,295                                    | 4 bytes |
| long   | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 8 bytes |
| ulong  | 0 to 18,446,744,073,709,551,615                       | 8 bytes |

**浮点类型 (Floating-point numeric types)**
| 类型   | 大致范围                       | 精度         | 大小    |
| ------ | ------------------------------- | ------------ | ------- |
| float  | ±1.5 × 10^(−45) 到 ±3.4 × 10^(38) | ~6-9 位数字  | 4 bytes |
| double | ±5.0 × 10^(−324) 到 ±1.7 × 10^(308) | ~15-17 位数字 | 8 bytes |

**向量类型和结构 (Vector mathematics types, Unity)**
| 类型 | 范围       | 大小   |
| ---- | --------- | ------ |
| [Vector2](https://docs.unity3d.com/ScriptReference/Vector2.html)       | 同 float | 8 bytes  |
| [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html)       | 同 float | 12 bytes |
| [Vector4](https://docs.unity3d.com/ScriptReference/Vector4.html)       | 同 float | 16 bytes |
| [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) | 同 float | 16 bytes |

**颜色结构 (Color structures)**
| 类型 | 范围 / 精度 | 大小 |
| ---- | ----------- | ---- |
| [Color](https://docs.unity3d.com/ScriptReference/Color.html)     | 同 float | 16 bytes |
| [Color32](https://docs.unity3d.com/ScriptReference/Color32.html) | 同 byte  | 4 bytes  |

**文本类型和结构 (Text types and structures)**
| 类型   | 范围          | 大小           |
| ------ | ------------- | -------------- |
| char   | U+0000 到 U+FFFF | 2 bytes        |
| string | 同 char       | 2 bytes / 字符 |

**其他结构 (Other structures)**
| 类型              | 范围         | 大小           |
| ----------------- | ------------ | -------------- |
| [VRCUrl](#vrcurl) | U+0000 到 U+FFFF | 2 bytes / 字符 |
