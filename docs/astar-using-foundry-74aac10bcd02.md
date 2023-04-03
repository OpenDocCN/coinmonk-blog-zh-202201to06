# [Astar]使用铸造

> 原文：<https://medium.com/coinmonks/astar-using-foundry-74aac10bcd02?source=collection_archive---------9----------------------->

![](img/7cd653a26beb9fa753ddbbcb8174c96c.png)

# 为什么要代工？

我最近听说 solidity 开发人员有比 hardhat 更好的工具。它的名字叫铸造厂。听说有以下几个特点。

*   测试代码可以在 solidity 中实现，不用换头。
*   有一个强大的堆栈跟踪功能，所以你不必使用 console.log，这是在 hardhat 环境中经常使用的。
*   编译速度比 hardhat 快。等等。

我们试试用代工吧！

[](https://github.com/foundry-rs/foundry) [## foundry 是一个非常快速、便携和模块化的以太坊工具包…

### Foundry 是一个用 Rust 编写的以太坊应用程序开发的非常快速、可移植和模块化的工具包。铸造厂…

github.com](https://github.com/foundry-rs/foundry) 

# 安装

*   首先，不装锈，就得装锈。查看[官方网站](https://www.rust-lang.org/tools/install)。
*   网络安装代工。这是 [github](https://github.com/foundry-rs/foundry) 。

```
curl -L https://foundry.paradigm.xyz | bash
```

*   重启你的终端。

```
foundryup
```

# 创建项目

```
mkdir test_project
cd test_project
forge init
```

*   运行该命令应该会创建以下目录和文件。

```
% ls -la              
total 24
drwxr-xr-x  10 shin.takahashi  staff  320  4 22 20:26 .
drwxr-xr-x   3 shin.takahashi  staff   96  4 22 20:26 ..
drwxr-xr-x  13 shin.takahashi  staff  416  4 22 20:26 .git
drwxr-xr-x   3 shin.takahashi  staff   96  4 22 20:26 .github
-rw-r--r--   1 shin.takahashi  staff   12  4 22 20:26 .gitignore
-rw-r--r--   1 shin.takahashi  staff   88  4 22 20:26 .gitmodules
-rw-r--r--   1 shin.takahashi  staff  129  4 22 20:26 foundry.toml
drwxr-xr-x   3 shin.takahashi  staff   96  4 22 20:26 lib
drwxr-xr-x   3 shin.takahashi  staff   96  4 22 20:26 src
drwxr-xr-x   3 shin.takahashi  staff   96  4 22 20:26 test
```

# 执行合同

*   由于“src/Contract.sol”是一个空文件，所以让我们实现一个测试契约。这一次，我将使用混音附带的 storage.sol。

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;contract Contract {
    uint256 number; /**
     * [@dev](http://twitter.com/dev) Store value in variable
     * [@param](http://twitter.com/param) num value to store
     */
    function store(uint256 num) public {
        number = num;
    } /**
     * [@dev](http://twitter.com/dev) Return value 
     * [@return](http://twitter.com/return) value of 'number'
     */
    function retrieve() public view returns (uint256){
        return number;
    }}
```

# 编制

```
% forge build --contracts ./src/Contract.sol 
[⠊] Compiling...
[⠊] installing solc version "0.8.13"
[⠘] Successfully installed solc 0.8.13
[⠢] Compiling 3 files with 0.8.13
[⠆] Solc finished in 232.37ms
Compiler run successful
```

# 试验

*   Foundry 允许你在 solidity 中实现你的测试代码。
*   继承并实现“DSTest ”,它是创建项目时生成的测试类。
*   **似乎它不被认为是测试函数，除非在测试函数的开头加上“test”。请注意，我在不知情的情况下在这里度过了时光。例如:“testXXXX”。**

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;import "../src/Contract.sol";
import "../lib/ds-test/src/test.sol";contract ContractTest is DSTest {

    Contract test_contract;function setUp() public {
        test_contract = new Contract();
    }function testStoreOK() public {
        test_contract.store(1);
        assertEq(test_contract.retrieve(),1);
    }function testSotreNG() public {
        test_contract.store(2);
        assertTrue(test_contract.retrieve()!=3);
    }function testStoreFuzzing(uint256 x) public {
        test_contract.store(x);
        assertEq(test_contract.retrieve(), x);
    }
}
```

*   正常执行的测试如下。

```
forge test --contracts ./test/Contract.t.sol       
[⠢] Compiling...
[⠒] Compiling 3 files with 0.8.13
[⠑] Solc finished in 279.62ms
Compiler run successfulRunning 3 tests for test/Contract.t.sol:ContractTest
[PASS] testSotreNG() (gas: 28279)
[PASS] testStoreFuzzing(uint256) (runs: 256, μ: 27984, ~: 28451)
[PASS] testStoreOK() (gas: 28303)
Test result: ok. 3 passed; 0 failed; finished in 48.35ms
```

*   您可以输出堆栈跟踪。

```
forge test -vvvvv --contracts ./test/Contract.t.sol
[⠆] Compiling...
No files changed, compilation skippedRunning 3 tests for test/Contract.t.sol:ContractTest
[PASS] testSotreNG() (gas: 28279)
Traces:
  [71895] ContractTest::setUp() 
    ├─ [34487] → new Contract@0xce71065d4017f316ec606fe4422e11eb2c47c246
    │   └─ ← 172 bytes of code
    └─ ← ()[28279] ContractTest::testSotreNG() 
    ├─ [22312] Contract::store(2) 
    │   └─ ← ()
    ├─ [246] Contract::retrieve() [staticcall]
    │   └─ ← 2
    └─ ← ()[PASS] testStoreFuzzing(uint256) (runs: 256, μ: 27595, ~: 28451)
Traces:
  [71895] ContractTest::setUp() 
    ├─ [34487] → new Contract@0xce71065d4017f316ec606fe4422e11eb2c47c246
    │   └─ ← 172 bytes of code
    └─ ← ()[PASS] testStoreOK() (gas: 28303)
Traces:
  [71895] ContractTest::setUp() 
    ├─ [34487] → new Contract@0xce71065d4017f316ec606fe4422e11eb2c47c246
    │   └─ ← 172 bytes of code
    └─ ← ()[28303] ContractTest::testStoreOK() 
    ├─ [22312] Contract::store(1) 
    │   └─ ← ()
    ├─ [246] Contract::retrieve() [staticcall]
    │   └─ ← 1
    └─ ← ()Test result: ok. 3 passed; 0 failed; finished in 51.47ms
```

## 模糊测试

*   请注意 testStoreFuzzing 函数。
*   这个函数使用 uint256 中的 x 作为参数。
*   通过给参数一个随机值来运行测试是一个很好的特性。

```
[PASS] testStoreFuzzing(uint256) (runs: 256, μ: 27595, ~: 28451)
Traces:
  [71895] ContractTest::setUp() 
    ├─ [34487] → new Contract@0xce71065d4017f316ec606fe4422e11eb2c47c246
    │   └─ ← 172 bytes of code
    └─ ← ()[PASS] testStoreOK() (gas: 28303)
```

# 结论

老实说，我发现很难使用安全帽，因为它太棒了，我已经太习惯了。但是，我认为测试代码可以可靠地实现的点和执行随机测试的点是非常奇妙的功能。它似乎没有像 hardhat 那样的节点。也许我就是找不到。
非常期待未来的版本升级和功能增加。

# 关于 Astar

Astar Network(以前称为 Plasm)是 Polkadot 上的一个 dApp hub，支持以太坊、WebAssembly 和第 2 层解决方案，如 ZK 汇总。Astar 的目标是成为一个多链智能合约平台，支持多种区块链和虚拟机。Polkadot 中继链不支持智能合约。这就是为什么生态系统必须有一个副链，让所有想要在 Polkadot 生态系统中构建的开发者都能够做到这一点。Astar 致力于为所有开发商提供最佳解决方案，支持 EVM，打造一条 EVM 和 WASM 智能合同共存、互通的纽带。

# 跟着我们

[**网站**](https://astar.network/) **|** [**推特**](https://twitter.com/AstarNetwork) **|** [**不和**](https://discord.gg/Z3nC9U4) **|** [**电报**](https://t.me/PlasmOfficial)**|**[**Github**](https://github.com/AstarNetwork)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [10 本关于加密的最佳书籍](https://coincodecap.com/best-crypto-books) | [英国 5 个最佳加密机器人](https://coincodecap.com/uk-trading-bots)
*   [ko only 回顾](https://coincodecap.com/koinly-review) | [Binaryx 回顾](https://coincodecap.com/binaryx-review)|[Hodlnaut vs CakeDefi](https://coincodecap.com/hodlnaut-vs-cakedefi-vs-celsius)
*   [MoonXBT vs Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt) | [硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6)
*   [火币交易机器人](https://coincodecap.com/huobi-trading-bot) | [如何购买 ADA](https://coincodecap.com/buy-ada-cardano) | [Geco？一次回顾](https://coincodecap.com/geco-one-review)
*   [币安 vs 比特邮票](https://coincodecap.com/binance-vs-bitstamp) | [比特熊猫 vs 比特币基地 vs Coinsbit](https://coincodecap.com/bitpanda-coinbase-coinsbit)
*   [如何购买 Ripple (XRP)](https://coincodecap.com/buy-ripple-india) | [非洲最好的加密交易所](https://coincodecap.com/crypto-exchange-africa)