### Get the latest blockhash

- Deploy your own contract that additionally develope following two functions by hardhat with [contract-demo-poll](https://github.com/klaytn/contract-demo-poll) repository
  - totalVotes() is a read-only function that returns total number of votes (cat + dog)
  - getOwner() is a read-only function that returns contract owner’s address
- Submit the `contract address` and the `NFT receiver address` to the designated smart contract
  - Verify Contract: 0xd6b655e1f3ecdf95649a9bb79d7e562227b369e8
  - Verify function: ```function verify(address pollAddr, address NFTReceiver) public returns (bool)```
- NFT receiver will get the NFT!

#### How to call the verify function?
  - Using klaytnscope’s [WriteContract](https://scope.klaytn.com/account/0x941d2Cf7dcE933b9928281A6Dcc4166386747D3E?tabId=contractCode) feature
  - Using [caver-js](https://www.npmjs.com/package/caver-js) or [web3klaytn](https://github.com/klaytn/web3klaytn)

#### Lecture
- [Klaytn Dev Bootcamp #5](https://www.youtube.com/watch?v=7gSsFxqFbGk&list=PLmYPZbd2veWKWZGbT3kxnjRr9sJAYDiOs&index=5) (korean)