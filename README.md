# Application of Monte Carlo Simulation in Financial Forecasting 
Business management would often make predictions about the future development of their businesses, in terms of metrics such as revenues, costs and profits. The finance team of the firm would likely construct certain financial models and present several scenarios, for example the best scenario, the normal scenario and the worst scenario, with different underlying assumptions. This is to provide the management with a better overview of how much the business would gain or lose under different market environment.

Nonetheless, there is a drawback in modeling the prospects of a business this way. is that we do not know how likely that a certain scenario would occur. 
In this article, I would discuss the application of Monte Carlo Simulation which would address this issue and provide further insight on how likely the business could achieve a certain level of result using Python.

# What is Monte Carlo Simulation?
Monte Carlo Simulations are usually used to model the probability of different outcomes that are not easily predictable due to the randomness in variables. The methods in conducting Monte Carlo Simulations vary significantly but they follow the patterns of generating inputs randomly from an assumed probability distribution, performing computation on the inputs and then aggregating the results. To put it simply, Monte Carlo Simulation is to run the model for thousands of times to obtain a series of results that some are more likely than others.

The application of Monte Carlo Simulation ranges across different disciplines from Physics to Finance. In the field of Finance, common applications include option pricing (Black Scholes model) and default risk analysis (Value at Risk, VaR).

A simple example of Monte Carlo Simulation would be the Unit Root/Random Walk model. The Random Walk model states that the value in the current period depends on the value in the previous period plus a random noise that follows a normal distribution.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{t-1} %2B Z_t, S_0 = 0, Z_t ~ N(0,1)">

The below chart shows 10 simulations of the Random Walk model with 10 time steps.

![random_walk](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/random_walk.png?raw=true)

A slightly more sophisticated model would be the Geometric Brownian Motion (GBM) model. The GBM model assumes that the future is independent of the past. If this model is applied in the context of asset pricing, it assumes that the past price information has already been incorporated into the current price and the price movement in the future is conditionally independent of any price movements in the past. 

The below equation defines the GBM model.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{0}\, exp((\mu - \sigma^2/2)t - \sigma\times W_t)">

<img src="https://render.githubusercontent.com/render/math?math=\large W_t"> is the Brownian motion term, in which <img src="https://render.githubusercontent.com/render/math?math=\large W_t - W_{t-1} = sqrt(dt)Z_t"> and <img src="https://render.githubusercontent.com/render/math?math=\large Z_t"> is an independent standard normal variable.

<img src="https://render.githubusercontent.com/render/math?math=\large \mu"> is the drift rate which determines the changes (or growth) in the average value of the random process. <img src="https://render.githubusercontent.com/render/math?math=\large \sigma"> is the volatility of the drift rate.

The GBM model can also be written in an iterative form.

<img src="https://render.githubusercontent.com/render/math?math=\Large S_t = S_{t-1}\, exp((\mu - \sigma^2/2)dt - \sigma \, sqrt(dt) Z_t">

The below chart shows 10 simulations of the GBM model with <img src="https://render.githubusercontent.com/render/math?math=\large S_0 = 1, \mu = 0.05, \sigma = 0.2">

![GBM](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/GBM.png?raw=true)

# Application in Business Forecasting
First, let’s start with a simple financial model which <img src="https://render.githubusercontent.com/render/math?math=\ Profit = Revenue - Fixed Cost - Variable Cost">. If we assume in Year 0, revenue is at $10, fixed cost is at $2 and variable cost is at 10% of the revenue, and we further assume that revenue would at 2% per year for the next 10 years, we would arrive a deterministic path of profits for the next 10 years shown in the below chart.

![profit](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit.png?raw=true)

Now let’s introduce Monte Carlo Simulation into our financial model by assuming that revenue follows a GBM model with a growth rate of 2% and a volatility of 5%, and we run the model for 10,000 times. As you can see from the chart below, instead of just one prediction, we have 10,000 predictions which all follow a different path.

![gross_profit_mcs](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_mcs.png?raw=true)

We can then aggregate the results from the simulation and calculate a 95% interval that the profits would fall within.

![gross_profit_range](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_range.png?raw=true)

By incorporating Monte Carlo Simulation in financial forecasting, the business management would have a better gauge about the likely range that the future profits would fall into, conditional on the initial assumptions of growth rate and volatility. The growth rate and volatility assumptions can be the historical data or the figures of any comparable businesses, and can be adjusted if it is expected that the future growth rates would differ from the historical ones.

We can also add more complexity to our model by introducing more randomness. Let’s assume that the variable cost margin follows a normal distribution with a mean of 10% and a standard deviation of 5%. As we can see from the charts, introducing more randomness into the model would lead to the profit prediction being more volatile.

![gross_profit_mcs2](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_mcs_2.png?raw=true)
![gross_profit_range2](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/gross_profit_range_2.png?raw=true)

As the financial model gets more complex, the randomness can be introduced in different inputs of the model. For example, if we are forecasting the profits of an airline company, oil price would be one of the main inputs in its variable costs which can be modeled using Monte Carlo Simulation.

On a further note, for companies that heavily depend on the commodity prices such as oil prices in the case of an airline company, we can incorporate the changes of the forward commodity prices as an estimate into the GBM model.

# Conclusion
By incorporating Monte Carlo Simulation in financial forecasting, it would provide a wider picture of the likely results of the businesses, and would be more insightful than the ordinary approach of presentation for the management to make more informed decision.
