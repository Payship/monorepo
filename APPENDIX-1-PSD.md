# PSD: Payship Standard Denominator

*Veronika Voss, Daniel D. Feist — December 2020*

### Abstract

Payship Standard Denominator (PSD) is a new stablecoin designed for the Payship/Swapship lending/dex and the RTC Ecosystem. It is a super-stablecoin: using a fixed 1:1 ratio to the major existing stablecoins (initially to DAI, USDC & USDT) it is in a super-position, tethered to each of them at the same time.

The 1:1 ratio is maintained by the PSD smart contract. The market value is maintained by the three corresponding Uniswap pools: DAI-PSD, USDC-PSD and USDT-PSD. The market incentive to support PSD exists in the arbitrage opportunity within the DAI-USDC-USDT triangle between the real PSD value within each Uniswap pool and the 1:1 value within the PSD smart contract.

```
              DAI
               .
               .
               .
              PSD
            .     .
         .           .
      .                 .
USDC                       USDT
```

## Introduction

Payship Standard Denominator is the stablecoin for the Payship lending platform and the Swapship DEX. To be more precise, the PSD and accompanying smart contracts **are** the Payship and Swapship platforms.

When a person swaps one token for another using Swapship, the first token is sold for PSD and the second is bought with PSD through the Swapship L2 exchange (initially not available to public).

When a person deposits a token to Payship, they receive the at-the-time value of that token in the amount of X PSD. When they want to withdraw the token from Payship to unlock their deposit+interest, they need to return the exact same amount of X PSD, no matter the current value of the token or PSD.

When a person borrows a token from Payship, they need to repay the loan+interest in either the token itself or in PSD at token's value at the moment of the repayment.

This makes PSD a super-stablecoin and a super-arbitrage across all the ERC20 tokens available on Payship and Swapship.

## Mechanics & Security

The PSD smart contract and the Uniswap pools are an integral part of the PSD mechanics.

1. The PSD smart contract allows anyone to mint and burn the PSD tokens.

2. To mint the PSD tokens, a person must supply any amount of DAI, USDC or USDT (collateral). The minting fee is 0.3% (like the Uniswap fee to buy PSD from the pools, but with 0% slippage!). The PSD smart contract has a fixed minting ratio of 1:1 (unlike the Uniswap pools).

3. To redeem DAI, USDC or USDT, a person must burn PSD. The PSD smart contract has a fixed burning ratio of 1:1. The burning fee is 0.3%, but slippage is 0%!

4. The above two points mean that PSD can be used to exchange between stablecoins with 0% slippage! But with a fixed fee: depending on implementation it could be 0.3% bypassing PSD mint/burn, or 0.6% if done through the mint/burn process.

5. To prevent flash-loan attacks, burning and minting within the same Ethereum block is disabled (per-address or global depending on market conditions).

6. To prevent excessive arbitrage, burning is limited to 5,000 PSD tokens per block (adjustable). The limit will be increasing with PSD market liquidity and collateral increasing.

7. Burning/minting will input/output, depending on the choice of the function caller, a single collateral, or the triage split depending on the PSD smart contract deposited collateral. Combined with a stablecoin exchange implementation mentioned in 4) this mechanism could give an opportunity to, for example, exchange 1,000 DAI for 500 USDC and 500 USDT within one transaction. 

8. The PSD smart contract makes it possible to include more stablecoins to super-impose PSD against. This will expand PSD arbitrage opportunities, increase its collateral and volumes, increasing the collected fees.

9. The PSD smart contract makes it possible to delegate minting to other smart contracts like Payship and Swapship, to seamlessly base these platforms on PSD.

10. PSD collects fees from all its implementations and secures them for: management by the RTC token holders, distribution towards PSHP and SWSH token holders, and more.

11. Corresponding PSD Uniswap pools determine the market value of PSD, but they are constantly adjusted by the arbitrage opportunity coming from the 1:1 fixed ratio of the PSD smart contract. The arbitrage limit is the amount of collateral within the PSD smart contract. As PSD adoption increases, the smart contract collateral increases, and the arbitrage opportunities increase as well.

12. Additional security limitations and mechanics may be added in the course of the PSD development depending on market conditions and behaviours.

## Conclusion

The goal of the PSD is to effectively become an index of the major stablecoins (a super-stablecoin). Through the fixed exchange ratio with each of the underlying stablecoins, PSD is pulling each stablecoin towards the equilibrium, while at the same time enabling super-arbitrage and constant volume within the PSD pools without taking into account other PSD applications.

Through constant volume, PSD ensures a stream of transaction fees supporting the RTC Ecosystem treasury and its sustainable development.
