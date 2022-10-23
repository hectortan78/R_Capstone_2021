# R_capstone 
Observing Interplay Between Cryptocurrencies Trading Activity, Market Sentiments, and US Fiscal Stimulus

- To discern if the volume of cryptocurrency trading activity is directly or indirectly affected by social media buzz and influencers
- Scraped Google Search, Yahoo, Reddit, Twitter



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
