---
title: "Methodology"
# date: 2020-09-15T11:30:03+00:00
weight: 2
# aliases: ["/first"]
tags: ["Methodology"]
categories: ["Retrieval"]
# author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
summary: "Implementation"
description: "Pre-processing and approach"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: false
# ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/Nickdv9/twitter_retrieval/tree/main/content/"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

### Web Scraping

An important part of information retrieval is scraping. We used a library called Tweepy for extracting tweets from the Twitter Api. The search query and the date_since fields can be dynamically entered by the user.

We used "elon" as the search query and date_since is from the beginning of this year.We extracted popular tweets first, but the number of tweets returned were really less. Then we extracted mixed tweets, which is a mix of popular as well as real time tweets and came up with a scoring function to rank these tweets. ( we can include the get_tweet_score function here)

We used a filter to obtain tweets with embedded links, then we cleaned up the link metadata. We used another filter to obtain tweets from verified profiles. The idea of including verified profiles is to ensure the information that is posted on Twitter is coming from the actual source instead of bots or fake profiles (Ex. - A tweet from a source claiming to be NY Times is indeed NY Times and not a pretend-profile.)

For the scraping, we tried both BeautifulSoup and Selenium. Selenium was better at handling pop-ups and paywalls. This results in our final dataset.

    # Following is the scoring function we used to rearrange the links

    def get_tweet_score(followers, following, totaltweets, retweetcount):
        # factors denoting popularity of a given tweet
        # consider the following order of importance
            # retweetcount
            # followers to following ratio
            # totaltweets by the user account

        # normalized follower to following ratio
        ratio = (0.8 * (followers + 1))/(0.2 * (following + 1))

        # weights distribution

        # 60% retweetcount
        wt_rt_count = 0.6

        # 40% followers-to-following ratio
        wt_ratio = 0.4

        # log(totaltweets) since total tweets can be very large
        wt_total = math.log10(totaltweets)

        # calculate score and return
        return wt_rt_count*(retweetcount) + wt_ratio*ratio + wt_total


### Pre-Processing

The pre-processing step included working on the query terms and the body scraped from the links as mentioned above.

Following steps were followed with the help of NLTK package :
1.  URLs were removed 
2.  Contractions were replaced (eg: `I'll` was converted to `I will`)
3.  Tokenization 
4.  Punctuations were removed 
5.  Stop words were removed 
6.  Lowercase conversion
7.  Numbers were removed
8.  Stemming using Porter Stemmer

These helped us create cleaned query terms and the body content which we used to match. Once the preprocessing was done, scores were then calculated using different matching algorithms BM25, Tf-IDF, Tf-IDF with cosine similarity, PL2, InL2.

### Approaches

The following two approaches were implemented to process the data:

#### Approach 1

In this approach, the user will first pass the search query to extract tweets from the Twitter API. 
Then, we filter the tweets with links and also extract tweets that are mixed and popular. Mixed tweets also include tweets in real time.

Here we pass the tokenized version of the initial search query that is entered by the user as a query to the ranking algorithm. The idea behind passing tokenized information is to ensure we handle search queries that include multiple words. Data passed to the ranking algorithm in the form of documents is the body coming from the webpage referred by the URL

We tried several unsupervised ranking algorithms since we were unsure about ground truth, some of which are TFIDF with cosine similarity, BM25 etc. In Particular, we can obtain a relevant ranking score from these algorithms.

#### Approach 2

The other approach we considered was using different terms for matching. Instead of using the query words, we decided to introduce context words related to the query. 

Context words are essentially words which help build on the query words. For example if a user wants to query "Elon Musk", the API would return search results which contain those words. But there may be news regarding Tesla or SpaceX which may be currently trending and might be missed by the search results. 

Hence, to introduce context words, we are filtering through the popular tweets returned by the Twitter API. We assume that the popular tweets obtained from the Twitter API will also consist of tweets talking about Elon Musk as well as topics directly/indirectly related to him. We will preprocess these as explained and use these tokens to match with the body of different links. 

Now, the links which match higher with these tokens will contain more tokens from the context words as well, thereby making the results more relevant to currently trending topics.
