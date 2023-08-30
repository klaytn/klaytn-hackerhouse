### Fee Delegation

- Make a fee-delegated transaction by web3klaytn SDK
  - You can use [ethers-ext](https://github.com/klaytn/web3klaytn/tree/dev/ethers-ext), [web3j-ext](https://github.com/klaytn/web3klaytn/tree/dev/web3j-ext) or [web3py-ext](https://github.com/klaytn/web3klaytn/tree/dev/web3py-ext) in the web3klaytn
- Call the verify function by a fee-delegated transaction
  - Verify Contract: 0x1c39604665DA84D4e81A747D95Ba3ef749DA502C
  - Verify function: ```function verify() public returns (bool)```
- Sender who calling the verify by transaction will get the NFT!

#### How to call the verify function?
- Below code is a `ethers-ext` example code that sends a `FeeDelegated valueTransfer` and you can use it as base code.
```javascript
const { Wallet, parseKlay, JsonRpcProvider, TxType } = require("@klaytn/ethers-ext");

const provider = new JsonRpcProvider("https://public-en-cypress.klaytn.net");

async function main() {
    const userWallet = new Wallet(senderAddr, senderNewPriv, provider);
    let tx = {
        type: TxType.FeeDelegatedValueTransfer,
        from: userWallet.address,
        to: “0xae...”,
        value: parseKlay("1"),
    }
    tx = await userWallet.populateTransaction(tx)
    // user signing
    const signedTx = await userWallet.signTransaction(tx)

    const feePayerWallet = new Wallet(feePayerPriv, provider);
    // fee payer signing and sending the transaction
    const txHash = await feePayerWallet.sendTransactionAsFeePayer(senderTxHashRLP);
    const rc = await txHash.wait()
}
```
- Setup the `user's private key`. It doesn't matter if the user have the KLAY
- Setup the `fee payer's private key`. Some KLAY should be in this account
- You should use `0xfc735e99` data that means calling verify function in the input field or of cource can use the contract instance web3 SDKs offer.
- Use the `TxType.FeeDelegatedSmartContractExecution` for transaction type