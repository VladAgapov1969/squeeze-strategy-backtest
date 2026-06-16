# Squeeze Strategy - Walk-Forward Validation Results

## Strategy Overview

A mean-reversion trading strategy that identifies low-volatility "squeeze" periods using channel width and ATR percentiles. The strategy enters both long and short positions at the channel middle during squeeze periods, exits at channel bounds, and re-enters on pullbacks to the middle or opposite bound.

### Trading Rules

| Aspect | Rule |
|--------|------|
| **Entry** | Enter both Long and Short at channel middle during squeeze |
| **Exit** | Long exits at upper bound, Short exits at lower bound |
| **Re-entry** | After exit, re-enter when price returns to middle or opposite bound |
| **Broker** | Fusion Brokerage with 0.6 pip round trip cost cap |
| **Trading Hours** | Quiet hours (22-23, 0-1, 4-5 GMT) |

---

## Walk-Forward Validation Results (4 Months)

**Test Period:** February 2, 2020 – May 27, 2020 (102 trading days)

**Methodology:** Rolling 20-day In-Sample (IS) optimization with 10-day Out-of-Sample (OOS) tests, stepped forward by 10-day increments (8 cycles total).

### Aggregated OOS Performance (All Cycles Combined)

| Metric | Value |
|--------|-------|
| **Total OOS Trades** | 179 |
| **Total OOS Net PnL** | 295.80 pips ($2,958 for 1 lot) |
| **OOS Win Rate** | 68.2% |
| **OOS Profit Factor** | 7.06 |
| **OOS Sharpe Ratio (annualized)** | **8.24** |
| **Profitable OOS Cycles** | 8/8 (100.0%) |

### Performance by Lot Size (Aggregated OOS)

| Lot Size | Net PnL (USD) | Sharpe Ratio |
|----------|---------------|--------------|
| 1 | $2,958 | 8.24 |
| 2 | $5,916 | 8.24 |
| 3 | $8,874 | 8.24 |
| 4 | $11,832 | 8.24 |
| 5 | $14,790 | 8.24 |

> Note: Sharpe ratio is consistent across lot sizes as it measures risk-adjusted returns per unit.

---

## Cycle-by-Cycle Breakdown

| Cycle | IS Period | OOS Period | IS Sharpe | IS Trades | OOS Trades | OOS PnL (pips) | OOS Sharpe |
|-------|-----------|------------|-----------|-----------|------------|----------------|------------|
| 1 | 2020-02-02 → 2020-02-24 | 2020-02-25 → 2020-03-06 | 10.70 | 35 | 18 | 15.50 | 10.23 |
| 2 | 2020-02-13 → 2020-03-06 | 2020-03-08 → 2020-03-18 | 11.87 | 50 | 33 | 91.80 | 14.45 |
| 3 | 2020-02-25 → 2020-03-18 | 2020-03-19 → 2020-03-30 | 14.49 | 40 | 22 | 58.60 | 14.07 |
| 4 | 2020-03-08 → 2020-03-30 | 2020-03-31 → 2020-04-10 | 17.44 | 44 | 16 | 10.40 | 3.76 |
| 5 | 2020-03-19 → 2020-04-10 | 2020-04-12 → 2020-04-22 | 10.31 | 42 | 19 | 35.60 | 10.55 |
| 6 | 2020-03-31 → 2020-04-22 | 2020-04-23 → 2020-05-04 | 9.87 | 55 | 26 | 30.30 | 10.41 |
| 7 | 2020-04-12 → 2020-05-04 | 2020-05-05 → 2020-05-15 | 13.00 | 47 | 25 | 37.30 | 19.07 |
| 8 | 2020-04-23 → 2020-05-15 | 2020-05-17 → 2020-05-27 | 16.83 | 43 | 20 | 16.30 | 10.87 |

**Cycle OOS Sharpe Statistics:**
- Average OOS Sharpe per cycle: **11.68**
- Median OOS Sharpe per cycle: **10.71**
- Sharpe Std Deviation: 4.13

---

## Parameter Stability

Parameters remained highly consistent across all 8 optimization cycles:

