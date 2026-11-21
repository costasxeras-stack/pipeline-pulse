# 0002: Forecast with stage weights the user can change

**Status:** accepted, 0.1.0

## Context

Teams forecast in different ways: rep calls, stage weights, or models trained on history. Models need more history than one export usually has.

## Decision

Forecast = won this quarter + open deals closing this quarter × the weight of their stage. Weights start as a sensible ladder and can be edited. The page also shows the best case, every open deal closing, so the user can see the range.

## Tradeoff

- Anyone can explain the number in one sentence.
- Weights are a guess until the team checks them against its own win rates by stage.
- Deals without a close date are left out of the quarter, which the Pipeline tab makes visible.
