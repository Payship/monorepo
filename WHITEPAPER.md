# Payship: Pool-based crypto lending across all ERC20 tokens

*Veronika Voss, Daniel D. Feist — July 2020*

### Abstract

Payship is a major step forward in **crypto lending**: Deposit any ERC20 token. Use any ERC20 token as collateral. Earn interest on any deposit. Borrow any ERC20 token. Stake PSHP to earn a portion of Payship income. Vote with PSHP on Payship future.

Payship is a major step forward in **lending economics**: Collateral factors and interest rates of deposits and borrows are re-calculated once a day based on the performance of the entire Ethereum ERC20 token ecosystem. 

Payship is a major step forward in **borrower protection**: Every rate has a 24-hour guarantee through the single re-calculation once a day. Every borrower found under liquidation after the re-calculation has 24 hours to fix the position before being liquidated on the next re-calculation. Off-chain Systems Model (refer to the section below) enables automatic borrower protection from liquidation in case of a price increase on a borrowed asset or price decrease on a collateral: in case of a borrower going below the liquidation threshold, Payship can automatically and for free repay a portion of the loan using the collateral.

Payship is a major step forward in **lender protection**: Upon every deposit the lender instantly receives back to the wallet the equivalent value in Payship platform ERC20 stablecoin, the PSD (Payship Dollar). The PSD is unique because while it aims to maintain a peg to the dollar on the open market, within the Payship platform it maintains a peg to each lender's deposit. It means within the Payship platform the value of PSD will be different for each lender. This also means that the lender has a choice in the event the deposit value changes due to price fluctuations of the underlying token: use the initial deposit value denominated in PSD in the lender's wallet and forego the original token, or swap PSD and take the original token out.

Payship is a major step forward in **gas costs**: Through native use of Ethereum blockchain transfers and smart off-chain transactions, Payship wants to ensure most interactions are free and on-chain deposits/withdraws cost no more than 0.002 ETH ($0.64 @ $320 / ETH).

Payship vision sees all ERC20 tokens having a purpose (no more "sh%tcoin" names). Payship core functionality is truly autonomous (no more "whale voting" on rate curves and collateral factors). Payship runs on Ethereum and aspires to be like Ethereum, if Ethereum was built today with AMM & DEX functionality buil-in natively on-chain.

## Introduction

Currently, crypto lending platforms are decentralized on the protocol level, but not on the administration level. Each platform has its form of governance (private or public), its system of interest rates and collateral factors. In both forms of governance, there are "leaders" who control the majority stake and steer decisions.

The interest rates and collateral factors on these lending platforms are decided either by algorithms with variables set by "leaders" or by governance voting dominated by "leaders." This is a semi-decentralized state.

To achieve a true decentralized and autonomous organization, it's imperative to abstract from the urge to control and regulate the market rates. The global ERC20 market data is sufficient to define variables to algorithmically regulate the interest and collateral rates on its own.

The same goes for the limited choice of ERC20 tokens available for deposits and borrowings. They too, are decided by "leaders" or by governance voting dominated by "leaders". There's no autonomy. Payship is different.

## Payship Overview

The basic principles that Payship operates on can be divided into three models: Economics, Systems and Rewards.

### Economics Model

1. **All ERC20 tokens can be useful.** To prevent spam, Payship will take into account only tokens older than 90 days (since contract creation transaction date). For now, ERC777 tokens are not considered due to their "exotic" properties and unexpected behaviours.

2. **All ERC20 tokens can be used as collateral.** Global ERC20 token market defines the rates according to a specified algorithm.

   - **Stability Factor.** This percentage defines token volatility calculated as: 
     ```
           [token's last 30 days % change] + [token's last 90 days % change] + [token's last 180 days % change]
     100 - ––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––
                                                           3
     ```

   - **Volume Factor.** This percentage defines token popularity in the ERC20 ecosystem and is calculated as:
     ```
           100 * [token's average daily volume across last 90 days]
     ––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––
     [average daily total volume across all ERC20 tokens in last 90 days]
     ```

   - **Collateral Factor.** This percentage defines token borrowing power calculated as:
     ```
     75% * [Stability Factor] * [Volume Factor]
     ```
     As such, no deposit can borrow more than 75% of its value.

