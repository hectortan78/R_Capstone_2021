# R_capstone 
Observing Interplay Between Cryptocurrencies Trading Activity, Market Sentiments, and US Fiscal Stimulus

- To discern if the volume of cryptocurrency trading activity is directly or indirectly affected by social media buzz and influencers
- Scraped gTrends, Yahoo, Reddit, Twitter

# Code and Resources Used
R Studio Version: Version 1.4.1103

Packages: tidyverse, quantmod, rtweet, gtrendsR, lubridate, psych, jtools, RedditExtractoR, rvest, broom, gvlma, ggfortify, tidytext, ggstatsplot, reshape2, interactions, equatiomatic, sandwich, textdata


## Problem Statement

#Background 

Cryptocurrency (cryptos) was first conceptualised in 2008 with the advent of blockchain. Industry pundits touted the first cryptocurrency, bitcoin, as the future of money. Despite the numerous research and white papers around bitcoin as a gamechanger, interest in cryptos remained lukewarm in the years that followed. Bitcoin is notorious for its volatility. Prices rose to a high of USD18,0000 per coin in 2018, and very quickly fell to an adjusted price of USD3,400. Average price of bitcoin subsequently hovered at an average of around USD7,500 for the most part of 2018 to 2019. 

Fast forward to the start of 2020, and the prices for bitcoin began to rise in earnest. The price for a bitcoin averaged at USD8,300 in Jan 2020. By Dec 2020, this figure had risen to a whopping average of USD20,000. The perceived value of bitcoin was exacerbated by the COVID19 virus which began its rampage across the world with market lockdowns and social distancing restrictions, further encouraging positive sentiments for digital transactions and technology that enabled contactless forms of interactions between humans.

At around the same time, the US Federal reserve announced a Covid-19 stimulus and relief package, sometime during Mar 2020. This package involved the printing of trillions of USD which is believed to have resulted in the gradual decline of the USD Index. The US Federal Reserve has been tasked by the US government to find out if there is a possible relation between these events, i.e. the decreasing value of USDX which subsequently led to the rise in trading activity, or interest, for cryptocurrency.

#Narrative

This is an area of concern as exuberant cashflows  into crypto currency would diminish the Federal Reserve’s ability to regulate the economy.  Hence, the US Federal Reserve tasked The Firm to look into this issue. 

At quick glance of the dating sequence of events, The Firm hypothesized that the fall in USD Index may have indeed resulted in an increased interest in cryptos trading as the USD value’s decline seemed to coincide with the increase in cryptos trading activity. It is also logical to believe that market sentiment or general knowledge of cryptos had a correlation with its trading activity. The Firm decided to approach the matter by studying these two phenomena and how they interplay with crypto trading: 

  - Market sentiments - this is defined by user generated interest as well as word-of-mouth conversations         around cryptocurrency. 
          + User search queries in search engines i.e. gTrends data
          + Social hype caused by word-of-mouth due to the media news and influential individuals i.e. Twitter             data
          + Talks and sentiments in forums i.e. Reddit

  - Value of the US Dollar - this will be measured and defined according to the USD Index (USDX), which is a      measurement of the dollar's value relative to six foreign currencies as measured by their exchange rates.

  - Cryptocurrency trading activity - this will be the trading volume of the top 5 crypto-currencies by market     capitalization: BTC, ETH, BNB, ADA, and XRP. USDT, although having a larger market cap than some of the        listed cryptos, is a stable coin and is likely to behave differently. For this fact, we excluded it at the     onset.

Time period of analysis: 23 months, July 2019 - May 2021. 

The Firm chose a 23-month time period as July 2019 is the earliest time period where The Firm could get a full set of data extracted from Twitter regarding influential individuals. 

During the course of the data mining and analysis, The Firm discovered/faced some constraints to the data available, which contributed to a lack of data points for a robust analysis. This will be elaborated further below.


