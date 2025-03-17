# RSI-Momentum-for-Mag7
backtest RSI and Momentum strategies for Magnificent 7


## RSI Signal Logic Interpretation
1. check for buy and sell signal
* buy if rsi < 25 and the stock is not already in the portfolio
* sell if rsi > 75
  
2. if at least one buy or sell signal exists, proceed with the following steps

2.1 rebalance portfolio if any stock exceeds 30% of total portfolio value
* exclude stocks that have a sell signal since they will be sold in the next step
* for remaining stocks, if any position exceeds 30% of aum, sell the excess until it is within the limit

3. execute sell orders
* sell all shares of any stock that has an rsi > 75
* add the proceeds to cash

4. execute buy orders
* if there is enough cash, buy stocks in the buy signal list so that their value matches existing stocks in the portfolio (to avoid buying existing stockswithout buy signal)
* if cash is insufficient:
  * calculate the target allocation per stock using k = total portfolio value / number of stocks (existing + new buys)
  * if k > 30% of aum, set k = 30% of total portfolio value
  * sell portions of existing stocks to balance the portfolio and generate enough cash
* buy new stocks at value k

5. apply risk-free interest on cash holdings
update cash balance using cash = cash * (1 + 2% / 252) to account for daily interest earnings
