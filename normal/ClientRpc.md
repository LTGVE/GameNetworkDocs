# ClientRpc  ||  [RPC(RPCType.Client)]
<div style="background: #804444; border-left: 4px solid #ff0000; padding: 0.5em 1em; margin: 0.5em 0;">
  🔴 <strong>注意：</strong> 所有的RPC方法必须以Rpc为结尾,且方法传参不能包含不可序列化的参数!
</div>

被标记的方法将会在```任意客户端```上执行,包括```服务器,主机,客户端```,但触发只能在```服务器或主机```上执行   
注意!被标记的方法只有在NetBehaviour的派生类和被注册后才能触发!    
您不必手动添加发送RPC序列化的逻辑,ILProcess会自动处理.   
如下列所示:   
```Csharp
[ClientRpc]//[RPC(RPCType.Client)]
public void DoSomething(string msg){
    Debug.Log($"Server invoked ClientRpc method! Message {msg}");
}
```
经过处理后的伪源码:   
```Csharp
[ClientRpc]//[RPC(RPCType.Client)]
public void DoSomething(string msg){
    	NetworkMachine networkClient = base.NetworkClient;
		bool isHost = networkClient.IsHost;
		bool isClient = networkClient.IsClient;
		if (isHost && isClient)
		{
			ValueBufferWriter valueBufferWriter = new ValueBufferWriter();
			valueBufferWriter.Write<string>(msg);
			RPCManager.SendClientRPC(/*DoSomeThingMethod's hash*/, valueBufferWriter, this.NetworkInstanceID);
		}
        Debug.Log($"Server invoked ClientRpc method! Message {msg}");
}

```