3. **All ERC20 token deposits can earn interest, all ERC20 tokens can be borrowed provided there's supply.**

   - **Token Deposit Interest Rate**. This percentage is calculated as:
     ```50% * [Token Borrow Interest Rate]```
   
   - **Token Borrow Interest Rate**. Utilization is calculated as: 
     ```
                 [tokens in borrows]
     ––––––––––––––––––––––––––––––––––––––––––––
     ([tokens in borrows] + [tokens in deposits])
     ```
     Utilization percentage is then applied to the rate curve: if utilization is lower than token collateral factor, interest rate is: 
     ```
          [utilization]
     ––––––––––––––––––––––––
     (2 * [Stability Factor])
     ```
     otherwise it is: 
     ```
        [utilization]
     ––––––––––––––––––
     [Stability Factor]
     ```

4. **All ERC20 token deposits are insured towards lenders via the PSD stablecoin.** The initial supply of PSD will be created through a Liquidity Generation Event, building a solid collateral.

5. All economic updates happen once a day at 09:00 AM UTC.

6. All economic models can be adjusted internally during the beta period. Further adjustments after full launch will be performed by the PayshipDAO.

### Rewards Model

0. Total PSHP supply will be no more than 11,000 tokens. Total PSD supply will be dependent on the underlying collateral.

1. **Phase 0 – ILO:** 11,000 PSHP tokens are minted at the inception of Payship, with the following distribution:
  
  - 1,000 PSHP tokens are given away proportionally to the top 32 SwapShip (SWSH) holders based on an Oct 10, 2020 snapshot.
  - 4,000 PSHP tokens are offered in a 5 day presale starting on Oct 12, 2020 with a starting price of 0.25 ETH per 1 PSHP.
  - 2,000 PSHP tokens are reserved for DEX and/or CEX release. The first DEX launch will happen on Uniswap with a starting price of 0.4 ETH.
  - 2,000 PSHP tokens are reserved for the team and locked after the presale for at least 6 months.
  - 2,000 PSHP tokens are reserved for advisers, promotions and marketing.

2. **Phase 1 – Pilot:** 100% of Payship daily income denominated in PSD since the pilot launch of Payship will be distributed among wallets that connect to Payship and become active participants of lending and borrowing, proportionate to each wallet holdings: 
```
[wallet deposits + wallet borrows]
––––––––––––––––––––––––––––––––––
 [total deposits + total borrows]
```
The pilot will last 14 days.

3. **Phase 2 – Soft Launch:** Every wallet that decides to stake PSHP in the Payship staking pool will receive daily PSD proportional to its stake and daily Payship income: 
```
[100% of Payship daily income denominated in PSD] * [wallet PSHP staked] * [wallet deposits + wallet borrows]
–––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––
                          [total deposits + total borrows] * [total PSHP staked]
```

### Systems Model

Payship proposes an experiment to minimise gas costs and its impact on platform operations (transaction delays, errors, drops and denial attacks). Instead of starting with smart contracts outright, Payship proposes a user-to-platform transaction-based deposit/withdrawal model. Similar to how CEX operates, platform actions would be executed off-chain. Then they could be batched and sealed on-chain in a single transaction, minimising costs, on user's request.

The deposit flow is as follows:

1. Lender deposits token A in amount Z of value X USD from lender's wallet address 0xABC...XYZ
2. Lender receives PSD token in amount Y of value X USD to lender's wallet address 0xABC...XYZ
3. Later on, to redeem token A, lender can either deposit back the amount Y of PSD token and receive back token A in amount Z (which market value may or may not still be X USD), or the lender can forego token A and keep the PSD token in amount Y of value approx. X USD (it's more likely that PSD keeps its value than token A).

The borrow flow is simpler: borrower receives the token B of borrower's choice in amount V of value W USD, and must repay using that same token B in amount V. Token value can change in either direction, which may be a cause of liquidation in the even token B price increases, while borrower's collateral does not.

This model needs experimenting and balancing the levels between user convenience and user trust. The correct balance should be found within bounds between a fully CEX approach (on-chain transfer transactions representing deposits/withdrawals only) and a fully DEX approach (on-chain smart contract transactions representing all platform operations).

## Conclusion

Payship offers a uniquely open, decentralized and autonomous organization on the economics level. Payship does not discriminate or put preference towards tokens and users. Payship tries to increase lenders and borrowers safety. Payship proposes a rewards model that incentivizes platform use and offering revenue sharing, and – in the future – governance as well.

Payship gives the whole ERC20 ecosystem the ability to obtain additional capital from collateral, with significantly smaller transaction costs than existing platforms.

Payship is a Decentralized interest rate policy. Payship is an Autonomous economy model. Payship is an Organization of stakeholders. Payship is DAO. Welcome to Payship.org
