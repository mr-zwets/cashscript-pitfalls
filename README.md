# CashScript Pitfalls

Repo with example CashScript smart contracts which each contains a critical mistake!

Test your knowledge of CashScript and BitcoinCash by investigating the contracts 🔎

> **Note:** Only 1 of the 3 pitfalls still exists in practice today. Contract2's pitfall was resolved in CashScript v0.13+ (strict parameter type enforcement), and Contract3's pitfall was resolved by the May 2026 network upgrade ([CHIP-2024-12 P2S](https://github.com/bitjson/bch-p2s), which relaxed output standardness rules). This limits the repo's usefulness as a learning exercise, but the resolved examples remain useful for understanding the historical quirks. Only Contract1 (`SharedFunds`) demonstrates a pitfall that still applies.

## Contracts

- Contract1: `SharedFunds` tests knowledge of the CashScript documentation / understanding of underlying low level-opcodes
- Contract2: `SharedVault` tests knowledge of CashScript quirks (v0.12 and prior — resolved in v0.13+)
- Contract3: `LastToRefreshWins` tests knowledge of the Bitcoin Cash network rules (resolved by the May 2026 P2S upgrade)