# R_capstone 
Observing Interplay Between Cryptocurrencies Trading Activity, Market Sentiments, and US Fiscal Stimulus

- To discern if the volume of cryptocurrency trading activity is directly or indirectly affected by social media buzz and influencers
- Scraped gTrends, Yahoo, Reddit, Twitter



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


Data sets that were obtained:

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

