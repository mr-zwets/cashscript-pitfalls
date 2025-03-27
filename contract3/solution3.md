## Pitfall

The user provided argument `userLockingBytecode` is checked to be `bytes25` to match the length of a `P2pkhLockingBytecode` but it can still be a non-standard locking script.

## Solution

Use `new LockingBytecodeP2PKH()` to turn a `bytes20` item into a valid `P2pkhLockingBytecode`

```solidity
      // use bytes20 userPkh
      bytes userPkh = tx.inputs[0].nftCommitment;
      bytes25 userLockingBytecode = new LockingBytecodeP2PKH(userPkh);
      require(tx.outputs[0].lockingBytecode == payoutLockingBytecode);
```

## Relevant Documentation

Output Standardness:
https://next.cashscript.org/docs/compiler/script-limits#output-standardness

https://documentation.cash/protocol/blockchain/transaction/locking-script.html