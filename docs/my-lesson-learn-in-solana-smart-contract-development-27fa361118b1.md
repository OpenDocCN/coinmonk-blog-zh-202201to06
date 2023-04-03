# 我在 Solana 智能合同开发中吸取教训

> 原文：<https://medium.com/coinmonks/my-lesson-learn-in-solana-smart-contract-development-27fa361118b1?source=collection_archive---------9----------------------->

[Solana](https://docs.solana.com/introduction) 是一个旨在提供高性能区块链的项目。其处理速度可高达每秒 20 万次交易(tps)，而与比特币和以太坊等其他热门区块链相比，它们的处理速度仅为 15 tps 左右。其极快的事务时间是由于使用了历史证明(PoH ),这为分布式系统带来了“同步时间”。“同步时间”实际上是由可验证延迟函数(VDF)产生的状态序列。有了这些时间信息，集群中的每个节点都可以在更短的时间内验证这些信息。

从应用的角度来看，智能合同的编程模型与其他区块链有很大不同。索拉纳智能合约是在索拉纳区块链执行的代码。与有状态的以太坊智能合约相反，Solana 智能合约是无状态的，这意味着它不会在合约中存储任何数据。所有数据都存储在验证器中的某种“帐户”(程序派生的帐户)中。这就像我们的计算机应用程序将数据存储在存储系统中的文件上一样。

在开始任何交易之前，前端应用程序将请求系统程序为智能合约创建程序派生帐户(`SystemProgram.createAccountWithSeed`)以存储交易状态。

```
const transaction = new Transaction().add(
      SystemProgram.createAccountWithSeed({        
                fromPubkey: payer.publicKey,        
                basePubkey: payer.publicKey,        
                seed: GREETING_SEED,        
                newAccountPubkey: greetedPubkey,        
                lamports,        
                space: GREETING_SIZE,        
                programId,      }),    );    
await sendAndConfirmTransaction(connection, transaction, [payer]);
```

然后，它会将程序派生的帐户地址(`greetedPubkey`)以及可选的付款人帐户地址和受益人帐户地址传递给智能合同处理器功能。

```
const instruction = new TransactionInstruction({    
                        keys: [{pubkey: greetedPubkey, 
                              isSigner: false, 
                              isWritable: true}],    
                        programId,    
                        data: Buffer.from(s, 'utf-8')  });  
await sendAndConfirmTransaction(    
          connection,    
          new Transaction().add(instruction),    
          [payer],  );
```

所有交易逻辑将在处理器功能内执行，如从付款人账户借记、向受益人账户贷记、更新程序衍生账户中的状态。额外的指令数据(`data: Buffer.from(s, ‘utf-8’)`)也可以从前端应用程序传递到函数参数`_instruction_data`中显示的处理器函数。

下面是 Rust 中的智能合同处理器函数定义

```
pub fn process_instruction(    
    program_id: &Pubkey, // Public key program loaded
    accounts: &[AccountInfo], // The account array storing the state
    _instruction_data: &[u8], // addition instruction data 
) -> ProgramResult {
```

智能合约可以用编程语言——Rust 开发，前端 app 可以用 Web3.0 API 用 typescript 开发。

在这里，我试图分享我在开发一个简单的智能合同方面的学习经验，但我发现它最终并不那么简单。

首先，我下载了 [hello-world 示例](https://github.com/solana-labs/example-helloworld/blob/master/README.md)，并按照自述文件上的说明进行操作。hello-world 的例子非常简单。每次调用智能协定时，它都会增加一个计数器。计数器存储在程序状态帐户的整数变量中。之后，前端应用程序可以读取递增后的计数器值。

接下来，基于 hello-world 示例，我在状态变量中使用“String”而不是 integer。然而，有一些挑战，我面对的只是一点点变化。

当 typescript 前端应用程序发送创建状态帐户的请求时，它需要指定大小。帐户一旦创建，就不能调整大小。状态变量中的所有数据将以二进制格式序列化并写入帐户。typescript 前端通过添加每个状态变量(即字符串类型变量)的内存大小来计算大小。然后智能合约函数将读取数据并反序列化到内存中。但是我发现 typescript 的字符串变量实现和 Rust 不一样。所以帐户的大小与 Rust 中的变量大小不匹配，这导致了反序列化中的错误。最终，我通过将字符串转换为固定长度的字节数组来解决它，这样大小就可以正确计算并相互匹配。

下面是在 Rust 中表示字符串变量的字节数组的结构。

```
const SIZE: usize = 512;#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct GreetingAccount {    
    pub _field1: [u8; SIZE],
}
```

注意:指令(`#[derive(BorshSerialize, BorshDeserialize, Debug)]`)是让`BorshSerialize`和`BorshDerialize`应用于自定义结构类型`GreetingAccount`。

下面是字节数组 struct 的类型脚本代码，账户存储数组的空间可以通过`borsh.serialize( GreetingSchema, new GreetingAccount(),).length;`计算出来

```
class GreetingAccount {  
    jsonstring = new Uint8Array(SIZE);  
    constructor(fields: {jsonstring: Uint8Array} 
| undefined = undefined) {    
          if (fields) {      
              this.jsonstring = new Uint8Array(fields.jsonstring); 
              console.log("get string",fields.jsonstring);    
          }
  }}/** * Borsh schema definition for greeting accounts */
const GreetingSchema = new Map([  
[GreetingAccount, 
{kind: 'struct', fields: [['jsonstring',[SIZE]] ]}]
]);borsh.serialize(  GreetingSchema,  new GreetingAccount(),).length;
```

接下来，我需要解决定长限制。在实践中，字符串长度会随着时间的推移而变化，我将数组大小设置为一个足够大的值，并用 0 位填充字节数组。字符串字符字节将被写入字节数组，其余字节为零位。我们可以通过读取字节并截断尾随的零字节来将其转换回字符串。

下面是用零填充字节数组的 Rust 代码。

```
fn fill_from_str(mut bytes: &mut [u8], s: &[u8]) {
    bytes.write(s).unwrap();
}let new_b = // new string data in byte array

let n = new_b.len();    
let mut bytes: [u8; SIZE] = [0; SIZE];    
if n >= SIZE {
   new_account._field1.clone_from_slice(&new_b[0..SIZE]);    
} else {        
   fill_from_str(&mut bytes,new_b );
   new_account._field1.clone_from_slice(&bytes[0..SIZE]);    
}
```

一开始，我想将`SIZE`设置为一个大值，然而，我发现当我将其设置为大于 512 的值时，`borsh`序列化/反序列化库会抛出错误。似乎库函数对数组长度有一些限制。另一个限制是每个计划状态帐户必须小于 10 MB，尽管我们可以将多个帐户传递给智能合同处理器。

下面是序列化/反序列化的代码。`try_from_slice`是将账户数据反序列化为强类型结构。然后新更新的结构`new_account`将`serialize`放入账户数据中。

```
// Deserialize the account data into the struct type variables.let mut greeting_account =
        GreetingAccount::try_from_slice(&account.data.borrow())?;// Serialize new string into the account data 

new_account.serialize(&mut &mut account.data.borrow_mut()[..])?;
```

下面是在智能合约更新字符串变量后反序列化帐户数据的 typescript 应用程序。

```
const accountInfo = await connection.getAccountInfo(greetedPubkey);
const greeting =
 borsh.deserialize(GreetingSchema,GreetingAccount,accountInfo.data);   console.log( Buffer.from(greeting.jsonstring.buffer).toString());
```

最后，我分享一些我学到的有用的调试工具。这里是日志记录功能，让您检查日志中的参数数据。如果智能合约抛出任何错误，日志将显示在前端应用程序事务提交调用中。

```
sol_log_params(accounts, _instruction_data);    sol_log_slice(&account.data.borrow());
```

帐户数据可以通过 Solana cli 显示。

```
solana account <account pub key address>
```

[Rust 智能合约](https://github.com/iwasnothing/solana-smart-contract/blob/main/src/program-rust/src/lib.rs)和[前端打字稿 app](https://github.com/iwasnothing/solana-smart-contract/blob/main/src/client/json_contract.ts) 的完整代码可以在我的 [Git](https://github.com/iwasnothing/solana-smart-contract) 中找到。