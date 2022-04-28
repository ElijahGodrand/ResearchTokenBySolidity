SHIBA INU，缩写SHIB，又叫SHI币。它是以太坊ERC20代币。在EtherScan输入SHIBA合约的地址0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE，可以在“contract”-->“code”看到其源码，直接看这里也行
https://etherscan.io/address/0x95ad61b0a150d79219dcf64e1e6cc01f0b64c4ce#code

SHIB的官方主页 https://shibatoken.com ，twitter: @shibtoken。coinmarketbase也有一些有帮助的信息 https://coinmarketcap.com/currencies/shiba-inu/ 。主要信息就这些了。

源码总共497行，大部分是注释。第一部分“interface IERC20 ”是ERC20的接口定义。注意ERC20有9个函数，2个事件，这块只有6个函数，2个事件，name(), symbol(),decimal()三个函数没写，没写的原因，将来把name, symbol, decimal定义成公有变量，编译后自动生成相应函数。

第二部分“library SafeMath”，顾名思义，安全的算术运算：加、减、乘、除、求余，解决加和乘的溢出，以及减、除、求余的大于零等于零问题。这块也差不多标准化了，凡是智能合约这块都有类似的内容。为了节省代码空间和gas费用，这个库没有判断所有可能，仍然依赖于调用者的细致耐心。

第三部分“contract ERC20 is IERC20 ”，这部分最重要。实现了ERC20函数，函数名下划线打头的是内部函数。除了ERC20函数之外，还实现了其他功能，比如_mint和_burn。实现方式中规中矩，没有花头。ERC20比较难理解的是approve和allowence，由此又引起对transFrom的理解。

第四部分“ contract TokenMintERC20Token is ERC20 ”。最后一部分。这部分很简单，实现构造函数，传入参数。

结论：SHIB的智能合约，是相当标准的发币合约，规范，注释详细，单纯地发币，没有任何花头，比如投票，比如智能合约升级。因为它完全没有任何“个性化”的东西，因此未来发币的筒子们可以直接用它部署，部署的时候在构造函数填上新参数即可。
