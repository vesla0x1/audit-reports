# [M-1] Malicious actors can accumulate a huge amount of internal points (FMP) and inflate their value

## Summary
Malicious actors can take advantage of the absence of a time restriction (or penalty) mechanism for withdrawing collateral to earn internal points (FMP) at a very low rate (only the 0.3% withdraw fee), inflating their value.

## Vulnerability Detail
A bad actor can deposit collateral, earning FMP points and withdraw all the collateral deposited instantly, paying only the small withdraw fee (0.3% - keeper fees can be avoided if the order is executed by the user). Once there is no time restriction to earn points or a penalty mechanism to reduce points when withdrawing collateral, the bad actor can repeat this process (almost) indefinitely (until all its collateral is spent paying the withdraw fee), accumulating FMP points and inflating their value.

## Impact
Malicious users can accumulate a huge amount of FMP, inflating their value.

## Code Snippet
https://github.com/sherlock-audit/2023-12-flatmoney/blob/main/flatcoin-v1/src/StableModule.sol#L82-L84

https://github.com/sherlock-audit/2023-12-flatmoney/blob/main/flatcoin-v1/src/PointsModule.sol#L77-L87

## Tool used
Foundry

## Recommendation
Implement a mechanism that restricts the FMP earnings by time and/or reduces the point quantity when a user withdraws collateral.