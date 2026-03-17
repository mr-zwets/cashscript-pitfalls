## Pitfall (v0.12 and prior)

> **Note:** This pitfall no longer exists in CashScript v0.13+, which strictly enforces function parameter types (bounded bytes and boolean values) at the compiler level.

The typings for the function arguments are only semantic, this means the length of bounded bytes type `bytes20` for `newAuthorizedPayoutPkh` is not enforced automatically and can be any length in reality.

This causes issues in `updateVault` because the nft commitment is overwritten with the new field:

```solidity
      bytes maximumWithdrawal = tx.outputs[0].nftCommitment.split(20)[1];
      bytes newCommitment = newAuthorizedPayoutPkh + maximumWithdrawal;
      require(tx.outputs[0].nftCommitment == newCommitment);
```

So if `newAuthorizedPayoutPkh` is 28 bytes, then the commitment would look like this:

```solidity
/*  --- State Mutable NFT ---
    bytes28 newAuthorizedPayoutPkh
    bytes8 old-maximumWithdrawal
*/
```
which would be overwrite the `maximumWithdrawal`

```solidity
/*  --- State Mutable NFT ---
    bytes20 newAuthorizedPayoutPkh
    bytes8 overwritten-maximumWithdrawal
    bytes8 unused-data
*/
```

## Solution

Add an explicit length check for the byte-length of the user argument:

```solidity
        // check if the lockingbytecode added to the state is of the expected length
        require(newAuthorizedPayoutPkh.length == 20);
```

## Relevant Documentation

In CashScript v0.12 and prior, the typings for the function arguments are only semantic, this means the length of bounded bytes types like `bytes20` are **not** contract enforced automatically. Instead add an explicit length check. Starting from v0.13, function parameter types are strictly enforced by the compiler.

https://next.cashscript.org/docs/language/contracts#functions