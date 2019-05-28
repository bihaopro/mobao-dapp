# 墨宝DAPP开发教程

## 墨宝介绍

墨宝钱包是首款支持通证、收藏品、子链以及DAPP的MOAC移动端钱包。

墨宝钱包目前开放了第三方DAPP接口，让开发者可以开发自己的DAPP，为用户提供更多的选择和功能。

## 墨宝接口介绍

接口对象
```js
window.moac
```
接口属性
```js
window.moac.networkVersion //当前墨客网络ID
window.moac.isMobao //是否是墨宝的DAPP接口，返回true或false
window.moac.version //DAPP的接口版本
window.moac.selectedAddress //当前用户的钱包地址
```
接口方法
```js
moac.enable(callback)
//返回用户在墨宝的墨客钱包地址列表，当前只返回用户的当前地址。

moac.enable(function(accounts) {
    console.log(accounts[0]);
});
moac.sendAsync(options, callback)
//发送消息给墨宝，消息格式按Moac Chain3 JSON-RPC。

var params: [{
    "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
    "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
    "gas": "0x76c0", // 30400
    "gasPrice": "0x9184e72a000", // 10000000000000
    "value": "0x9184e72a", // 2441406250
    "data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
}];
moac.sendAsync({
    method: 'mc_sendTransaction',
    params: params
}, function(err, result) {
    // TODO
});
```


**目前支持的JSONRPC API包括如下**

1. [chain3\_clientVersion](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#chain3_clientversion)
2. [chain3\_sha3](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#chain3_sha3)
3. [net\_listening](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_listening)
4. [net\_peerCount](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_peerCount)
5. [net\_version](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_version)
6. [mc\_getBalance](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBalance)
7. [mc\_accounts](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_accounts)
8. [mc\_blockNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_blockNumber)
9. [mc\_call](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_call)
10. [mc\_coinbase](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_coinbase)
11. [mc\_estimateGas](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_estimateGas)
12. [mc\_gasPrice](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_gasPrice)
13. [mc\_getBlockByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockByHash)
14. [mc\_getBlockByNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockByNumber)
15. [mc\_getBlockTransactionCountByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockTransactionCountByHash)
16. [mc\_getBlockTransactionCountByNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockTransactionCountByNumber)
17. [mc\_getCode](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getCode)
18. [mc\_getStorageAt](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getStorageAt)
19. [mc\_getTransactionByBlockHashAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByBlockHashAndIndex)
20. [mc\_getTransactionByBlockNumberAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByBlockNumberAndIndex)
21. [mc\_getTransactionByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByHash)
22. [mc\_getTransactionCount](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionCount)
23. [mc\_getTransactionReceipt](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionReceipt)
24. [mc\_getUncleByBlockHashAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleByBlockHashAndIndex)
25. [mc\_getUncleByBlockNumberAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleByBlockNumberAndIndex)
26. [mc\_getUncleCountByBlockHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleCountByBlockHash)
27. [mc\_getUncleCountByBlockNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleCountByBlockNumber)
28. [mc\_hashrate](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_hashrate)
29. [mc\_mining](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_mining)
30. [mc\_protocolVersion](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_protocolVersion)
31. [mc\_sendRawTransaction](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_sendRawTransaction)
32. [mc\_sendTransaction](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_sendTransaction)
33. [mc\_syncing](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_syncing)

## 墨宝开发测试版本dapp使用介绍

开发测试DAPP，请下载&quot;墨宝开发测试版&quot;（以下简称&quot;墨宝&quot;），下载地址：[https://fir.im/mobaotest](https://fir.im/mobaotest)

![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/1.jpg)
![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/2.jpg)

墨宝DAPP列表里已经提供官方版的DAPP示例可供参考
。

![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/3.jpg)
![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/4.jpg)

墨宝安装完成后，创建或恢复钱包至少一个地址，选择墨宝中的“发现”，点击“自定义添加DAPP”，输入名称、URL、ABI点击确定即可，DAPP列表中就会出现刚刚添加的DAPP。

页面在墨宝打开之后，墨宝钱包会注入moac对象，可以使用window.moac访问，据此判断DAPP是否是在墨宝中打开。

![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/5.jpg)
![image](https://github.com/bihaopro/mobao-dapp/blob/master/images/6.jpg)

```js
if (typeof window.moac === 'undefined') {
console.log(“你需要在墨宝app中访问”)            
} else {
// TODO
    moac.enable(function(accounts) {
    	console.log(accounts[0]);
});
moac.networkVersion，当前墨客网络ID
moac.isMobao，是否是墨宝的DAPP接口，返回true或false
moac.version，DAPP的接口版本
moac.selectedAddress，当前用户的钱包地址
moac.enable(callback)，返回用户在墨宝的墨客钱包地址列表
moac.sendAsync(options, callback)，发送消息给墨宝    
}
```
