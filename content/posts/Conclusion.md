---
title: "Conclusion"
# date: 2020-09-15T11:30:03+00:00
weight: 5
# aliases: ["/first"]
tags: ["Conclusion", "Limitations"]
categories: ["Retrieval", "Analysis"]
# author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: true
hidemeta: false
comments: false
summary: "Conclusion"
description: "limitations of approach"
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

As seen in the results section, we understood that Kendall Tau shows negative similarity scores. This is because it tries to penalize the order equally in higher ranks as well as the lower ranks. Since our ranked list consists of around ~50 elements (assuming the dataset size is ~200 elements), it is very difficult to get accurate results for the entire list.

On the other hand, RBO scores give out a decent correlation of around 0.6. RBO penalizes the order more if there are errors higher up but is lenient with errors down the order. 

### Limitations of our approach

We observed the following limitations during our testing:

1. Evaluation: In the absence of a ground truth ranked list, we can not evaluate the ranked list we have produced. Given the nature of our problem statement, it is very difficult for us to get the ground truth since this will change for every query that the user inputs. This is also particularly difficult to estimate as it won't be giving an accurate representation of the results that we obtain from our ranking algorithm.
2.  Bad links: Some links have to be excluded from our analysis due to scraping issues. We found that the algorithm is often limited by the type of content it can scrape and this is particularly difficult for pages that include pop ups, ads and other restrictions like authentication and rate limits that are enforced by the web pages being scraped. In our current approach we tried to overcome this using Selenium and by scraping the body tags. Selenium also allowed us to eliminate some of the other html tags that might get scraped along with the required content. While it is also possible to use Selenium to perform per-page processing such as removal of pop-ups by specifying coordinates where could selenium auto-click in attempt to close the pop-ups, it was not feasible to do that for every webpage we are trying to scrape (given the differing structure and positioning of popups on webpage).