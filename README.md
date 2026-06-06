# Squeeze Strategy Backtest Results

## Strategy Overview

A mean-reversion trading strategy that identifies low-volatility "squeeze" periods using channel width and ATR percentiles.

### Trading Rules

| Aspect | Rule |
|--------|------|
| **Entry** | Enter both Long and Short at channel middle during squeeze |
| **Exit** | Long exits at upper bound, Short exits at lower bound |
| **Re-entry** | After exit, re-enter when price returns to middle or opposite bound |
| **Broker** | Fusion Brokerage with 0.6 pip round trip cost cap |
| **Trading Hours** | Quiet hours (22-23, 0-1, 4-5 GMT) |

## Performance Summary

### IS Period (2021-05-16 to 2021-06-03) - 17 days

| Metric | Value |
|--------|-------|
| **Total Trades** | 10 (7 Long, 3 Short) |
| **Win Rate** | 70% |
| **Gross PnL** | 15.90 pips |
| **Rebate Received** | 1.10 pips |
| **Net PnL** | **17.00 pips ($170 for 1 lot)** |

### OOS Period (2021-06-04 to 2021-06-15) - 10 days

| Metric | Value |
|--------|-------|
| **Total Trades** | 10 (4 Long, 6 Short) |
| **Win Rate** | 70% |
| **Gross PnL** | 7.90 pips |
| **Rebate Received** | 2.50 pips |
| **Net PnL** | **10.40 pips ($104 for 1 lot)** |

### Performance by Lot Size (OOS Period)

| Lot Size | Net PnL (USD) | Max Drawdown | Sharpe Ratio* |
|----------|---------------|--------------|---------------|
| 1 | $104 | - | - |
| 2 | $208 | - | - |
| 3 | $312 | - | - |
| 4 | $416 | - | - |
| 5 | $520 | - | - |

> *Sharpe ratio not statistically meaningful with only 10 trades

## Equity Curves

![Equity Curves](results/equity_curves.png)

## Key Findings

1. **Re-entry Logic Works**: Successfully generated additional trades after exits
2. **Cost Advantage**: 0.6 pip cap provided rebates when spreads exceeded threshold
3. **Consistent Performance**: 70% win rate across both periods
4. **Limited Sample**: Only 17 days IS, 10 days OOS - requires longer validation

## Limitations

- Small sample size (10 trades per period)
- Tested only on GBPUSD during specific quiet hours
- No slippage modeling beyond spread costs
- Not statistically validated for live trading

## File Structure

squeeze-strategy-backtest/
├── README.md # This file
├── results/
│ ├── equity_curves.png # IS and OOS equity curves
│ ├── is_trades.csv # IS period trade log
│ └── oos_trades.csv # OOS period trade log
└── LICENSE # MIT License


## Data Source

- **Instrument**: GBPUSD
- **Period**: May 16, 2021 - June 15, 2021 (27 days)
- **Data Type**: Tick data (Bid/Ask)
- **Source**: Historical tick data

## How to Use These Results

1. Review the trade logs in `results/` folder
2. Examine equity curves for performance visualization
3. **Important**: Results are for educational purposes only
4. **Not trading advice** - validate on larger datasets before considering live trading

## Next Steps for Research

- [ ] Test on larger dataset (multiple years)
- [ ] Validate on other currency pairs (EURUSD, USDJPY)
- [ ] Add position sizing optimization
- [ ] Implement stop-loss mechanisms
- [ ] Calculate statistically significant Sharpe ratios

## Disclaimer

⚠️ **FOR EDUCATIONAL PURPOSES ONLY**

This is a backtest of a trading strategy on historical data. Past performance does not guarantee future results. This is not financial advice. Always conduct your own research and consult with a qualified financial advisor before making investment decisions.

## License

MIT License - See LICENSE file for details

## Contact

For questions or collaboration, please open an issue on GitHub.
