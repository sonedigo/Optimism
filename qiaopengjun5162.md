---
timezone: Asia/Shanghai # 中国标准时间 (UTC+8)
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)

timezone: America/Anchorage # 阿拉斯加标准时间 (UTC-9)

timezone: America/Los_Angeles # 太平洋标准时间 (UTC-8)

timezone: America/Denver # 山地标准时间 (UTC-7)

timezone: America/Chicago # 中部标准时间 (UTC-6)

timezone: America/New_York # 东部标准时间 (UTC-5)

timezone: America/Halifax # 大西洋标准时间 (UTC-4)

timezone: America/St_Johns # 纽芬兰标准时间 (UTC-3:30)

timezone: America/Sao_Paulo # 巴西利亚时间 (UTC-3)

timezone: Atlantic/Azores # 亚速尔群岛时间 (UTC-1)

timezone: Europe/London # 格林威治标准时间 (UTC+0)

timezone: Europe/Berlin # 中欧标准时间 (UTC+1)

timezone: Europe/Helsinki # 东欧标准时间 (UTC+2)

timezone: Europe/Moscow # 莫斯科标准时间 (UTC+3)

timezone: Asia/Dubai # 海湾标准时间 (UTC+4)

timezone: Asia/Kolkata # 印度标准时间 (UTC+5:30)

timezone: Asia/Dhaka # 孟加拉国标准时间 (UTC+6)

timezone: Asia/Bangkok # 中南半岛时间 (UTC+7)

timezone: Asia/Shanghai # 中国标准时间 (UTC+8)

timezone: Asia/Tokyo # 日本标准时间 (UTC+9)

timezone: Australia/Sydney # 澳大利亚东部标准时间 (UTC+10)

timezone: Pacific/Auckland # 新西兰标准时间 (UTC+12)

---

# {你的名字}

1. 自我介绍
大家好，我是 Paxon Qiao，来自中国，是一名Web3开发工程师。我热爱编程，喜欢挑战自我，不断学习新技术。我期待在这次残酷学习中，能够与大家共同进步，互相学习，共同成长。

2. 你认为你会完成本次残酷学习吗？
我会，我相信我可以完成这次残酷学习。我对 Web3 生态感兴趣，对 blockchain 技术有所涉�及，并且有丰富的编程经验。我相信，只要我坚持不懈，努力学习，我一定能够完成这次残酷学习，并取得优异的成绩。

## Notes

<!-- Content_START -->

### 2025.01.06

Rollups 通过将大量交易打包到一个单一交易中，并将其提交到主链。这种方法可以分为两种类型：乐观 Rollups（Optimistic Rollups）和零知识 Rollups（zk-Rollups）。

- Op Rollups：假设交易是有效的，只有在有争议时才进行验证
- Zk Rollups：通过零知识证明技术，在提交交易数据的同时，保证其正确性。

### 2025.01.07

Optimistic Rollups 是一种基于承诺链（commit chain）和执行链（execution chain）的 Layer2 扩展方案。它将大量交易数据存储在链外的执行链上，并定期将执行结果提交到链上的承诺链中。通过链外计算和链上争议解决机制，Optimistic Rollups 实现了高性能的智能合约执行，同时保留了以太坊的去中心化特性。

### 2025.01.08

Op-stack 主要由 op-node, op-geth, op-batcher, op-proposer, CrossDomainMessenger, OptimismPortal, Bridge contracts 和 L2OutputOracle contract 等角色组成

### 2025.01.09

Op-stack 的 rollup 由两个服务来承担

op-batcher 服务：主要职责是负责将交易数据提交到 Layer1 的 EOA 地址
op-proposer 服务：主要职责是负责将交易状态提交到 Layer1 的 L2OutputOracle 合约

### 2025.01.10

信使合约的主要功能是跨链通信，核心方法位 sendMessage 与 relayMessage；
sendMessage: 将包裹的消息从源链发送到目标链上，维护自增的 msgNonce, 确报跨链消息的唯一性和安全性
relayMessage: 将源链发过来的消息在目标链上构建 MsgHash 对比，确保消息的一致性之后在目前链上调度执行该消息 在 op-stack 中在 L1 和 L2 层分别有
L1CrossDomainMessenger
L2CrossDomainMessenger 继承自 CrossDomainMessenger 合约，来承载跨链通信

