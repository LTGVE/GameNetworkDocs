# RPC
<div style="background: #fff0f0; border-left: 4px solid #ff0000; padding: 0.5em 1em; margin: 0.5em 0;">
  🔴 <strong>注意：</strong> 所有的RPC方法必须以Rpc为结尾,且方法传参不能包含不可序列化的参数!
</div>
用于标记RPC方法的特性.需要传入一个固定参数标明分发类型.   



|传参|类型|说明|
|:-------|:-------:|-------:|
|Type|[RPCType](/normal/RPCType.md)|用于传入来判断分发类型|