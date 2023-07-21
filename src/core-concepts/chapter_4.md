# Programs

任何开发者都可以编写和部署程序到Solana区块链。这些程序（在其他协议中被称为智能合约）是链上活动的基础，为DeFi和NFT等各种应用提供动力，包括社交媒体和游戏。

## 事实

> 情况说明书
> - 程序处理来自最终用户和其他程序的[指令](./chapter_5.md)
> - 所有程序都是无状态的：它们与之交互的任何数据都存储在通过指令传递的单独[账户](./chapter_3.md)中
> - 程序本身存储在标记为 `executable` 的帐户中
> - 所有程序均由 [BPF 加载器](https://docs.solana.com/developing/runtime-facilities/programs#bpf-loader)拥有并由 [Solana 运行时](https://docs.solana.com/developing/programming-model/runtime)执行
> - 开发人员最常使用 Rust 或 C++ 编写程序，但也可以选择任何针对 [LLVM](https://llvm.org/) 的 [BPF](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter) 后端的语言
> - 所有程序都有一个进行指令处理的入口点（即 `process_instruction` ）；参数始终包括：
>  - `program_id: pubkey`
>  - `accounts : array`
>  - `instruction_data: byte array`

## 深入挖掘

与大多数其他区块链不同，Solana完全将代码与数据分离。程序交互的所有数据都存储在单独的账户中，并通过指令以引用的方式传递。这种模型允许一个通用程序在不需要额外部署的情况下操作各种账户。这种模式在原生和SPL程序中都有常见的例子。


### 本地程序和Solana程序库（SPL）

Solana配备了一系列作为链上交互核心构建模块的程序。这些程序分为[原生程序](https://docs.solana.com/developing/runtime-facilities/programs#bpf-loader)和[Solana程序库（SPL）](https://spl.solana.com/)程序。

本地程序提供了操作验证器所需的基本功能。其中，最著名的是[系统程序](https://docs.solana.com/developing/runtime-facilities/programs#system-program)，负责管理新账户并在两个方之间转移SOL。

SPL程序支持一系列的链上活动，包括创建、交换和借贷代币，以及生成质押池和维护链上名称服务。[SPL代币程序](https://spl.solana.com/token)可以直接通过CLI调用，而其他程序（如[关联代币账户程序](https://spl.solana.com/associated-token-account)）通常与自定义程序一起使用。

### 编写程序

程序最常使用 Rust 或 C++ 开发，但也可以使用任何针对 LLVM 的 BPF 后端的语言进行开发。 [Neon Labs](https://neon-labs.org/) 和 [Solang](https://solang.readthedocs.io/en/latest/) 最近的举措实现了 [EVM](https://ethereum.org/en/developers/docs/evm/) 兼容性，并允许开发人员在 Solidity 中编写程序。

大多数基于 Rust 的程序都遵循以下架构：

| 文件 | 描述 |
| --- | --- |
| `src/lib.rs` | 注册模块 |
| `src/entrypoint.rs` | 程序的入口点 |
| `src/instruction.rs` | 程序 API，（反）序列化指令数据 |
| `src/processor.rs	` | 程序逻辑 |
| `src/state.rs` | 程序对象，（反）序列化状态 |
| `src/error.rs` | 特定于程序的错误 |

最近，[Anchor](https://github.com/coral-xyz/anchor) 已成为一种流行的程序开发框架。 Anchor 是一个固执己见的框架，类似于 Ruby on Rails，它可以减少样板文件并简化基于 Rust 的开发的（反）序列化过程。

程序通常在部署到测试网或主网之前针对本地主机和 Devnet 环境进行开发和测试。 Solana 支持以下环境：

| 环境 | Rpc connection Url  |
| --- | --- |
| 主网测试版 | https://api.mainnet-beta.solana.com |
| 测试网 | https://api.testnet.solana.com |
| 开发网 | https://api.devnet.solana.com |
| 本地主机 | Default port: 8899 (e.g. http://localhost:8899, http://192.168.1.88:8899) |

一旦部署到环境中，客户端就可以通过到相应集群的 [RPC 连接](https://docs.solana.com/api/http)与链上程序进行交互。

###  部署程序

开发人员可以通过 [CLI 部署](https://docs.solana.com/cli/deploy-a-program)他们的程序：

```bash
solana program deploy <PROGRAM_FILEPATH>
```

当程序部署时，它会被编译为[ELF共享对象](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)（包含BPF字节码）并上传到Solana集群。程序存在于帐户中（与 Solana 上的其他所有内容非常相似），只不过这些帐户被标记为 `executable` 并分配给 BPF 加载程序。该账户的地址称为 `program_id` ，用于在以后的所有交易中引用该程序。

Solana 支持多种 BPF 加载器，最新的是[可升级 BPF 加载器](https://explorer.solana.com/address/BPFLoaderUpgradeab1e11111111111111111111111)。 BPF 加载程序负责管理程序的帐户并通过 `program_id` 将其提供给客户端。所有程序都有一个进行指令处理的入口点（即 process_instruction ），并且参数始终包括：

- `program_id: pubkey`
- `accounts : array`
- `instruction_data: byte array`

一旦调用，程序将由 Solana 运行时执行。

## 其他资源

- [Solana 官方文档](https://docs.solana.com/developing/on-chain-programs/overview)
- [Spl docs](https://spl.solana.com/)
- [程序由 Justin Starry 部署](https://jstarry.notion.site/Program-deploys-29780c48794c47308d5f138074dd9838)
- [Iron Addicted Dog 的 Solana 入门套件](https://solmeet.gen3.network/notes/solana-starter-kit)
- [Paulx 在 Solana 上编程](https://paulx.dev/blog/2021/01/14/programming-on-solana-an-introduction/)
- [Hana 对 Solana 区块链的介绍](https://2501babe.github.io/posts/solana101.html)
- [Anchor](https://github.com/coral-xyz/anchor)