### 2025.01.11

Optimism 是以太坊的第 2 层 （L2） 扩展解决方案，旨在以低廉的成本提供闪电般的交易速度。旨在推动以太坊的愿景，通过透明和可持续的区块链实现去中心化，为公众创造利益。

作为 L2，Optimism 建立在以太坊架构之上。因此，它相当于以太坊虚拟机，是以太坊主层的最小延伸。通过这种方式，开发者和加密货币用户能够以低费用享受快速交易，同时享受以太坊架构的安全性。

Optimism 现旨在通过一个名为 Superchain 的平台进一步增强其可扩展性，该平台由基于 OP Stack 构建的链网络组成，该网络将其 OP 主网与其他 L2 链合并。作为超级链，Optimism 旨在打造可互操作且可组合的生态系统，简化 L2s 的集成。

### 2025.01.12

用户调用 SDK 获取提现交易的状态，若状态为 READY_TO_PROVE, 说明交易可以进行证明； 用户可以调用 SDK 的 proveMessage 去进行交易的证明，或者直接 call OptimismPortal 合约 proveWithdrawalTransaction 方法进行交易的证明，当证明交易产生之后，等到交易过了挑战期，交易状态会变成 READY_FOR_RELAY；这个时候用户可以调用 SDK 的 finalizeMessage 方法进行资金的 Claim, 也可以直接调用 OptimismPortal 合约的 finalizeWithdrawalTransaction 方法进行资金的 Claim。

### 2025.01.13

充值交易会调用到 depositTransaction; depositTransaction 会抛出 TransactionDeposited 事件，事件里面携带信息如下 emit TransactionDeposited(from, _to, DEPOSIT_VERSION, opaqueData); op-node 监听到该合约事件之后，会在二层去执行充值交易

### 2025.01.14

Rollup :

1. 提交交易数据到DA
2. 提交交易状态到L1

### 2025.01.15

排序器（Sequencer）是以太坊扩容方案 Rollup 中的核心组件之一，负责对交易进行排序，并执行区块创建、交易接受、交易排序、交易执行以及交易数据提交等相关任务。
Sequencer：交易排序器
交易落块
第一笔交易是充值的交易
verifier：交易验证器

### 2025.01.16

verifier：交易验证器
根据交易生成证明，验证交易是否有效，如果无效则提交到以太坊上验证

### 2025.01.17

RPC: 转发用户发送的交易，提供对外的服务
ZK Prover：零知识证明器，生成证明 op-code 电路 链下交易证明生成器

### 2025.01.18

Sequencer：交易排序器 提交交易数据到DA, 提交交易状态到L1
verifier：交易验证器 链下交易证明生成器

### 2025.01.19

ZK Prover：零知识证明器，生成证明 op-code 电路 链下交易证明生成器
DA: 数据 availability layer
纠删码：纠删码是一种数据编码技术，用于对数据进行编码，以减少数据丢失的概率。
bls 签名：bls 签名是一种签名算法，它使用一对密钥对（公钥和私钥）来对数据进行签名。聚合签名是一种签名技术，它允许多个签名者对同一数据进行签名，并使用这些签名来验证数据的完整性和真实性。
共识：共识是一种协议，它定义了如何确定一个网络中的成员是否一致。
重新质押：重新质押是一种机制，它允许用户在网络中重新质押其质押的代币，以获得更多的奖励。
kzg 证明：kzg 证明是一种零知识证明技术，它允许用户对数据进行签名，而不需要公开数据。

### 2025.01.20

笔记内容

### 2025.01.21

笔记内容

### 2025.01.22

笔记内容

### 2025.01.23

笔记内容

### 2025.01.24

笔记内容

### 2025.01.25

笔记内容

### 2025.01.26

笔记内容

<!-- Content_END -->
