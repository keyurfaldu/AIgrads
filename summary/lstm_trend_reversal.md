
## A new LSTM based reversal point prediction method using upward/downward reversal point feature sets. 
### JuHyok, U., Lu, P., Kim, C., Ryu, U., & Pak, K. (2020). 
### Chaos, Solitons & Fractals, 132, 109559.


**Key Points**
* Novel LSTM model for predicting trend reversal points for both upward and downward trends.
* It used 27 feature sets combiing both candlestick and technical parameters, and the best feature set was selected based on the performance.
* Candlestick indicators like Body, topTail, bottomTail, Whole etc were used, and following technical parameters were used
    * MACD - Moving Average Convergence and Divergence
    * Rate of Change (ROC)
    * Stochastic Oscillator - momentum indicator that reflects the current price in the of historical price range.
    * Commodity channel index - strength and direction of the price trend by the difference between recent price and moving average of price.
    * Relative strength index ( RSI )
    * Volume Ratio - ratio of trading volume in assending days to descending days.
    * Psychological line - ratio of days of ascending in stock price vs total days in a certain period of time.
    * Volumen moving average 
    * AB ratio - ratio determining trend is bullish or bearish
* Trend reversal point is computed as the contineous increase in MA over last n days, and the close price now has difference greater than threshold over min/max of future MA in next a days. 
    * If someone is a weekly trader with 5% as the significant profit, a = 5 days, theta = 0.05.
* LSTM model was compared with CNN, SVM, MLP, etc and turned out better.
