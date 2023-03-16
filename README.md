# Gogopool - Mitigation contest details

- Total Prize Pool: $32,000 USDC
- [Warden guidelines for C4 mitigation reviews](https://code4rena.notion.site/Guidelines-for-Versus-mitigation-reviews-ed10fc5cfbf640bd8dcec66f38b343c4)
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-02-gogopool-versus-mitigation-contest/submit)
- Starts February 10, 2023 20:00 UTC
- Ends February 15, 2023 20:00 UTC

## Important note

Each warden must submit a mitigation review for _every High and Medium finding_ from the parent contest. **Incomplete mitigation reviews will not be eligible for awards.**

## Findings being mitigated

### High Risk Findings

- H-01: [AVAX Assigned High Water is updated incorrectly](https://github.com/code-423n4/2022-12-gogopool-findings/issues/566)
- H-02: [ProtocolDAO lacks a method to take out GGP](https://github.com/code-423n4/2022-12-gogopool-findings/issues/532)
- H-03: [node operator is getting slashed for full duration even though rewards are distributed based on a 14 day cycle](https://github.com/code-423n4/2022-12-gogopool-findings/issues/493)
- H-04: [Hijacking of node operators minipool causes loss of staked funds](https://github.com/code-423n4/2022-12-gogopool-findings/issues/213)
- H-05: [Inflation of ggAVAX share price by first depositor](https://github.com/code-423n4/2022-12-gogopool-findings/issues/209)
- H-06: [MinipoolManager: node operator can avoid being slashed](https://github.com/code-423n4/2022-12-gogopool-findings/issues/136)

### Medium Risk Findings

- M-01: [RewardsPool.sol : It is safe to have the startRewardsCycle with WhenNotPaused modifier](https://github.com/code-423n4/2022-12-gogopool-findings/issues/823)
- M-02: [Coding logic of the contract upgrading renders upgrading contracts impractical](https://github.com/code-423n4/2022-12-gogopool-findings/issues/742)
- M-03: [NodeOp funds may be trapped by a invalid state transition](https://github.com/code-423n4/2022-12-gogopool-findings/issues/723)
- M-04: [requireNextActiveMultisig will always return the first enabled multisig which increases the probability of stuck minipools](https://github.com/code-423n4/2022-12-gogopool-findings/issues/702)
- M-05: [Bypass whenNotPaused modifier](https://github.com/code-423n4/2022-12-gogopool-findings/issues/673)
- M-06: [Inflation rate can be reduce by half at most if it get called every 1.99 interval.](https://github.com/code-423n4/2022-12-gogopool-findings/issues/648)
- M-07: [Rialto may not be able to cancel minipools created by contracts that cannot receive AVAX](https://github.com/code-423n4/2022-12-gogopool-findings/issues/623)
- M-08: [Recreated pools receive a wrong AVAX amount due to miscalculated compounded liquid staker amount](https://github.com/code-423n4/2022-12-gogopool-findings/issues/620)
- M-09: [State Transition: Minipools can be created using other operator's AVAX deposit via recreateMinipool](https://github.com/code-423n4/2022-12-gogopool-findings/issues/569)
- M-10: [Functions cancelMinipool() doesn't reset the value of the RewardsStartTime for user when user's minipoolcount is zero](https://github.com/code-423n4/2022-12-gogopool-findings/issues/555)
- M-11: [MultisigManager may not be able to add a valid Multisig](https://github.com/code-423n4/2022-12-gogopool-findings/issues/521)
- M-12: [Cancellation of minipool may skip MinipoolCancelMoratoriumSeconds checking if it was cancelled before](https://github.com/code-423n4/2022-12-gogopool-findings/issues/519)
- M-13: [slashing fails when node operator doesn't have enough staked GGP](https://github.com/code-423n4/2022-12-gogopool-findings/issues/494)
- M-14: [any duration can be passed by node operator](https://github.com/code-423n4/2022-12-gogopool-findings/issues/492)
- M-15: [wrong reward distribution between early and late depositors because of the late syncRewards() call in the cycle, syncReward() logic should be executed in each withdraw or deposits (without reverting)](https://github.com/code-423n4/2022-12-gogopool-findings/issues/478)
- M-16: [maxWithdraw() and maxRedeem() doesn't return correct value which can make other contracts fail while working with protocol](https://github.com/code-423n4/2022-12-gogopool-findings/issues/476)
- M-17: [NodeOp can get rewards even if there was an error in registering the node as a validator](https://github.com/code-423n4/2022-12-gogopool-findings/issues/471)
- M-18: [Users may not be able to redeem their shares due to underflow](https://github.com/code-423n4/2022-12-gogopool-findings/issues/317)
- M-19: [MinipoolManager: recordStakingError function does not decrease minipoolCount leading to too high GGP rewards for staker](https://github.com/code-423n4/2022-12-gogopool-findings/issues/235)
- M-20: [TokenggAVAX: maxDeposit and maxMint return wrong value when contract is paused](https://github.com/code-423n4/2022-12-gogopool-findings/issues/144)
- M-21: [Division by zero error can block RewardsPool#startRewardCycle if all multisig wallet are disabled.](https://github.com/code-423n4/2022-12-gogopool-findings/issues/143)
- M-22: [Inaccurate estimation of validation rewards from function ExpectedRewardAVA in MiniPoolManager.sol](https://github.com/code-423n4/2022-12-gogopool-findings/issues/122)

## Overview of changes

First of all, I don't know half of you half as well as I should like; and I like less than half of you half as well as you deserve.

With that in mind, thanks for all the great findings! Your hard work is much appreciated.

Without further ado, here's our biggest changes to look out for:

1. Minipool State Machine - We've tightened up the allowed state transitions including a new recreate minipool method that's atomic and doesn't allow node ops to withdraw funds or hijack a minipool.
2. Tracking AVAX High Water - Our previous system forced some tradeoffs to which AVAX is calculated in HighWater. We added a new variable `AVAXValidating` which tracks amount of AVAX actually validating on the P-Chain, and High Water is simply the highest validating amount during the period.
3. TokenGGP - Changed how tokens are inflated to actually mint rather than track tokens in the ProtocolDAO
4. Contract Upgrades - We're now able to upgrade as expected, to a contract with the same name as the existing contract
5. Upgradeable Tokens - ERC20Upgradeable takes a variable version for it's domain separator and we added storage gaps across the board

## Mitigations to be reviewed

| URL                                               | Mitigation of | Purpose                                                                       |
| ------------------------------------------------- | ------------- | ----------------------------------------------------------------------------- |
| https://github.com/multisig-labs/gogopool/pull/25 | H-01          | New variable to track validating avax                                         |
| Not fixing                                        | H-02          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/41 | H-03          | Base slash on validation period not full duration                             |
| https://github.com/multisig-labs/gogopool/pull/23 | H-04          | Atomically recreate minipool to not allow hijack                              |
| https://github.com/multisig-labs/gogopool/pull/49 | H-05          | Initialize ggAVAX with a deposit                                              |
| https://github.com/multisig-labs/gogopool/pull/41 | H-06          | If staked GGP doesn't cover slash amount, slash it all                        |
| https://github.com/multisig-labs/gogopool/pull/22 | M-01          | Pause startRewardsCycle when protocol is paused                               |
| https://github.com/multisig-labs/gogopool/pull/32 | M-02          | Fix upgrade to work when a contract has the same name                         |
| https://github.com/multisig-labs/gogopool/pull/20 | M-03          | Remove method that trapped Node Operator's funds                              |
| Not fixing                                        | M-04          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/22 | M-05          | Pause claimAndRestake as well                                                 |
| Not fixing                                        | M-06          | N/A                                                                           |
| Not fixing                                        | M-07          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/43 | M-08          | Use liquid staker avax amount instead of node op amount                       |
| https://github.com/multisig-labs/gogopool/pull/23 | M-09          | Atomically recreate minipool so a node operator can't withdraw inbetween      |
| https://github.com/multisig-labs/gogopool/pull/51 | M-10          | Reset rewards start time in cancel minipool                                   |
| Not fixing                                        | M-11          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/40 | M-12          | Base cancelMinipool delay on minipool creation time not rewards start time    |
| https://github.com/multisig-labs/gogopool/pull/41 | M-13          | If staked GGP doesn't cover slash amount, slash it all                        |
| https://github.com/multisig-labs/gogopool/pull/38 | M-14          | Added bounds for duration passed by Node Operator                             |
| not fixing in this version of the protocol        | M-15          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/50 | M-16          | ggAVAX max redeem incorrect, not fixing, but made test to illustrate.         |
| https://github.com/multisig-labs/gogopool/pull/28 | M-17          | Remove the state transition from Staking to Error.                            |
| not fixing in this version of the protocol        | M-18          | N/A                                                                           |
| https://github.com/multisig-labs/gogopool/pull/42 | M-19          | We removed minipool count entirely.                                           |
| https://github.com/multisig-labs/gogopool/pull/33 | M-20          | Return correct value from maxMint and maxDeposit when the contract is paused. |
| https://github.com/multisig-labs/gogopool/pull/37 | M-21          | Prevents division by zero error blocking startRewardCycle().                  |
| not fixing in this version of the protocol        | M-22          | N/A                                                                           |
