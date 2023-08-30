
### Get the latest blockhash

- Get the `blockhash` of the `latest block` from any of public EN on Cypress
- Submit the `blocknumber` and the `blockhash` to the designated smart contract
  - Verify Contract: 0x941d2Cf7dcE933b9928281A6Dcc4166386747D3E
  - Verify function: ```function verify(uint blocknum, bytes32 hash) public returns (bool)```
- Sender who calling the verify by transaction will get the NFT!

#### How to call the verify function?
  - Using klaytnfinder’s [WriteContract](https://www.klaytnfinder.io/account/0x941d2cf7dce933b9928281a6dcc4166386747d3e?tabId=contract&subTabId=writeContract) feature
  - Using klaytnscope’s [WriteContract](https://scope.klaytn.com/account/0x941d2Cf7dcE933b9928281A6Dcc4166386747D3E?tabId=contractCode) feature
  - Using [caver-js](https://www.npmjs.com/package/caver-js) or [web3klaytn](https://github.com/klaytn/web3klaytn)
