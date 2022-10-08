# Withdrawal Fee

Withdrawing on Exegol may incur a withdrawal fee. The withdrawal fee has been instituted to dissuade frequent withdrawals, which enables the team to have a higher capital utilisation (increasing overall APR), and creates an economic deterrent to any smart contract vulnerabilities that may be discovered. 

The maximum withdrawal fee is currently 10% of the withdrawal output at the `start block`, and _linearly decreases over time_, becoming zero after approximately 100800 L1 blocks, which is approximately 14 days. 

The Exegol team may adjust the maximum withdrawal fee and decay duration depending on user requirements and protocol dynamics.

!!!info
Swaps on DEXes are not subject to a withdrawal fee, but may be subject to swap fees. However swapping on a DEX may reset the `start block` for the recipient wallet. Users are encouraged to compare withdrawing on a DEX and via the official website.
!!!

The `start block` is tied to a wallet. The `start block`
- is set when the wallet buys eUSD for the first time via the official website or anytime on a DEX
- is moved forward for the recipient when transferring eUSD if sender has a more recent `start_block` (may affect DEX swaps)
- is moved forward when withdrawing on the official website

## Example Scenario

|              |                  |
| ------------ | ---------------- |
| Fee duration | 100800 L1 blocks |
| Max fee      | 10%              |

1. User 1 buys eUSD via the website at L1 block 1570000. 
    > Withdrawal fee linearly decays and becomes zero at L1 block 1670800.
2. User 1 withdraws some eUSD via the website at L1 block 1620400. Withdrawal fee is 50% of the max fee, which is 5%.
    > `start block` is now 1620400, and the withdrawal fee will be zero at L1 block 1721200.
3. User 1 swaps eUSD to USDC on a DEX at L1 block 1620500.
    > `start block` is unchanged. However the `start block` for the DEX contract may be increased, affecting subsequent eUSD buyers.
4. User 1 sends eUSD to User 2 at L1 block 1620600.
    > User 1's `start block` does not change, however User 2's `start block` is set to 1620600. The withdrawal fee for User 1 is unchanged, and for User 2 will be zero at L1 block 1721400.
5. User 1 buys more eUSD via the website at L1 block 1620700.
    > User 1's `start block` does not change.
6. User 1 buys more eUSD via the website at L1 block 1620800.
    > User 1's `start block` may be updated to the DEX contract's `start block`.