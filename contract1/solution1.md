## Pitfall

> All signature checking functions must comply with the [NULLFAIL][bip146] rule which only allows `0x` as an invalid signature — any other invalid signature will **immediately fail** the entire script.

furthermore

> The operators || and && don't apply common short-circuiting rules. This means that in the expression f(x) || g(y), g(y) will still be executed even if f(x) evaluates to true.

This means that the double signature check against the same `userSig` will always fail the script, locking funds in the contract and making them unspendable:

```solidity
    require(checkSig(userSig, pkPerson0) || checkSig(userSig, pkPerson1));
```

## Solution

The `NULLFAIL` rule means passing an invalid  signature to `checkSig()` does not return `false` — it fails the script. To safely return `false` on a signature check, use an empty `0x` signature instead, as shown below:

```solidity
// instead, use 2 different  signatures
// set the unused signature to 0x so 'checkSig' returns false instead of failing the script
require(checkSig(userSig0, pkPerson0) || checkSig(userSig1, pkPerson1));
```

## Relevant Documentation

null-fail rule:
https://next.cashscript.org/docs/language/functions#signature-checking-functions

no short-circuiting rules:
https://next.cashscript.org/docs/language/types#boolean