## Data sets that were obtained:

  1. Data on Crypto Trading
  
  Data on the top 5 cryptos were pulled from Yahoo Finance using the quantmod package. Looking at the data pulled, we found that volume traded for BTC and ETH were significantly higher than BNB, ADA, and XRP. Hence, we focused only on BTC and ETH. 
  
  2. Data on the Value of USD
  
  The USD index represents the strength of USD by valuing it against a basket of other foreign currencies. This data was also pulled using the quantmod package. 
  
  3. Twitter Timelines of Conventional Influencers, Crypto Influencers and Traditional News Outlets. 
  
  The idea was to look at how these parties influenced cryptos. We wanted to use the rtweets package to pull the timelines of the top 5 notable twitter handles that fell into the categories of (i) conventional influencers in the crypto space.  We term this group fo people as "Conventional Influencers"
  This was based off articles published on these two information sources:-
  - London post 
  www.london-post.co.uk/the-top-3-crypto-influencers-who-make-new-waves-and-trends-in-the-market/
  - Bloomberg 
  www.bloomberg.com/news/articles/2021-05-19/what-elon-musk-cathie-wood-mike-novogratz-say-about-bitcoin-btc-collapse
  
  Next, people in the crypto space that have grown to become influencers, and this based off their total social following (twitter + instagram + youtube + tiktok). We term this group fo people as "Crypto Influencers"
  The information source was based on:-
  - CityAM
  www.cityam.com/worlds-biggest-crypto-influencers-revealed-with-a-surprise-at-number-one/
  
  Lastly, news outlets, which was also based off the total monthly visits by users to their respective websites. 
   We term this as "News Outlets". This was based off information from:-
   - Press Gazette
   pressgazette.co.uk/top-50-largest-news-websites-in-the-world-right-wing-outlets-see-biggest-growth/
  
  However, due to the restriction by twitter to only allow the last 3200 tweets, we faced issues with the timeline coverage. In what will be shown below (row 153 to 164, and row 218 to 251), many of the twitter handles of crpyto influencers and traditional news outlets output a lot of tweets and such that their 3200th tweet does not reach back to our intended start period of Jan 2020. Hence, we will only focus on using data from the list of conventional influencers, less elon musk, where we also faced the same issues in getting comprehensive tweet data.
  
  4. Gtrends 

  Using gTrends package, we extracted queries on crypotcurrency primarily using four keywords that represented queries, or user search interest, in bitcoin and ethereum:-
- Bitcoin keywords: "btc", "bitcoin" 
- Ethereum keywords: "eth","ethereum"

We then ran a quick visualization to get a sensing of the data. 

  5. Reddit
  
  We believed that the activity or chatter on reddit may be well correlated with the volume of cryto traded as these individuals may frequent both trading platform and forum. To retrieve data from reddit, we attempted two methods: (i) Using the reddit API, RedditExtractoR and (ii) web-scraping of reddit directly. 
  
  We had some success with the reddit API. Although we are able pull relevant threads using the reddit_urls function, subsequently pull the comments using reddit_content function, and do a sentiment analysis on the comments, we faced a similar issue as with twitter. There seemed to be a limit on the number of urls that can be pulled using the reddit_urls function, being only able to pull 249 observations. This data set would then only stretch back to Apr 2021.
  
  We then sought to do a web scraping of reddit. We identified a thread on the "CryptoCurrency" subreddit, called "Daily Discussion" which is posted daily and has a high number of comments. Here is an example of the url "https://www.reddit.com/r/CryptoCurrency/comments/ol553c/daily_discussion_july_16_2021_gmt0/". On the surface, it seemed that it would be a good candidate since we can create a staging table and loop through the month, day, and year. However, there is a random string of alphanumeric characters within "...comments/XXXXX/daily_discussion..." which prevented this. Hence, the reddit dataset was also dropped. 

