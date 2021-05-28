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

❌&nbsp;&nbsp;错误提示:<br/>
```
Error: chaincode install failed with status: 500 - Failed to authorize invocation due to failed ACL check: Failed verifying that proposal's creator satisfies local MSP principal during channelless check policy with policy [Admins]: [This identity is not an admin]
```
- 🔍&nbsp;&nbsp;原因:<br/>
没有链码安装权限，`CORE_PEER_MSPCONFIGPATH`环境变量设置错误
- 💡&nbsp;&nbsp;解决:<br/>
设置`CORE_PEER_MSPCONFIGPATH`为管理员，例如:<br/>`export CORE_PEER_MSPCONFIGPATH=/tmp/hyperledger/org1/admin/msp`

---

❌&nbsp;&nbsp;错误提示:<br/>
```
Error: endorsement failure during invoke. response: status:500 message:"error in simulation: failed to execute transaction e9acf419acbf9d966d5cc70ff5e42d72574e154f87552f78e7d03830bec51dd0: could not launch chaincode fileinfo:8b0eb63f2142a26d172096c5d1ef0c44ab4b483d7a60bfed41cd5832d62293da: chaincode registration failed: container exited with 137" 
```
- 🔍&nbsp;&nbsp;原因:<br/>
安装链码后链码没有启动
- 💡&nbsp;&nbsp;解决:<br/>
在docker中启动链码

---

❌&nbsp;&nbsp;错误提示:<br/>
```
ERROR org.hyperledger.fabric.sdk.ServiceDiscovery - Error failed constructing descriptor for chaincodes:<name:"fileinfo" >
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
在应用中调用链码是出现错误
- 🔍&nbsp;&nbsp;可能原因:<br/>
链码初始化后数据不同步
- 💡&nbsp;&nbsp;解决:<br/>
在docker重新启动节点

---
❌&nbsp;&nbsp;错误提示:<br/>
```
ESCC invoke result: response:<status:500 message:"error in simulation: failed to execute transaction dc84996405944109ed3b82676ab5cbb7bb3af6188fbb0f7d2716c68e5e582275: could not launch chaincode fileinfo:06a966b7f3f1f747003f0987c3f071536bf7c9426977223f801b8ee3a46a0a36: error starting container: error starting container: API error (404): network fileinfo_fabric-ca not found" > 
Error: endorsement failure during invoke. response: status:500 message:"error in simulation: failed to execute transaction dc84996405944109ed3b82676ab5cbb7bb3af6188fbb0f7d2716c68e5e582275: could not launch chaincode fileinfo:06a966b7f3f1f747003f0987c3f071536bf7c9426977223f801b8ee3a46a0a36: error starting container: error starting container: API error (404): network fileinfo_fabric-ca not found"
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
无法提交链码
- 🔍&nbsp;&nbsp;原因:<br/>
`docker-compose`文件`CORE_VM_DOCKER_HOSTCONFIG_NETWORKMODE`参数配置错误
- 💡&nbsp;&nbsp;解决:<br/>
修改`CORE_VM_DOCKER_HOSTCONFIG_NETWORKMODE`与其他容器在同一个网络中

---

❌&nbsp;&nbsp;错误提示:<br/>
```
Failed to send transaction to the orderer
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
在应用中进行交易出现错误
- 🔍&nbsp;&nbsp;原因:<br/>
无法访问`order`节点
- 💡&nbsp;&nbsp;解决:<br/>
在`/etc/hosts`中添加域名映射

---

❌&nbsp;&nbsp;错误提示:<br/>
```
No valid proposal responses received. 2 peer error responses: error in simulation: transaction returned with failure: Error during contract method execution; error in simulation: transaction returned with failure: Error during contract method execution
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
在应用中进行交易时出现错误
- 🔍&nbsp;&nbsp;可能原因:<br/>
    - 交易传参错误
    - 网络问题
- 💡&nbsp;&nbsp;解决:<br/>
    - 检查参数
    - 重启节点

---

❌&nbsp;&nbsp;错误提示:<br/>
```
ESCC invoke result: response:<status:500 message:"error in simulation: failed to execute transaction 6f92ca3c706b35c361ab828a7a0c472dc910f7fadc53704e137ecf049bc5c956: error sending: chaincode stream terminated" > 
Error: endorsement failure during invoke. response: status:500 message:"error in simulation: failed to execute transaction 6f92ca3c706b35c361ab828a7a0c472dc910f7fadc53704e137ecf049bc5c956: error sending: chaincode stream terminated" 
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
    - 进行链码初始化时出现提示
    - 链码容器不断重启
- 🔍&nbsp;&nbsp;可能原因:<br/>
    - 链码容器自动关闭
- 💡&nbsp;&nbsp;解决:<br/>
    - 设置节点配置文件`core.yaml`中的`chaincode.keepalive:30`或者其他值

---

❌&nbsp;&nbsp;错误提示:<br/>
```
fabric The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server. 
```
- ✏️&nbsp;&nbsp;问题描述:<br/>
    - 进行链码初始化时提示
- 🔍&nbsp;&nbsp;原因:<br/>
    - 因为初始化链码时数据来源于mysql,连接数据库失败导致
- 💡&nbsp;&nbsp;解决:<br/>
    - 检查数据库连接地址、账号、密码
