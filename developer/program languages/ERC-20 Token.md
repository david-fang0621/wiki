1. how to create and deploy an ERC-20 token on Ethereum.
   network: Rinkeby Testnet
   Contract name : FangElibToken
   Symbol: FangElib
   Metamask Account: 0x4721aAb706CbCd1111bB4edf57262255a662427D
   0x62da26ab856BEeC7FfC5c65088747910e221f845

faucets:
https://faucet.metamask.io/https://faucets.chain.link/rinkebyhttps://faucet.paradigm.xyz/

Contract Code:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "<https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol>";

contract LW3Token is ERC20 {
    constructor(string memory _name, string memory _symbol) ERC20(_name, _symbol) {
        _mint(msg.sender, 10 * 10 ** 18);
    }
}

```

1. Create An Ethereum Dapp with Ethersjs
   Ropsten Testnet faucet
   https://faucet.egorfine.com/https://faucet.ropsten.be/

ABI: [
{
"inputs": [],
"name": "getMood",
"outputs": [
{
"internalType": "string",
"name": "",
"type": "string"
}
],
"stateMutability": "view",
"type": "function"
},
{
"inputs": [
{
"internalType": "string",
"name": "_mood",
"type": "string"
}
],
"name": "setMood",
"outputs": [],
"stateMutability": "nonpayable",
"type": "function"
}
]

0x6D6718682eaBfE46eA65114087aB8752a4a8d8a8

1. https://github.com/LearnWeb3DAO/NFT-Tutorial
