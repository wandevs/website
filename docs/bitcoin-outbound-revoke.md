---
layout: page
title: Revoke an Bitcoin Outbound Transaction
---

The outbound Bitcoin revoke is essentially identical to the outbound Ethereum
revoke. With that said, let's start by making a new script file for the revoke.

```bash
$ vi wbtc2btc-revoke.js
```

Copy over the top portion of previous Bitcoin outbound, though as before make
sure to add in the redeemKey generated by the expired outbound transaction.

```js
const opts = {
  ...
  redeemKey: {
    x: '<the x value>',
    xHash: '<the xHash value>',
  }
};
```

Then we can set up the revoke call.

```js
Promise.resolve([])
  .then(sendRevoke)
```

Now define the `sendRevoke` function.

```js
function sendRevoke(txCount) {

  // Get the raw revoke tx
  const revokeTx = cctx.buildRevokeTx(opts);

  // Send the revoke transaction on Bitcoin
  const receipt = await utils.sendRawWanTx(web3wan, revokeTx, opts.from, wanPrivateKey)

  console.log('Revoke sent:', receipt);
}
```

Finally, go ahead and run the script.

```bash
$ node btc2wbtc-revoke.js
```