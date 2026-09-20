# variational-swaps-perps

Delta-neutral funding arbitrage between the XAU swap and the XAU perp on Variational Omni.

| Leg  | Market | Link |
|------|--------|------|
| Long | XAUS (Swap) | https://omni.variational.io/swap/XAUS |
| Short | XAU (Perp) | https://omni.variational.io/perpetual/XAU |

---

## How funding works

### Swap: based on interest rates

Swap funding depends on interest rates, not on how traders are positioned.

**Example: EUR/USD**

| Position | What you're doing | You receive funding when | You pay funding when |
|----------|-------------------|--------------------------|----------------------|
| Long  | Borrow USD to hold EUR | EUR rate > USD rate | USD rate > EUR rate |
| Short | Borrow EUR to hold USD | USD rate > EUR rate | EUR rate > USD rate |

### Perp: based on the crowd

Perp funding can be positive or negative, depending on where the perp price sits relative to the spot price.

| Funding | Perp price | Why | Who pays | Effect |
|---------|------------|-----|----------|--------|
| Positive | Above spot | Too many longs | Longs pay shorts | Pushes price down |
| Negative | Below spot | Too many shorts | Shorts pay longs | Pushes price up |

---

## Why the arbitrage exists

The swap and the perp give the same price exposure but charge for it differently:

- **Swap:** follows interest rates, so it's fixed and predictable.
- **Perp:** follows the crowd, so it's variable.

Nothing forces the two costs to be equal, so a gap can open between them.

---

## The trade

**Long the swap + short the perp.**

Price moves cancel out. What's left is the funding difference: you pay the fixed swap rate and receive the perp funding.

```
Profit = perp funding − swap funding − trading costs
```

---

## Backtest result

- XAU perp funding stayed positive throughout the backtest period.
- Both legs were compared on the same annualized basis. The perp settles every 4 hours; the swap charges daily.
- Estimated net return: **~10% APR**.

---

## Notes

- **Past results aren't guaranteed.** Perp funding can turn negative. Exit if the spread stops covering the swap rate.
- **Wednesday triple charge.** The swap charges triple funding on Wednesday to cover the weekend, even if the position is closed before the weekend.
- **Short swap history.** Swaps launched September 1, 2026, so the swap rate is based on limited data.
