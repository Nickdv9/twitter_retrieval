---
title: "Introduction"
# date: 2020-09-15T11:30:03+00:00
weight: 1
# aliases: ["/first"]
tags: ["Introduction"]
categories: ["Retreival"]
# author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
summary: "Intro to URL embedded retreival"
description: "Introduction to URL Embedded Retrieval & Ranking system for Twitter"
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

One of the major aspects of a social networking service like Twitter is its ability to provide an intuitive and accurate search system. Twitter makes use of Earlybird, a real-time, reverse index based on Apache Lucene, to provide real-time search results. Twitter's search engine serves billions of queries per day from different Lucene indexes, while appending millions of tweets per day in real time.

The search systems at Twitter process hundreds of thousands of queries per second and most involve searching through posting lists of thousands of items, making the speed at which we can consume the content inside the tweets a critical factor in serving queries efficiently. In order to improve the search experience we propose a different solution which allows users to facilitate tweets with link embeddings to get information on a particular subject matter.

Consider a scenario where the user desires to learn about some ongoing news on Twitter. Twitter results can be overwhelming at times with more information than the user can keep up. If the user's search query is "elon musk", the search result would often be related to Elon Musk. But user might actually be looking to get popular articles related to spaceX or Tesla or even about the recent acquisition of Twitter. Hence we have introduced an idea called context words.
