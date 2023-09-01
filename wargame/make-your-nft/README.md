### Make your NFT

- Deploy NFT by [Klaytn online toolkit](https://toolkit.klaytn.foundation/kct/KIP17Deploy)
  - NFT name must be “TASK”
- Mint the NFT to your address
- Submit the `NFT address` to the designated smart contract
  - Verify Contract: 0x6f59cd173e8f93840ef2cabbaa851c81467d0cfe
  - Verify function: ```function verify(address NFTAddress) public returns (bool)```
- Sender who calling the verify by transaction will get the NFT!

#### How to call the verify function?
  - Using klaytnfinder’s [WriteContract](https://www.klaytnfinder.io/account/0x6f59cd173e8f93840ef2cabbaa851c81467d0cfe?tabId=contract&subTabId=writeContract) feature
  - Using klaytnscope’s [WriteContract](https://scope.klaytn.com/account/0x6f59cd173e8f93840ef2cabbaa851c81467d0cfe?tabId=contractCode) feature
  - Using [caver-js](https://www.npmjs.com/package/caver-js) or [web3klaytn](https://github.com/klaytn/web3klaytn)

#### Lecture
- [Klaytn Dev Bootcamp #2](https://www.youtube.com/watch?v=HbPFI2-C2s8&list=PLmYPZbd2veWKWZGbT3kxnjRr9sJAYDiOs&index=2)