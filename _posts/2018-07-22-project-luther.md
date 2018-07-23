---
layout: post
title:

#### How much for the 'Dank Nuggs'?

![Subway Map](https://s.yimg.com/ny/api/res/1.2/ap6JwY3b8T_rTAULKBDg_A--~A/YXBwaWQ9aGlnaGxhbmRlcjtzbT0xO3c9ODAw/http://media.zenfs.com/en-US/homerun/motleyfool.com/04ad9cc31e2124e506c466d4439cbcda "NYC Subway System")

I just finished my third week at Metis in San Francisco. We spent most of the last two weeks learning about linear regression and web-scraping. For our second project I leveraged all of the tools I learned to help build a tool to predict flower cannabis prices at dispensaries. In this article, I will walk you through my approach to framing the problem, designing the data pipeline, and ultimately implementing the analysis. You can find the project on GitHub, along with links to all the data.

### The Problem

I was interested in investigating data from marijuana dispensary menus to try and build a model that can predict the price of cannabis flowers based on a set of features.

### The Approach

I scraped dispensary menus from weedmaps.com. I was able to write helper functions that allowed me to input a list of city names and then output an aggregated data set that contained information from the dispensary menus in those cities.

![Menu]({{ site.url }}/public/luther/menu.png)

The data set included information like the cost of the cannabis flower, its THC content, its strain name, the type of flower (Indica, Sativa, or Hybrid), and lots of of information related to the dispensary.

### The Analysis

I reviewed the available data to identify some reasonable a priori model specifications and ultimately settled on the following three:

 ![Equation]({{ site.url }}/public/luther/equation1.png)

 ![Equation]({{ site.url }}/public/luther/equation1.png)

 ![Equation]({{ site.url }}/public/luther/equation1.png)

Each of these specifications were then fed into a function that scored (R^2) all of the specifications for all of the available supervised machine learning algorithms I had available.

![Scores]({{ site.url }}/public/luther/results.png)

As you can see in the table above, specification 3 employing a Random Forest Regression model had the highest score. After running the same model on the test data, the score was only slightly lower indicating that over-fitting is not a huge issue.

The table below illustrates the predicted prices vs. the actual prices and it is clear that the model is not particularly accurate.

![Predict vs. Actual]({{ site.url }}/public/luther/predict.png)

The model is overpredicting prices below $8/gram and underpredicting prices greater than $8/gram. This is likely due to the way in which I processed the pricing variable as it does not take into account quantity discounts.


### Next Steps

While this project was a great exercise in learning how to scrape websites and employ supervised machine learning algorithms it is clear that the current model has a long way to go. I believe the models are omitting some critical features that determine prices at dispensaries. Namely, the smell ('nose') and aesthetics of the flowers. I don't know that I will be easy to find measurements of these features, however, maybe there are some computer visualization tools that will help.

Since a Random Forest Regression model was the most accurate predictor of the portfolio of models I tested, I would also like to spend some time tuning the hyperparameters of the model.
