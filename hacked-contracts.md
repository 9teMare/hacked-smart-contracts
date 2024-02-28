---
title: Hacked Smart Contracts
---
## 1. Skyward Finance

| Date    | Classification | Loss |
| -------- | ------- | ---- |
| 2022.11.1  | DeFi    | $ 1M NEAR

### Links
https://twitter.com/skywardfinance/status/1587947957789331457

https://www.theblock.co/post/182495/skyward-finance-exploit-near-protocol

https://nearblocks.io/address/5ebc5ecca14a44175464d0e6a7d3b2a6890229cd5f19cfb29ce8b1651fd58d39

[Near Transaction 92Gq7zehKPwSSnpoZ7LGGtSmgmBb4wP2XNDVJqUZRGqz | NearBlocks](https://nearblocks.io/txns/92Gq7zehKPwSSnpoZ7LGGtSmgmBb4wP2XNDVJqUZRGqz)

### Contract
https://github.com/skyward-finance/contracts/blob/master/skyward/src/treasury.rs#L158

In this transaction, the hacker redeemed more than 1.1 million wrapped Near tokens ($3 million) in a loop from Skyward’s treasury contract.

BlockSec found a bug in the contract's token-redemption function that failed to check for duplicate token account IDs, the firm said in a statement shared with The Block.

The incident comes as crypto hacks continue to grow. Just last month, as many as 44 exploits accounted for more than $650 million in losses.


---

## 2. ThirdWeb
| Date    | Classification |
| -------- | ------- |
| 2023.12.5  |  Infra   |
   
### Links
https://blocksec.com/blog/10-third-web-incident-incompatibility-between-trusted-modules-exposes-vulnerability (contracts are inside)

On December 5, 2023, Web3 development platform Thirdweb reported security vulnerabilities in their pre-built smart contracts. This flaw impacted all ERC20, ERC721, and ERC1155 tokens deployed using these contracts. In the following days, tokens deployed with the vulnerable contracts were progressively exploited in attacks.

#### ERC-2771 + Multicall

The issue arises due to inconsistencies in how calldata is packed and unpacked between these two components (ERC-2771 and Multicall). As per ERC-2771, the trusted forwarder should pack the message data and sender information together. The contract then uses _msgData() and _msgSender() to unpack the message data and sender information, respectively.

However, the multicall function is not compatible with how ERC-2771 packs data. If implemented correctly, Multicall should use _msgSender() to unpack the sender information and append it to each message's call data so that it can be unpacked properly in subsequent calls. But this step in the actual implemeantion is missed.

Meanwhile, the contract following ERC-2771 will try to unpack message data and sender information using _msgData() and _msgSender(). However, without the sender information appended to calldata, the sender information is unpacked as the last 20 bytes of _msgData(), which the attacker can control. This allows an attacker to construct manipulated calldata that executes malicious logic with an arbitrary sender information, violating the expectations set by the specifications.

---

## 3. SushiSwap
| Date    | Classification | Loss |
| -------- | ------- | ------- |
| 2023.4.9  |  DeFi   | $ 3.3M

### Links
https://blocksec.com/blog/8-sushi-swap-incident-a-clumsy-rescue-attempt-leads-to-a-series-of-copycat-attacks (contracts are inside)

https://phalcon.blocksec.com/explorer/tx/eth/0x43ff7e01423044cfb501b4fe9ef1386725c0ddc117dadd6e6620cb68bdeaf4f9

#### The Vulnerability
Unverified External Parameter
The RouteProcessor2 contract's processRoute() allows users complete control over the call flow (parameter route).

---

## 4. ParaSpace / Parallel Finance
| Date    | Classification | Loss |
| -------- | ------- | ------- |
| 2023.3.17  | DeFi    | $ 5M (prevented)

### Links
https://blocksec.com/blog/paraspace-incident-a-race-against-time-to-thwart-the-industrys-most-critical-attack-yet (contracts are inside)

---

## 5. Curve
| Date    | Classification |
| -------- | ------- |
| 2023.7.30  | DeFi  |

### Links
https://blocksec.com/blog/curve-incident-compiler-error-produces-faulty-bytecode-from-innocent-source-code (contracts are inside)

The vulnerability arises from a compiler bug that results in a lack of reentrancy protection.

---

## 6. Euler Finance
| Date    | Classification |
| -------- | ------- |
| 2023.3.13  | DeFi  |

### Links
https://blocksec.com/blog/euler-finance-incident-the-largest-hack-of-2023 (contracts are inside)

The root cause of this incident is due to the lack of insolvency check in the function donateToReserves(). Specifically, the vulnerable contract provides a functionality for users to donate their collateral to the protocol without checking if the user's position was solvent. What's worse, to get rid of this bad position, the protocol offered a large discount for liquidators to pay less debt to liquidate this position. The attacker created a large position and made this position insolvent by exploiting this functionality. Then, he was able to buy his collateral at a discount to profit.

---

## 7. KyberSwap
| Date    | Classification | Loss |
| -------- | ------- | ------- |
| 2023.11.23  | DeFi  | $ 48M |

### Links
https://blocksec.com/blog/kyberswap-incident-masterful-exploitation-of-rounding-errors-with-exceedingly-subtle-calculations (contracts are inside)

https://blocksec.com/blog/yet-another-tragedy-of-precision-loss-an-in-depth-analysis-of-the-kyber-swap-incident-1

The fundamental issue originated from incorrect rounding direction during KyberSwap's reinvestment process. This subsequently led to improper tick calculations and, ultimately, to double counting of liquidity.

---

## 8. Hundred Finance
| Date    | Classification | Loss |
| -------- | ------- | ------- |
| 2023.4.16   | DeFi  | $ 7.4M |

### Links
https://blocksec.com/blog/6-hundred-finance-incident-catalyzing-the-wave-of-precision-related-exploits-in-vulnerable-forked-protocols (contracts are inside)

The attack involved two main issues:

- A precision loss issue (an incorrect rounding issue);
- A empty markets, which allowed the hacker to manipulate the exchangeRate.

---

## 9. Platypus
| Date    | Classification | Loss |
| -------- | ------- | ------- |
| 2023.2.17   | DeFi  | $ 9.05M |
| 2023.7.12   | DeFi  | $ 50K |
| 2023.10.12   | DeFi  | $ 2.2M |

### Links
https://blocksec.com/blog/5-platypus-finance-surviving-three-attacks-with-a-stroke-of-luck (contracts are inside)

#### Attack 2: 

https://explorer.phalcon.xyz/tx/avax/0x20a88fff17d946c5eb3a4b1343fac1ba72cbbb625bb179a71b2cc0517f3954a5

https://phalcon.blocksec.com/explorer/tx/avalanche/0x20a88fff17d946c5eb3a4b1343fac1ba72cbbb625bb179a71b2cc0517f3954a5

#### Attack 3: 

https://twitter.com/BlockSecTeam/status/1712445197538468298

https://phalcon.blocksec.com/explorer/tx/avalanche/0xab5f6242fb073af1bb3cd6e891bc93d247e748a69e599a3744ff070447acb20f

https://phalcon.blocksec.com/explorer/tx/avalanche/0xab5f6242fb073af1bb3cd6e891bc93d247e748a69e599a3744ff070447acb20f