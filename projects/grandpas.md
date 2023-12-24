## Grandpas Dashboard Project

### Client

Name: Theodore Thudium
Discord: PracticalPsychology#9608
Email: [practicalpsychologytips@gmail.com](mailto:practicalpsychologytips@gmail.com)

### GitHub

https://github.com/WhiteBoardCrypto/GrandpasDashboard

### Description of Project

I am looking to create a web3 portfolio tracker with a few different features. Mainly be able to track a bunch of assets on layer 2 chains (Polygon, BSC, Avax). Along with that, I'm looking for a long-term web3 developer(s) to help with other projects I have in mind, which are more advanced, but I don't want to jump into them.
Price is negotiable, I have never hired for a web3 dev job before.
Please share any past dApp or web3 projects you have helped on, or developed yourself. Thanks!

Goals:

- Let users create an account (so they don't need to import addresses each time they visit)
- Let users add their addresses (Ethereum, Solana, Terra, Bitcoin, Litecoin -> The value add is they cover MANY different chains)
- Let users add ENS or UnstoppableDomain names and auto-import all associated address (simplicity)
- Read multiple blockchains for ins/outs and calculate list of all trades. Treat an "ETH in" as a "buy" and an "ETH out" as a "sell".
- Show all trades in easy-to-view way like shown on image
- Create "Cost Basis" and "Total Value" graphs, based on crypto buys and sells
- ALL DeFi. No centralized exchanges integration.
- "Share with Friend" button that shares your whole current portfolio of buys/sells and gains/losses

https://docs.google.com/document/d/1BfPOjbGraId-MnBglBTt8DNXlzIhC6KrYlKizd3XmPY/edit?usp=sharing

1. expected budget is 2.2k
2. 4 milestones

- user auth and address management - $500
- track several chains - $1000
- user dashboard - $500
- publish the portfolio and share with friend - $200

1. Sure, I can get it

### deployment

[ec2-3-90-44-248.compute-1.amazonaws.com](http://ec2-3-90-44-248.compute-1.amazonaws.com/)

Mysql
grandpas
fang/fang123

### tracks all transactions on Ethereum

https://api.etherscan.io/api?module=account&action=txlist&address=0x61236DE2834fDcE9A4b4Fa3B68dDe39Eca7199Cb&startblock=0&endblock=99999999&sort=asc&apikey=YourApiKeyToken
txlistinternal
Result:
{"blockNumber":"13891477","timeStamp":"1640663942","hash":"0x6022965712585d9da814547a2e160177b37986c45cfd9643c2abef71925f9f6b","nonce":"18","blockHash":"0xc720bec78cbc4b6cb2947c0966ba1f795f3466ba385187a638d4a1ecba5dad6d","transactionIndex":"160","from":"0x937d83da523ac0e2e4e52cd9233c5152bea5f9d9","to":"0x61236de2834fdce9a4b4fa3b68dde39eca7199cb","value":"75000000000000000","gas":"21000","gasPrice":"87242639346","isError":"0","txreceipt_status":"1","input":"0x","contractAddress":"","cumulativeGasUsed":"10433472","gasUsed":"21000","confirmations":"145802"}

Web3.PHP

### tracks all transactions on Bitcoin

[!] [blockchain.com](http://blockchain.com/)https://blockchain.info/rawaddr/15urYnyeJe3gwbGJ74wcX89Tz7ZtsFDVewhttps://chain.api.btc.com/v3/address/15urYnyeJe3gwbGJ74wcX89Tz7ZtsFDVew/tx

{"block_height":641200,"block_hash":"000000000000000000084fc9b0d4aeb3807dcaf57440ac3b5f295ef3e0b01472","block_time":1595955558,"created_at":1595955566,"confirmations":79150,"fee":32461,"hash":"7cc731b889c158af28e184936499f59360cdbdbd39de203145ae00aebfe7c408","inputs_count":1,"inputs_value":1695387,"is_coinbase":false,"is_double_spend":false,"is_sw_tx":false,"lock_time":0,"outputs_count":2,"outputs_value":1662926,"sigops":8,"size":226,"version":1,"vsize":226,"weight":904,"witness_hash":"7cc731b889c158af28e184936499f59360cdbdbd39de203145ae00aebfe7c408","balance_diff":10000}

### polygonscan

https://api.polygonscan.com/api?module=account&action=txlist&address=0xb91dd8225Db88dE4E3CD7B7eC538677A2c1Be8Cb&startblock=0&endblock=99999999&page=1&offset=10&sort=asc&apikey=PJKEWH9I6S6M65J839XGD3FQRPWY2H1HCQ
PJKEWH9I6S6M65J839XGD3FQRPWY2H1HCQ
Description: 5 calls per second, 100,000 API calls per day

{"blockNumber":"19087857","timeStamp":"1631600445","hash":"0x72d4375b21207307ae0154542f1f9f3b99275596b846337efd30e6597e764f78","nonce":"0","blockHash":"0x2dfa320b3a606769bcc11e3bf62bbccc78e9ad554477053c6296eb9421a0584a","transactionIndex":"66","from":"0xb91dd8225db88de4e3cd7b7ec538677a2c1be8cb","to":"0xa81ce04168e41a47f68a975d67a00fbef729af9b","value":"0","gas":"500000","gasPrice":"1000000001","isError":"0","txreceipt_status":"1","input":"0xedca65250000000000000000000000000000000000000000000000000000009e1e9e1409000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000040000000000000000000000008f2172568ad3b2024b8cb29b03279e4b3d4849c8000000000000000000000000cccec4a90b3435065f5e1fec6346be9da1b7b5ed000000000000000000000000adbf1854e5883eb8aa7baf50705338739e558e5b000000000000000000000000853ee4b2a13f8a742d64c8f088be7ba2131f670d","contractAddress":"","cumulativeGasUsed":"19685967","gasUsed":"56112","confirmations":"5064244"}

### php artisan schedule:run

- php /path/to/artisan schedule:run 1>> /dev/null 2>&1

### coinmarketcap-api

### Test address

ETH - 0x61236de2834fdce9a4b4fa3b68dde39eca7199cb
1INCH_MATIC - 0xb91dd8225db88de4e3cd7b7ec538677a2c1be8cb, 0x4296E52C8CE3f9fD1605ce7fFb6eC6114804329C
BTC - 15urYnyeJe3gwbGJ74wcX89Tz7ZtsFDVew
SOL - Y2akr3bXHRsqyP1QJtbm9G9N88ZV4t1KfaFeDzKRTfr, 5XLqnSjJBAm1XjAcR76QCn8eB1phEQ3py2VAE2f8pdCQ
AVAX - 0xA0EBc93cd2e1F10994f7a7439B3c8D6B4786879f, 0x410b3d37245a424178829E6af34635d2BBf3CA39
BNB - 0x0e0237d697B5c6EC3759c893722C9aedD64a9F8d

### 2022-03-04 new requirements

1. Email registration whitelist (Google shoot API integration) - 350
2. Fix graph data (reverse it so the most recent date is on the right side, and also make it show the total value on the day, not just value received) - 200
3. Auto tokens import (web3.js) - 300

LUNA: 0x95224B45fBbaB92872b4CDfA39951bA4a4e3fDfE

USDC: 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48
DAI: 0x6B175474E89094C44Da98b954EedeAC495271d0F
TRX: 0xE1Be5D3f34e89dE342Ee97E6e90D405884dA6c67

LINK: 0x514910771AF9Ca656af840dff83E8264EcF986CA
BAT: 0x0D8775F648430679A709E98d2b0Cb6250d2887EF
USDT: 0xdAC17F958D2ee523a2206206994597C13D831ec7
UNI: 0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984
SHIB: 0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE
OMG: 0xd26114cd6EE289AccF82350c8d8487fedB8A0C07
ZRX: 0xE41d2489571d322189246DaFA5ebDe1F4699F498
MKR: 0x9f8F72aA9304c8B593d555F12eF6589cC3A579A2
GNT: 0xa74476443119A942dE498590Fe1f2454d7D4aC0d
LRC: 0xBBbbCA6A901c926F240b89EacB641d8Aec7AEafD

Fantom
Harmony
Optimism
Arbitrum
NEAR

0x9f81b91E4e614729B6b0F55B42BB6Dc22CEeDF0c FTM
one10sxq8rv9ngadjvmvfccsrcv8pcdfpvcc54y243 ONE
0x7462da033c5cceb21691d2447af34f3e333e0b85 OPTIMISM
0x29eee582ad17b96c8f41da6233bcf1a031addfe0 ARBITRUM

# Digital Ocean

IP: 159.223.115.227

MySQL:
username: fang0621
password: fang1234!
database name: grandpas
