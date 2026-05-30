# INetObjectReference

此接口被NetObject和NetBehaviour继承.

|变量|公开性|说明|
|:-------|:-------:|-------:|
|NetworkObjectID|Public|对象在主机上的ID|
|m_NetworkObjectID|Protected|用于存储对象在主机上的ID|

|方法|公开性|说明|
|:-------|:-------:|-------:|
|RegisterNetworkObject(uint value)|Public|注册网络ID,并返回自己|
|GetGameObject()|Public|获取本身所在的游戏对象|
