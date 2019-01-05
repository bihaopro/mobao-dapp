# 墨客DAPP接口

## 概述

欢迎使用[墨宝](https://mobao.online/)(英文：mobao)的DAPP接口，墨宝是专门为墨客提供的钱包服务，主要功能包括ERC20、ERC721的支持、墨客子链的支持，以及墨客DAPP的支持。本文档主要描述墨宝DAPP接口。墨宝DAPP的接口参照墨客[MOACmask](https://github.com/MOACChain/MOACMask)，以及[以太坊Metamask](https://metamask.io/)的实现，提供兼容的接口服务。

在参考本文档的使用中，需要进一步了解[Metamask](https://metamask.github.io/metamask-docs)或者墨客的[chain3](https://github.com/MOACChain/moac-core/wiki/Chain3)接口可以相应的点击本文中的链接进行参考。

说明：墨宝只提供基于***window.moac***对象的形式进行提供DAP接口，不提供基于provider的DAP接口使用，同时墨客提供默认的公开RPC服务，如果需要自定义用户自己的RPC服务，可以在墨宝的设置里面进行设置。

## 使用

使用墨宝DAPP接口的第一步是判断是否在浏览器里面已经提供了墨宝DAPP接口，可以通过如下方式进行检测
    
```js
if (typeof window.moac === 'undefined') {
    alert('Looks like you are not connect to Mobao dapp interfaces');
} else {
    // TODO do things you want
}
```

墨宝提供例子方便大家的测试，例子在本github的[example.md](#example.md)。


## 属性

墨宝在启动DAP片的使用提供了如下一些属性，可以供用户进行DAPP开发使用：

    1. networkVersion，当前墨客网络ID
    2. isMobao，是否是墨宝的DAP接口，返回true或false
    3. dappVersion，DAPP的接口版本
    4. selectedAddress，当前用户的钱包地址

## 接口

### moac.enable(callback)

返回用户在墨宝的墨客钱包地址列表，当前只返回用户的当前地址。

```js
moac.enable(function(accounts) {
    console.log(accounts[0]);
});
```

### moac.sendAsync(options, callback)

发送消息给墨宝，消息格式按[Moac Chain3 JSON-RPC](https://github.com/MOACChain/moac-core/wiki/JSON-RPC)。

```js
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
    params: params,
    from: accounts[0]
}, function(err, result) {
    // TODO
});
```

### moac.on(eventName, callback)

    TODO


## 签名功能

如果你需要通过签名等操作，可以使用墨宝提供的签名功能函数功能，调用方式也是通过`sendAsync`。墨宝提供的签名方法为`mc_sign`，实现的原理和[Metamask]()的[`personal_sign`](https://metamask.github.io/metamask-docs/API_Reference/Signing_Data/Personal_Sign)签名对应。

Metamask提供三类签名方法，第一类是[`eth_sign`](https://metamask.github.io/metamask-docs/API_Reference/Signing_Data/Eth_Sign)，这个方法可以签署任何数据具有不安全性，所以已经不推荐使用。第二类[`persoal_sign`](https://metamask.github.io/metamask-docs/API_Reference/Signing_Data/Personal_Sign)方法在签署数据前面加了前缀进行区别，借鉴了安全问题。同时，Metamask也提供了其他团队提供的签名方法，例如[signTypedData](https://metamask.github.io/metamask-docs/API_Reference/Signing_Data/Sign_Typed_Data_v1)，包括[0xProtocol](https://0xproject.com/)和[SpankChain](https://spankchain.com/)提供的。

墨宝为了方便用户使用，只提供`personal_sign`的签名方法，也避免歧义，后面有其他需要可以进行添加。


## RPC API

墨宝使用`sendAsync`封装墨客底层的RPC功能，并提供请求转发服务。其中会包括部分需要墨宝用户进行认可、确认等操作，便于用户知悉DAPP对用户账号的使用。

`sendAsync`使用JSON的数据格式进行交互，并以JSON的数据格式进行回调返回用户请求的信息。

`options`参数依据如下格式进行输入：
```js
{
    method: 'supported json rpc method',
    params: [json rpc params array],
    from: 'selected account address'
}
```

`callback`回调函数是标准的Javascript回调函数，包括`err`和`result`，其中`err`表示错误信息，`result`是回调结果，`result`结果会根据每个json rpc请求的接口不一样而不一样，请参考相应的RPC接口文档。

`err`表示的是在请求墨宝的过程中产生的错误，`result`里面包括在执行用户请求的方法时墨客RPC中出现的错误。


目前支持的JSONRPC API包括如下：

   1. [chain3_clientVersion](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#chain3_clientversion)
   2. [chain3_sha3](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#chain3_sha3)
   3. [net_listening](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_listening)
   4. [net_peerCount](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_peerCount)
   5. [net_version](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#net_version)
   6. [mc_getBalance](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBalance)
   7. [mc_accounts](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_accounts)
   8. [mc_blockNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_blockNumber)
   9. [mc_call](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_call)
   10. [mc_coinbase](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_coinbase)
   11. [mc_estimateGas](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_estimateGas)
   12. [mc_gasPrice](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_gasPrice)
   13. [mc_getBlockByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockByHash)
   14. [mc_getBlockByNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockByNumber)
   15. [mc_getBlockTransactionCountByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockTransactionCountByHash)
   16. [mc_getBlockTransactionCountByNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getBlockTransactionCountByNumber)
   17. [mc_getCode](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getCode)
   18. [mc_getStorageAt](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getStorageAt)
   19. [mc_getTransactionByBlockHashAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByBlockHashAndIndex)
   20. [mc_getTransactionByBlockNumberAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByBlockNumberAndIndex)
   21. [mc_getTransactionByHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionByHash)
   22. [mc_getTransactionCount](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionCount)
   23. [mc_getTransactionReceipt](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getTransactionReceipt)
   24. [mc_getUncleByBlockHashAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleByBlockHashAndIndex)
   25. [mc_getUncleByBlockNumberAndIndex](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleByBlockNumberAndIndex)
   26. [mc_getUncleCountByBlockHash](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleCountByBlockHash)
   27. [mc_getUncleCountByBlockNumber](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_getUncleCountByBlockNumber)
   28. [mc_hashrate](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_hashrate)
   29. [mc_mining](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_mining)
   30. [mc_protocolVersion](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_protocolVersion)
   31. [mc_sendRawTransaction](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_sendRawTransaction)
   32. [mc_sendTransaction](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_sendTransaction)
   33. [mc_syncing](https://github.com/MOACChain/moac-core/wiki/JSON-RPC#mc_syncing)