| Parameter | Most Common Value | Range |
|-----------|-------------------|-------|
| Channel Period | 20 | 20 (100% of cycles) |
| Squeeze Periods | [12, 18, 24] or [10, 15, 20] | 2 variations |
| Width Percentile | 0.25 or 0.30 | 0.25–0.30 |
| ATR Percentile | 0.25 or 0.30 | 0.25–0.30 |
| Exit Tolerance | 0.03 | 0.03 (100% of cycles) |

---

## Equity Curve

![Walk-Forward Equity Curve](results/walk_forward_equity_curve.png)

*Aggregated OOS equity curve showing consistent upward progression across all trading cycles.*

---

## Key Findings

1. **Robust Performance Across Market Regimes:** The strategy delivered positive returns in all 8 OOS periods, covering volatile COVID-19 market conditions (March-April 2020) and calmer periods.

2. **Strong Risk-Adjusted Returns:** Aggregated Sharpe ratio of 8.24 significantly exceeds institutional thresholds, indicating exceptional risk-adjusted performance.

3. **Parameter Stability:** Optimal parameters remained consistent across cycles (channel period = 20, exit tolerance = 0.03), suggesting the strategy is not overfit to specific market conditions.

4. **High Win Rate:** 68.2% win rate across 179 trades demonstrates consistent edge.

5. **Profit Factor:** 7.06 profit factor indicates robust reward-to-risk ratio.

6. **Re-entry Logic Validation:** The re-entry mechanism successfully generated additional trades after exits, increasing total trade count and overall PnL.

---

## Comparison: Original vs. Walk-Forward Results

| Metric | Original (27 days) | Walk-Forward (102 days) |
|--------|-------------------|------------------------|
| Test Period | 27 days | 102 days |
| Total Trades | 20 | 179 |
| Total PnL (1 lot) | $274 | $2,958 |
| Win Rate | 70% | 68.2% |
| Sharpe Ratio | Not meaningful | 8.24 |
| Sample Size | Limited | Substantial |

---

## Limitations & Considerations

- **Single Instrument:** Tested only on GBPUSD (original) and AUDUSD (walk-forward)
- **Specific Trading Hours:** Strategy relies on quiet hours liquidity patterns
- **No Slippage Modeling:** Results assume ideal fills at tick prices
- **Spread Costs:** Realistic spread modeling included, but extreme volatility slippage not accounted for
- **COVID-19 Period:** Testing includes extreme volatility of March 2020; performance may differ in other regimes
- **Not Statistically Validated:** While results are strong, live trading requires further validation

---

## Next Steps for Research

- [ ] Test on EURUSD, USDJPY, and other major pairs
- [ ] Extend test period to 5+ years
- [ ] Add position sizing optimization (Kelly, optimal f)
- [ ] Implement stop-loss mechanisms for tail risk management
- [ ] Stress-test under various market conditions
- [ ] Implement transaction cost sensitivity analysis
- [ ] Develop risk management framework

---

## File Structure
squeeze-strategy-backtest/
├── README.md # This file
├── results/
│ ├── walk_forward_equity_curve.png # Aggregated OOS equity curve
│ ├── walk_forward_cycle_summary.csv # Cycle-by-cycle summary
│ ├── walk_forward_all_oos_trades.csv # All 179 OOS trades
│ └── walk_forward_aggregated_results.csv # Summary metrics
└── LICENSE # MIT License


---

## Data Source

- **Instrument:** AUDUSD
- **Period:** February 2, 2020 – May 27, 2020 (102 days)
- **Data Type:** Tick data (Bid/Ask)
- **Source:** Historical tick data (4 monthly files)

---

## How to Use These Results

1. Review the trade logs in the `results/` folder
2. Examine equity curves for performance visualization
3. **Important:** Results are for educational purposes only
4. **Not trading advice** - validate on larger datasets before considering live trading

---

## Disclaimer

⚠️ **FOR EDUCATIONAL PURPOSES ONLY**

This is a backtest of a trading strategy on historical data. Past performance does not guarantee future results. This is not financial advice. Always conduct your own research and consult with a qualified financial advisor before making investment decisions.

---

## License

MIT License - See LICENSE file for details

For questions or collaboration, please open an issue on GitHub.
