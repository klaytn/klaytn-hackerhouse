### Couple NFT
_It actually need to make a NFT transfer transaction in multisig account. But to simply verify the achievement, let's just make multi signed signatures_
- Make a multi signed transaction by web3klaytn SDK
  - You can use [ethers-ext](https://github.com/klaytn/web3klaytn/tree/dev/ethers-ext), [web3j-ext](https://github.com/klaytn/web3klaytn/tree/dev/web3j-ext) or [web3py-ext](https://github.com/klaytn/web3klaytn/tree/dev/web3py-ext) in the web3klaytn
- Submit the `multisig address` that has 2 keys, the `sigHash`, `appended signatures as a string` and `NFT receiver address` to the designated smart contract
  - Verify Contract: 0xd6fCF7BA7f12607066dce9971a05371E4552D97b
  - Verify function: ```function verify(address sender, bytes32 msgHash, bytes calldata sigs, address NFTReceiver) public returns (bool)```
- NFTReceiver will get the NFT!

#### How to call the verify function?
- Update an account as a multisig account, see [below](#to-update-an-account-as-a-multisig-account)
- Send some KLAY for gas fee to the multisig account
- Sign any transaction by the multisig account by web3klaytn
- Make appended two signatures as a string, see [below](#to-append-two-signatures)
- Make a sigHash, see [below](#to-get-sighash)
- Call the verify function with all the arguments by web3klaytn

#### To update an account as a multisig account
```javascript
const { Wallet, TxType, AccountKeyType, JsonRpcProvider } = require("@Klaytn/ethers-ext");
const ethers = require("ethers");

async function main() {
  const provider = new JsonRpcProvider("https://public-en-cypress.klaytn.net");
  const wallet = new Wallet(senderPriv, provider);

  let senderNewPub1 = new ethers.utils.SigningKey(member1Priv).compressedPublicKey;
  let senderNewPub2 = new ethers.utils.SigningKey(member2Priv).compressedPublicKey;

  let tx = {
    type: TxType.AccountUpdate,
    from: wallet.address,
    gasLimit: 100000,
    key: {
      type: AccountKeyType.WeightedMultiSig,
      keys: [
        2, // threshold
        [
          [1, senderNewPub1],
          [1, senderNewPub2],
        ]
      ]
    }
  };

  let txHash = await wallet.sendTransaction(tx);
  let rc = await txHash.wait();
  console.log("receipt", rc);
}

main();
```

#### To append two signatures
```javascript
const { Wallet, JsonRpcProvider } = require("@Klaytn/ethers-ext");
const {ethers} = require("ethers")

const provider = new JsonRpcProvider("https://public-en-cypress.klaytn.net");
const wallet = new Wallet(senderPriv, provider);

// You can use any multi signed transaction(multiSignedTx) 
// with above multisig account
let decoded = wallet.decodeTxFromRLP(multiSignedTx) 
decoded = await wallet.populateTransaction(decoded) 

const sig1 = decoded.txSignatures[0]
const sig2 = decoded.txSignatures[1]
const s1 = ethers.utils.joinSignature({
   v:sig1[0],
   r:sig1[1],
   s:sig1[2]
})
const s2 = ethers.utils.joinSignature({
   v:sig2[0],
   r:sig2[1],
   s:sig2[2]
})
```

#### To get sigHash
```javascript
const {KlaytnTxFactory} = require("@klaytn/ethers-ext")
const {ethers} = require("ethers")

// decode is same with above
const ttx = KlaytnTxFactory.fromObject(decoded) 
const sigHash = ethers.utils.keccak256(ttx.sigRLP());
```