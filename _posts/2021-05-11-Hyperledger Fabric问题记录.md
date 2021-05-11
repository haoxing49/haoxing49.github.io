---
layout:     post
title:      Hyperledger Fabric问题记录
subtitle:   Hyperledger Fabric问题记录
date:       2021-05-11
author:     haoxing49
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Hyperledger Fabric
---

```
Error: chaincode install failed with status: 500 - Failed to authorize invocation due to failed ACL check: Failed verifying that proposal's creator satisfies local MSP principal during channelless check policy with policy [Admins]: [This identity is not an admin]
```
- 🔭&nbsp;&nbsp;原因:<br/>
没有链码安装权限，`CORE_PEER_MSPCONFIGPATH`环境变量设置错误
- 💡&nbsp;&nbsp;解决:<br/>
设置`CORE_PEER_MSPCONFIGPATH`为管理员，例如:<br/>`export CORE_PEER_MSPCONFIGPATH=/tmp/hyperledger/org1/admin/msp`
------

```
Error: endorsement failure during invoke. response: status:500 message:"error in simulation: failed to execute transaction e9acf419acbf9d966d5cc70ff5e42d72574e154f87552f78e7d03830bec51dd0: could not launch chaincode fileinfo:8b0eb63f2142a26d172096c5d1ef0c44ab4b483d7a60bfed41cd5832d62293da: chaincode registration failed: container exited with 137" 
```
- 🔭&nbsp;&nbsp;原因:<br/>
安装链码后链码没有启动
- 💡&nbsp;&nbsp;解决:<br/>
在docker中启动链码
------
```
failed constructing descriptor for chaincodes
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
在应用中调用链码是出现错误
- 🔭&nbsp;&nbsp;可能原因:<br/>
链码初始化后数据不同步
- 💡&nbsp;&nbsp;解决:<br/>
在docker重新启动节点
---