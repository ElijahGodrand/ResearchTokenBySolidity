OpenZeppelin公司开源了openzeppelin-contracts项目：https://github.com/OpenZeppelin/openzeppelin-contracts。这是一个Solidity智能合约的库，已经有1.7万星了。

基于这个库开发以太坊代币，大概可以在10分钟搞定，非常方便。以4.6版本为例，有如下几步：

1.在Remix的主界面，以“load from github”方式导入如下4个文件：
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Context.sol
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol

注意：导入后，检查每个文件的import，看看是否有被遗漏的文件；各文件的solidity的版本要一致。

2.导入完毕后，在Remix的界面，出现一个目录“github”，在这个目录下，按照导入目录路径，存储了被导入的4个文件。

3.在Remix的contracts目录下，新建一个文件"shiba2.sol"，输入如下内容：
// contracts/SHIBA2022Token.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract SHIBA2022Token is ERC20 {
    constructor(uint256 initialSupply) ERC20("SHIBA INU 20220503", "SHIB") {
        _mint(msg.sender, initialSupply);
    }
}

注意：代币的名称和缩写在代码里定义了，部署的时候，再定义发多少代币。name和symbol放在源码里，通过编译过程确保字符串长度合理，以免部署的时候被恶意输入过长字符串导致溢出。

4.在Remix的部署页面，选择“ENVIRONMENT”为“JavaScript VM(london)”，"CONTRACT"为"SHIBA2022Token"，在“DEPLOY”设置构造函数参数"INITIALSUPPLY"为100000000，一亿。然后点击“Deploy”。

5.部署后，在“Deployed Contracts”出现“SHIBA2022Token”及其地址，在它下面，是SHIBA2022Token的各种函数，测试调用诸如"name"，"symbol"等函数，如果返回值符合预期，则表明部署成功。

