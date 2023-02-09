# Gogopool - Mitigation contest details
- Total Prize Pool: $32,000 USDC
- [Warden guidelines for C4 mitigation reviews](https://code4rena.notion.site/Guidelines-for-Versus-mitigation-reviews-ed10fc5cfbf640bd8dcec66f38b343c4)
- Submit findings [using the C4 form](https://code4rena.com/contests/YYYY-MM-sponsorName-mitigation-contest/submit)
- Starts February 10, 2023 20:00 UTC
- Ends February 17, 2023 20:00 UTC

## Important note 

Each warden must submit a mitigation review for *every High and Medium finding* from the parent contest. **Incomplete mitigation reviews will not be eligible for awards.**

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

[ ⭐️ SPONSORS TODO ]

Please provide context about the mitigations that were applied if applicable and identify any areas of specific concern.

## Mitigations to be reviewed

[ ⭐️ SPONSORS TODO ]

Wherever possible, mitigations should be provided in separate pull requests, one per issue. If that is not possible (e.g. because several audit findings stem from the same core problem), then please link the PR to all relevant issues in your findings repo. 

| URL | Mitigation of | Purpose | 
| ----------- | ------------- | ----------- |
| https://github.com/code4rena/sample-contracts/pull/XXX | H-01 | This mitigation does XYZ | 

