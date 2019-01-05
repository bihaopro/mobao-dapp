# 墨客DAPP接口

## 概述

欢迎使用墨宝(英文：mobao)的DAPP接口，墨宝是专门为墨客提供的钱包服务，主要功能包括ERC20、ERC721的支持、墨客子链的支持，以及墨客DAPP的支持。本文档主要描述墨宝DAPP接口。墨宝DAPP的接口参照墨客[MOACmask](https://github.com/MOACChain/MOACMask)，以及[以太坊Metamask](https://metamask.io/)的实现，提供兼容的接口服务。

在参考本文档的使用中，需要进一步了解[Metamask](https://metamask.github.io/metamask-docs)或者墨客的[chain3](https://github.com/MOACChain/moac-core/wiki/Chain3)接口可以相应的点击本文中的链接进行参考。

说明：墨宝只提供基于***window.moac***对象的形式进行提供DAP接口，不提供基于provider的DAP接口使用，同时墨客提供默认的公开RPC服务，如果需要自定义用户自己的RPC服务，可以在墨宝的设置里面进行设置。

## 使用

使用墨宝DAPP接口的第一步是判断是否在浏览器里面已经注入了墨宝DAPP接口，可以通过如下方式进行检测
    
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

1. moac.enable(callback)

返回用户在墨宝的墨客钱包地址列表，当前只返回用户的当前地址。

```js
moac.enable(function(accounts) {
    console.log(accounts[0]);
});
```

2. moac.sendAsync(options, callback)

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

3. moac.on(eventName, callback)

TODO


## RPC API

目前支持的JSONRPC API包括如下：

### 接口
    
