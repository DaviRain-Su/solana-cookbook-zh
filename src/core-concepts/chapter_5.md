# Transactions


客户可以通过向集群提交交易来调用[程序](./chapter_3.md)。一个交易可以包含多个指令，每个指令都针对自己的程序。当提交一个交易时，Solana[运行时](https://docs.solana.com/developing/programming-model/runtime)将按顺序和原子方式处理其指令。如果指令的任何部分失败，整个交易将失败。

## 事实

> 事实简报
>
> - 指令是Solana上最基本的操作单元
> - 每个指令包含：
>  - The `program_id` of the intended program
>  - 要读取或写入的所有 `accounts` 的数组
>  - An `instruction_data` byte array that is specific to the intended program
> - 多个指令可以捆绑成一个事务
> - 每个交易包含：
>   - 要读取或写入的所有 `accounts` 的数组
>   - 一个或多个 `instructions`
>   - 最近的一次 `blockhash`
>   - 一个或多个 `signatures`
> - 指令按顺序进行处理，并且是原子性的
> - 如果指令的任何部分失败，整个交易都会失败。
> - 交易限制为1232字节

## 深入挖掘

Solana Runtime需要指令和交易同时指定它们打算从中读取或写入的所有账户列表。通过事先要求这些账户，运行时能够在所有交易之间并行执行。

当一个交易被提交到集群时，运行时会按顺序和原子方式处理其指令。对于每个指令，接收程序将解释其数据数组并对指定的账户进行操作。程序要么成功返回，要么返回一个错误代码。如果返回错误，整个交易将立即失败。

任何旨在从账户中扣款或修改其数据的交易都需要账户持有人的签名。任何将被修改的账户都会被标记为 `writable` 。只要交易费支付者支付了必要的租金和交易费用，就可以在未经持有人许可的情况下向账户存入款项。

在提交之前，所有交易必须引用[最近的区块哈希](https://docs.solana.com/developing/programming-model/transactions#recent-blockhash)。区块哈希用于防止重复和清除过时的交易。交易的区块哈希的最大有效期为150个区块，或者大约1分19秒，截至本文撰写时。

## 费用

Solana网络收取两种类型的费用：

- 传播交易的[交易费用](https://docs.solana.com/transaction_fees)（也称为“燃气费”）
- 链上存储数据的[租金费用](./chapter_3.md)


在Solana中，交易费用是确定性的：没有费用市场的概念，用户无法支付更高的费用来增加被包含在下一个区块中的机会。在撰写本文时，交易费用仅由所需签名数量决定（即 lamports_per_signature ），而不是由使用的资源量决定。这是因为当前所有交易的字节上限为1232字节。

所有交易都需要至少一个账户来签署交易。一旦提交，被序列化为可写的签署者账户将成为支付手续费的账户。无论交易成功与否，该账户将支付交易的费用。如果支付手续费的账户余额不足以支付交易费用，交易将被取消。


在撰写本文时，所有交易费用的50%由生成区块的验证者收取，而剩下的50%将被销毁。这种结构的作用是激励验证者在领导者计划中的时间段内尽可能多地处理交易。

## 其他资源

- [Official Documentation](https://docs.solana.com/developing/programming-model/transactions)
- [Transaction Structure](https://solana.wiki/docs/solidity-guide/transactions/#solana-transaction-structure)
- [Transaction Fees by Justin Starry](https://jstarry.notion.site/Transaction-Fees-f09387e6a8d84287aa16a34ecb58e239)
- [An Introduction to Solana by Hana](https://2501babe.github.io/posts/solana101.html)
- [Transaction Processing by Jito Labs](https://www.jito.wtf/blog/solana-validator-101-transaction-processing/)
- [Solana Transaction in Depth by Alex Miller](https://medium.com/@asmiller1989/solana-transactions-in-depth-1f7f7fe06ac2)