## Quick visualization - Crypto and USDX
Quick look at cryptocurreny trading volume and value of USD
![quickvisualization_crypto_usdx](https://user-images.githubusercontent.com/41586829/197400878-2a7a30e6-4ab2-458d-bce1-e1217b339baa.png)

Quick look at the tweet volumes of cryptocurrency influencers

![quickvisualization_cryptoinfluencertweets](https://user-images.githubusercontent.com/41586829/197401058-4c335587-8a62-43c4-8dbc-7af4be9d53f0.png)

## Tidy & Transform

Tidied the shortlisted three data sets. Largely, tidying the data by grouped them by months and filtered for Jan 20 to May 21. Individual data sets for BTC and ETH were also combined.

For the twitter data sets. This was where we realized some of its additional deficiencies, such a few mentions of our key words, “bitcoin, btc, ethereum, eth” and that the tweets don’t go back far enough.


## Visualization
Running a general visualization, we can see that there seems to be a possible positive relationship between the rising sentiment activity in tweets, web searches and youtube searches on the trading activity of crypto. The rising price of gold, and weakening of the USD and RMB values seem to go hand in hand with the increased trading interest in crypto.

We combined all the variables into one dataset and normalized the values for consistency.
![visualization_cryptotrading_and_ tweets, web searches and youtube](https://user-images.githubusercontent.com/41586829/197401255-480ecc58-bd1c-4513-83bf-85be5fca8b16.png)

![visualization_cryptotrading_and_usdtrading](https://user-images.githubusercontent.com/41586829/197401286-c6af59c8-9249-431c-b43d-84e77d89cd95.png)

![visualization_cryptotrading_and_tweets,gtrends](https://user-images.githubusercontent.com/41586829/197401366-8c652f2b-d33f-4686-ba2f-f1f0f5bbf799.png)

![visualization_inverserelationship](https://user-images.githubusercontent.com/41586829/197401391-d51052ba-3e57-48e8-aaca-fa3600376453.png)

## Additional Cleaning and Visualization ----

![visualization_cryptotrades_and_othervariables](https://user-images.githubusercontent.com/41586829/197401443-e13b5d33-cca9-4d97-8c7c-fc2adab0ab6f.png)

![visualization_checking_for_relationshsip_between_variables](https://user-images.githubusercontent.com/41586829/197401484-4c915d63-4201-4a67-9880-3291db088300.png)


## Model preparation
For the preparation of the model:

- Reliability test using Cronbach’s Alpha - Poor raw_alpha but good std.alpha (alpha > 0.7)
- Correlational matrix - Generally high r values
------

## Poor raw_alpha but good std.alpha (alpha > 0.7, except Tweet_Sentiments, Gold_Price)

## 
## Reliability analysis   
## Call: alpha(x = ., check.keys = TRUE)
## 
##   raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
##       0.88      0.88    0.93      0.52 7.7 0.017 0.58 0.77     0.55
## 
##  lower alpha upper     95% confidence boundaries
## 0.85 0.88 0.92 
## 
##  Reliability if an item is dropped:
##                   raw_alpha std.alpha G6(smc) average_r  S/N alpha se var.r
## Trade_Volume           0.85      0.85    0.91      0.49  5.7    0.023 0.078
## Tweet_Sentiments       0.92      0.92    0.95      0.64 10.8    0.014 0.038
## Webtrend_Hits          0.87      0.87    0.92      0.53  6.6    0.020 0.074
## Youtubetrend_Hits      0.84      0.84    0.89      0.46  5.2    0.025 0.064
## USDX_Index-            0.85      0.85    0.89      0.48  5.6    0.023 0.072
## RMB_Index-             0.84      0.84    0.90      0.47  5.4    0.024 0.067
## Gold_Price             0.89      0.89    0.93      0.58  8.3    0.017 0.066
##                   med.r
## Trade_Volume       0.52
## Tweet_Sentiments   0.69
## Webtrend_Hits      0.52
## Youtubetrend_Hits  0.52
## USDX_Index-        0.41
## RMB_Index-         0.41
## Gold_Price         0.64
## 
##  Item statistics 
##                     n raw.r std.r r.cor r.drop     mean sd
## Trade_Volume      101  0.85  0.86  0.85   0.80 -1.6e-17  1
## Tweet_Sentiments   48  0.43  0.43  0.30   0.26  1.2e-18  1
## Webtrend_Hits     100  0.75  0.76  0.73   0.66  1.4e-17  1
## Youtubetrend_Hits  99  0.92  0.93  0.95   0.90  4.9e-17  1
## USDX_Index-       100  0.89  0.88  0.90   0.83  2.0e+00  1
## RMB_Index-         98  0.91  0.90  0.91   0.85  2.0e+00  1
## Gold_Price        100  0.64  0.61  0.56   0.47 -4.2e-16  1

-----
## Model model regressed GOLD, RMB, USDX, web search queries (Gtrends hits), tweet volume and youtube searches (Youtube search queries) onto trade volume of crypto.

All components of gvlma has acceptable assumptions.
![model_ regressed GOLD, RMB, USDX, web search queries (Gtrends hits), tweet volume and youtube searches (Youtube search queries) onto trade volume of crypto](https://user-images.githubusercontent.com/41586829/197402275-17a4d9f1-95e5-4c7e-8c46-d3030aab21d4.png)

## All components passed
Model has an r^2 that is high (>0.85) with the estimate +/- CI of the model not include 0.

It appears that only RMB, USDX and web search queries display significant effects on the trading activity of crypto.
## # A tibble: 7 x 5
##   term              estimate std.error statistic p.value
##   <chr>                <dbl>     <dbl>     <dbl>   <dbl>
## 1 (Intercept)         0.205     0.0840     2.43  0.0196 
## 2 Tweet_Sentiments    0.0123    0.0657     0.187 0.853  
## 3 Webtrend_Hits       0.625     0.270      2.31  0.0260 
## 4 Youtubetrend_Hits   0.356     0.263      1.36  0.183  
## 5 USDX_Index          0.673     0.214      3.15  0.00310
## 6 RMB_Index          -0.447     0.207     -2.16  0.0368 
## 7 Gold_Price          0.257     0.149      1.73  0.0922
## # A tibble: 1 x 12
##   r.squared adj.r.squared sigma statistic  p.value    df logLik   AIC   BIC
##       <dbl>         <dbl> <dbl>     <dbl>    <dbl> <dbl>  <dbl> <dbl> <dbl>
## 1     0.874         0.854 0.399      44.9 5.18e-16     6  -19.2  54.4  69.0
## # ... with 3 more variables: deviance <dbl>, df.residual <int>, nobs <int>
  
  
Model 1
(Intercept)	0.205 * 
[0.035, 0.375]  
Tweet_Sentiments	0.012   
[-0.121, 0.145]  
Webtrend_Hits	0.625 * 
[0.079, 1.171]  
Youtubetrend_Hits	0.356   
[-0.176, 0.888]  
USDX_Index	0.673 **
[0.241, 1.105]  
RMB_Index	-0.447 * 
[-0.865, -0.029]  
Gold_Price	0.257   
[-0.044, 0.557]  
N	46       
R2	0.874   
*** p < 0.001; ** p < 0.01; * p < 0.05.

## Visualization of the Model ----
![visualization_of_the_model](https://user-images.githubusercontent.com/41586829/197402579-ad0db875-109a-4332-a2c3-51e8b2bc3681.png)
                                       
## Assess Multicollinearity ----

![assess_multicollinearity](https://user-images.githubusercontent.com/41586829/197402653-7e16544a-7847-48eb-b542-8229a79d4906.JPG)

Webtrend_Hits, Youtubetrend_Hits, USDX_Index, RMB_Index all have high VIF values of > 10 indicating high multicolinearity. We will be probing for interaction effects from these variables. 
  
  
  Trade_Volume=α+β1(Tweet_Sentiments)+β2(Webtrend_Hits)+β3(Youtubetrend_Hits)+β4(USDX_Index)+β5(RMB_Index)+β6(Gold_Price)+ϵ
![probing for interaction effects](https://user-images.githubusercontent.com/41586829/197402852-a807265c-12d9-4800-9fc1-f179a732b315.JPG)

  ![probing for interaction effects 1](https://user-images.githubusercontent.com/41586829/197402911-0e549dfe-76da-424d-913f-ab35c3c570b4.JPG)

  
Based on this we shortlisted the variables that display significant effects, and probed for interaction effects between them, namely RMB_Index, USDX_Index, and Webtrend_Hits on the rest of our variables individually. This is reflected in Parts 1-3 respectively.
  
# Part 1: RMB_Index * (Webtrend_Hits + Youtubetrend_Hits + Tweet_Sentiments + USDX_Index + Gold_Price)

To visualize the OLS regression analysis performed above, we stored the OLS regression model’s predictions. The analysis showed that the other variables had no interaction effect with RMB_Index.
  
![part1](https://user-images.githubusercontent.com/41586829/197403085-0d07c297-e542-455f-8c47-7f3f66905888.JPG)

![part1_](https://user-images.githubusercontent.com/41586829/197403089-f7fd02bf-fa42-4bc1-9887-c24d3594b72d.JPG)
![visualization_of_the_model_part1](https://user-images.githubusercontent.com/41586829/197403112-a31daa15-4b02-4c39-8b75-0f02b20f1227.png)

# Part 2: USDX_Index * (Gold_Price + RMB_Index + Webtrend_Hits + Youtubetrend_Hits + Tweet_Sentiments)
  
To visualize the OLS regression analysis performed above, we stored the OLS regression model’s predictions. THe analysis showed that there was an interaction effect between Tweet_Sentiments and USDX_Index. However on further probing, at all values of USDX_Index, there was no interaction effect of Tweet_Sentiments.
  
![part2](https://user-images.githubusercontent.com/41586829/197403215-f2e96726-8772-424a-8225-a1fdb66eaf8e.JPG)
![part2_](https://user-images.githubusercontent.com/41586829/197403221-ff9e554c-74e4-4308-934f-813ef8349420.png)
  
![part2_Plot Interaction (Tweet_Volume)](https://user-images.githubusercontent.com/41586829/197403224-2380dd31-2b45-4dbb-9b7a-3c20dece3aaa.png)

Run Simple Slopes Analysis ----
## SIMPLE SLOPES ANALYSIS 
## 
## Slope of USDX_Index when Tweet_Sentiments = -0.93 (- 1 SD): 
## 
##   Est.   S.E.   t val.      p
## ------ ------ -------- ------
##   0.52   0.31     1.70   0.10
## 
## Slope of USDX_Index when Tweet_Sentiments =  0.06 (Mean): 
## 
##   Est.   S.E.   t val.      p
## ------ ------ -------- ------
##   0.67   0.30     2.23   0.03
## 
## Slope of USDX_Index when Tweet_Sentiments =  1.04 (+ 1 SD): 
## 
##   Est.   S.E.   t val.      p
## ------ ------ -------- ------
##   0.82   0.31     2.66   0.01
