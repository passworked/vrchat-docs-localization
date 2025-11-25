---
upstreamCommit: f1bf1da95129772851a2ddf4840a99de14271ff8
---

# Examples

* [旋转立方体](#旋转立方体)
* [玩家设定](#玩家设定)
* [开关](#开关)
* [传送玩家](#传送玩家)
* [获取玩家列表](#获取玩家列表)
* [UdonSharp类示例](#udonsharp类示例)


---

### 旋转立方体
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

### 玩家设定
```cs
using UnityEngine;
using UdonSharp;
using VRC.SDKBase;

public class PlayerModSettings : UdonSharpBehaviour
{
    VRCPlayerApi playerApi;

    [Header("Player Settings")]
    [SerializeField] float jumpImpulse = 3;
    [SerializeField] float walkSpeed = 2;
    [SerializeField] float runSpeed = 4;
    [SerializeField] float gravityStrengh = 1;

    void Start()
    {
        playerApi = Networking.LocalPlayer;
        playerApi.SetJumpImpulse(jumpImpulse);
        playerApi.SetWalkSpeed(walkSpeed);
        playerApi.SetRunSpeed(runSpeed);
        playerApi.SetGravityStrength(gravityStrengh);
    }
}
```
更高级的示例位于[UdonSharp 示例文件夹](https://github.com/Merlin-san/UdonSharp/blob/master/Assets/UdonSharp/Examples/Utilities/PlayerModSetter.cs).

### 开关
```cs
using UnityEngine;
using UdonSharp;

public class ClickMe: UdonSharpBehaviour
{
    public override void Interact()
    {
        gameObject.SetActive(false);
    }
}
```

### 传送玩家
```cs
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;

public class TeleportPlayer : UdonSharpBehaviour
{
    [SerializeField] Transform targetPosition;

    public override void Interact()
    {
        Networking.LocalPlayer.TeleportTo(targetPosition.position, 
                                          targetPosition.rotation, 
                                          VRC_SceneDescriptor.SpawnOrientation.Default, 
                                          false);
    }
}
```

### 获取玩家列表
示例：如何获取当前房间中的所有玩家。
```cs
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;

public class GetPlayersExample : UdonSharpBehaviour
{
    // 世界最大人数为 10，所以我们创建一个长度为 20（硬上限）的数组
    VRCPlayerApi[] players = new VRCPlayerApi[20];

    void Start()
    {
        VRCPlayerApi.GetPlayers(players);

        foreach(VRCPlayerApi player in players) {
            if(player == null) continue;
            Debug.Log(player.displayName);
        }
    }
}
```

### UdonSharp类示例
这是一个UdonSharp类示例，用来展示它如何与其他 UdonSharp 行为通讯。
```cs
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon.Common.Interfaces;

namespace UdonSharpExample
{
    public class Example : UdonSharpBehaviour
    {
         // UdonSharpBehaviour 类（影响 Inspector）
        [SerializeField] AnotherExample anotherExample;

        void Start()
        {
            // 相当于：anotherExample.GetProgramVariable("publicBoolean");
            if(anotherExample.publicBoolean)
            {
                // 相当于：anotherExample.SendCustomEvent("RunMethod");
                anotherExample.RunMethod();
            }
        }

        // VRChat 事件
        public override void Interact()
        {
            // 相当于：SendCustomEvent("DoStuff");
            DoStuff();
        }

        public void DoStuff()
        {
            // 这个事件会被发送到所有客户端，并在它们本地运行（包括发送者）
            SendCustomNetworkEvent(NetworkEventTarget.All, "NetworkEventStuff");
        }

        public void NetworkEventStuff()
        {
            // 相当于：anotherExample.SetProgramVariable("publicBoolean", false);
            anotherExample.publicBoolean = false;

             // 相当于：anotherExample.SendCustomEvent("RunMethod");
            anotherExample.RunMethod();

            anotherExample.SendCustomNetworkEvent(NetworkEventTarget.Owner, "DoOwnerStuff");
        }
    }
}
```