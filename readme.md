<h1>Project Proposal</h1>

By Sidra Nasir (18859261), Mitchell Spencer (19034205), Sean Gibbon (19770237), Matthew Johnston (19777775)<br />

<h3>Summary</h3>

In this project we will retrieve and use the raw data collected by the Bureau of Meteorology in order to construct our model and consequently predict the rainfall of Perth. In concurrence with Gabriel and Neumann 1962 (who created a statistical model modelling daily rainfall occurrence in Tel Aviv) we will also use the last 10 years of daily rainfall data, starting in 2009 through to 2019 (in the construction of our model). <br />

By going to: http://www.bom.gov.au/climate/data/index.shtml, we will be able to access this daily rainfall data from the Perth Metro weather station (009225). <br />

Because there will be a fair amount of days where there is no rainfall. Seasonality must also be considered as we will expect greater rainfall during winter and less during summer. The way to do this is to add a weight to a set of specific months to increase the probability of rainfall during winter and less during summer. <br />

A Markov Chain is a mathematical system that transits states from one to another, where any given state is dependent on the state directly before it; however, the transit can also end in the same state. In our simulation, we will specifically be using a two-state Markov Chain (our two states being dry and wet). In order to make the Markov Chain work, we will first need to specify both a dry day and rainy day. By classifying a ‘rainy day’ as one that has more than 1mm in rainfall, we can also consequently define a ‘dry day’. <br />

x < 1: x = dry <br />

x >= 1 : x = rainfall

Here, our Markov Chain has two nodes (or states), dry and rainy and can be used to define a transition matrix such:

According to Gabriel and Neumann 1962, “several authors have found wet and dry spells to have geometric distributions”. However, upon rudimentary levels of examination we have found the exponential distribution to fit relatively well. We would also be using the chi-squared distribution to check the goodness of fit of our model.




<h3>Methodology for the problem</h3>
The purpose of this weather generator is to simulate rainfall patterns as close to the real world as possible. In order to achieve this, we will need to simulate the transitions between the two states. This will be done using the two state Markov chain. We will first assign a value to each state with wet = 1 and dry = 0. Then after looping through the data as a vector of values, all values above 1mm will be assigned 1 while the rest will be assigned 0. Since there is a greater number of values larger than 1mm, it is technically possible that the result from the weather generator will output the same pattern (if every day of the year is either raining or dry); although this is highly unlikely. After computing the generated amount of rain per day and the sequences of wet and dry days separately, we will combine them to get our final results.<br />

To evaluate the weather generator, we are going to use a Wilcoxon signed-rank test to test the predicted rainfall quantities against the actual rainfall quantities. The main reason we have chosen to use this method of testing is because it allows us to conduct the test across all of the data points instead of just using a sample mean or smaller sample of the data. <br/>

At this stage, our presentation of results will be done primarily through the use of R plotting libraries (such as ggplot2 and or Plotly). These libraries facilitate the construction of graphs; thus enabling a quick and efficient way to visualise data. The graphs will be line, scatter plots and bar graphs for both wet and dry days. We will likely use one colour to represent the generated rainfall amount, and another other colour to represent the actual values. To visualise the wet and dry days, a histogram demonstrating Bernoulli trials will be utilised, having one colour representing actual data and another colour representing the generated data. <br/>

To make the simulation more like actual rainfall data, more factors need to be taken into consideration when creating the primary function of the generator. The first variable we will need to consider is the seasonality of the dataset. That is to say that during winter there will be more rainy days and therefore, we will need to assign a weighting during that period and take that into consideration in the generator (in order to increase the probability of wet days occurring and dry days occurring during summer). <br />

Another option we could consider is to add multiple markov chains to represent the transition states between monthly changes and yearly changes as opposed to just daily changes. These extra markov chains and their associated probabilities could then be used in our generator’s prediction function. This would ultimately make it more accurate since it would take into consideration what the weather had been like the previous month and / or the previous year. 



<h3>References</h3>
Gabriel, K.R. and Neumann, J. (1962), A Markov chain model for daily rainfall occurrence at Tel Aviv. Q.J.R. Meteorol. Soc., 88: 90-95. doi:10.1002/qj.49708837511. <br />
Miller, D. K. and Homan, S. M. (1994), Determining Transition Probabilities: Confusion and Suggestions. Medical Decision Making., 14: 52-58.<br />
Wilks, D. S and Wilby, R. L. (1999), The Weather generation game: a review of stochastic weather models. Progress in Physical Geography., 23: 329-357.<br />
Bureau of Meteorology. (2013). Climate Data Online. Australian Government Bureau of Meteorology. http://www.bom.gov.au/climate/data/index.shtml
