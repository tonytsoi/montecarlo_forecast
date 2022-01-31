# Application of Monte Carlo Simulation in Financial Forecasting 
Business management would often want to make predictions about the future performance of their businesses in terms of metrics such as revenues, costs and profits. The finance team of the firm would likely be tasked to construct financial models and present the results under several scenarios, for example the best scenario, the normal scenario and the worst scenario, by varying the underlying assumptions. The purpose of this exercise is to provide the management with a better overview of how much the business would gain or lose under different market environment.

Nonetheless, the drawback in modeling the prospects of a business this way is that we do not know how likely that a certain scenario would occur. In this article, I discuss the application of Monte Carlo Simulation which would address this issue and provide further insight on the likelihood that the business could achieve its desired result using Python.

# What is Monte Carlo Simulation?
Monte Carlo Simulations are usually used to model the probability of different outcomes that are not easily predictable due to the randomness in variables. The methods in conducting Monte Carlo Simulations vary significantly but they follow the patterns of generating inputs randomly from an assumed probability distribution, performing computation on the inputs and then aggregating the results. To put it simply, Monte Carlo Simulation is to run the model for at least thousands of times to obtain a series of results in which some are more likely to occur than others, then combine them to form an overview.

The application of Monte Carlo Simulation ranges across different disciplines from Physics to Finance. In the field of Finance, common applications include option pricing (Black Scholes model) and default risk analysis (Value at Risk, VaR).

A simple model for Monte Carlo Simulation would be the Unit Root/Random Walk model. The Random Walk model defines that the value in the current period depends on the value in the previous period plus a random noise that follows a normal distribution with a mean of zero and standard deviation of 1.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{t-1} %2B Z_t, S_0 = 0, Z_t ~ N(0,1)">

The chart below shows 10 simulations results of the Random Walk model with 10 time steps.

![random_walk](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/random_walk.png?raw=true)

A slightly more sophisticated model would be the Geometric Brownian Motion (GBM) model. The GBM model assumes that the future is independent of the past. If this model is applied in the context of asset pricing, it assumes that the past price information has already been incorporated into the current price and the price movement in the future is conditionally independent of any price movements in the past.

The below equation defines the GBM model.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{0}\, exp((\mu - \sigma^2/2)t - \sigma\times W_t)">

<img src="https://render.githubusercontent.com/render/math?math=\large W_t"> is the Brownian motion term, in which <img src="https://render.githubusercontent.com/render/math?math=\large W_t - W_{t-1} = sqrt(dt)Z_t"> and <img src="https://render.githubusercontent.com/render/math?math=\large Z_t"> is an independent standard normal variable.

<img src="https://render.githubusercontent.com/render/math?math=\large \mu"> is the drift rate which determines the changes (or growth) in the average value of the random process. <img src="https://render.githubusercontent.com/render/math?math=\large \sigma"> is the volatility of the drift rate.

The GBM model can also be written in an iterative form as the following.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{t-1}\, exp((\mu - \sigma^2/2)dt - \sigma \, sqrt(dt) Z_t">

The below chart shows 10 simulations of the GBM model with <img src="https://render.githubusercontent.com/render/math?math=\large S_0 = 1, \mu = 0.05, \sigma = 0.2">

![GBM](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/GBM.png?raw=true)

# Application in Business Forecasting
First, let’s start with a simple financial model which <img src="https://render.githubusercontent.com/render/math?math=\ Profit = Revenue - Fixed Cost - Variable Cost">. Say we assume in Year 0, revenue is at $10, fixed cost is at $2 and variable cost is at 10% of the revenue, and we further assume that revenue would grow at 2% per year for the next 10 years, we would obtain a deterministic path of profits for the next 10 years shown in the chart below.

![profit](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit.png?raw=true)

Now let’s introduce Monte Carlo Simulation into our financial model by assuming that revenue follows a GBM model with a growth rate of 2% and a volatility of 5%, and we run the model for 10,000 times. As you can see from the chart below, instead of just one prediction, we now have 10,000 predictions which all follow a different path.

![gross_profit_mcs](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_mcs.png?raw=true)

We can then summarize the results from the simulation by calculating a 95% interval that the profits would fall within, which is presented as the shaded area in the chart below.

![gross_profit_range](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_range.png?raw=true)

By incorporating Monte Carlo Simulation in financial forecasting, the business management would have a better gauge about the probability that the future profits would fall within a certain range, conditional on the initial assumptions of growth rate and volatility etc. The growth rate and volatility assumptions can be estimated using the historical data or the financial information of any comparable businesses, and can be adjusted if there is the expectation that the future growth rate would differ from the historical one.

We can also add more complexity to our model by introducing more randomness. Let’s assume that the variable cost margin follows a normal distribution with a mean of 10% and a standard deviation of 5%. As we can see from the charts below, introducing another random variable into the model would lead to the resulting profit prediction being more volatile.

![gross_profit_mcs2](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_mcs_2.png?raw=true)
![gross_profit_range2](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_range_2.png?raw=true)

As the financial model gets more complex, different inputs of the model can be modeled as a random variable. For example, if we are forecasting the profits of an airline company, oil price would be one of the main components in its variable costs which can be modeled using Monte Carlo Simulation, as it is highly volatile and unpredictable.

In addition, for companies that are heavily affected by commodity prices such as the oil price in the case of an airline company, we can incorporate the changes of the forward commodity prices as the drift rate in the GBM model, which in effect incorporate the market expectation into the model.

# Conclusion
By applying Monte Carlo Simulation in financial forecasting, it would provide a comprehensive view of the results of the business, and would be more insightful than the ordinary approach of presentation for the management to make more informed decisions.
