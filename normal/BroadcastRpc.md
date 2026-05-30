# BroadcastRpc  ||  [RPC(RPCType.Broadcast)]
<div style="background: #fff0f0; border-left: 4px solid #ff0000; padding: 0.5em 1em; margin: 0.5em 0;">
  🔴 <strong>注意：</strong> 所有的RPC方法必须以Rpc为结尾,且方法传参不能包含不可序列化的参数!
</div>

被标记的方法将会在```任意客户端```上执行,包括```服务器,主机,客户端```,且能被任意方触发.
注意!被标记的方法只有在NetBehaviour的派生类和被注册后才能触发!    
您不必手动添加发送RPC序列化的逻辑,ILProcess会自动处理.   
如下列所示:   
```Csharp
[BroadcastRpc]//[RPC(RPCType.Broadcast)]
public void DoSomething(string msg){
    Debug.Log($"Client invoked BroadcatRpc method! Message {msg}");
}
```
经过处理后的伪源码:   
```Csharp
[BroadcastRpc]//[RPC(RPCType.Broadcast)]
public void DoSomething(string msg){
    	NetworkMachine networkClient = base.NetworkClient;
		bool isHost = networkClient.IsHost;
		bool isClient = networkClient.IsClient;
		ValueBufferWriter valueBufferWriter = new ValueBufferWriter();
		valueBufferWriter.Write<string>(msg);
        RPCManager.SendBoradcastRPC(/*DoSomeThingMethod's hash*/, valueBufferWriter, this.NetworkInstanceID);
        Debug.Log($"Client invoked BroadcatRpc method! Message {msg}");
}

```
