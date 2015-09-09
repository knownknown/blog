---
title: Wikileaks 2 - A Brief Note on Sentiment
author: author
date: 2014-04-23
template: article.jade
---

*Inferring the emotional content of text opens up very cool possibilities, but it's just not appropriate for data with this level of nuance and complexity.*

<span class="more">

**Introduction**

*This post is part #2 in an ongoing series describing data analyses of the Wikileaks cables.*

One of the more exciting NLP applications to this data is "sentiment" analysis, which aims to automatically classify sentences and entities with the writer's contextual emotions. Naively, one could this by simply taking a set of words with known sentiment scores ("happy"=positive, "awful"=negative, etc.) and counting up their occurrences to get an overall sentence or document score (the so-called _bag of words_ model which ignores word order and grammar). This has some obvious draw-backs ("he was happy to spit in our face", "we had an awfully good time") and has been heavily extended to take into account local and even multi-sentence context. The Stanford [Recursive Model](http://nlp.stanford.edu/sentiment/), for example, turns the sentence into a tree using parts-of-speech, then builds a combined score from the leaves up. Perhaps "awfully good" could be correctly understood as single positive phrase instead of one positive word and one negative word. If the algorithm works, the implications can be tantalizing; see, for example, the IKANOW [analysis](http://www.ikanow.com/making-the-most-of-sentiment-scores-with-ikanow-and-r/) of Enron e-mails; and Saif Mohammad's time-series [analysis](http://www.saifmohammad.com/WebDocs/NRC-TechReport-emotions-in-books-and-mail.pdf) of sentiment in books. In the context of diplomatic data, quantifying sentiment would express in numbers the cloud of emotions surrounding those actors and organizations we're studying:

* What individuals are the most/least liked?
* How has that changed over time?
* Which are the most controversial, liked and hated in equal measure?
* Which diplomats are unusually friendly to some individuals but not others? This last one is especially important as it provides insight into the potential biases of our narrators.

This emotional content may be even more informative than the factual, especially when the data has been heavily ascertained from one point-of-view. As it happens, bag-of-words sentiment analysis has been applied to such data to quantify U.S. relationships with foreign nations ([here](http://www.technologyreview.com/view/423601/automated-processing-of-wikileaks-cables-reveals-us-friends-foes/) and [here](http://vikparuchuri.com/blog/tracking-us-sentiments-over-time-in/)). Those projects are novel and the application clever, but the results are clearly noisy and not particularly informative without many assumptions. Perhaps we could do better by using a more advanced sentiment parser; analysing a single region where word-choice is more likely to be controlled; linking the sentiment to known political actors, and looking at a generally richer dataset.

**Results**

Let's start with the good news. Here are some example sentences that had the highest sentiment:

* Analysts predict several decades of sustained robust economic growth, thanks in part to India's youthful population and its technical and scientific prowess.
* USAID post-tsunami reconstruction projects are moving ahead smartly.
* He has good Kremlin access and a well-developed sense of what is realistic in light of Kremlin policies.
* He and President Putin are very popular and receive credit for Belgorod's strong economy, active civil society, and vibrant academia.

In the second instance we almost certainly got lucky that some other British-ism hadn't been used instead of "smartly" (say, "briskly"). And the last two examples are nuanced in the real subject of their approval. But let's not quibble, these are really quite positive!

The bad news, though, is that these examples are pretty much the only true positives (in every sense of the word) over the tens of thousands of sentences that received sentiment scores before my computer said "enough". Nearly every sentence was given a negative score, and examining individual cables that had extreme sentiment averages showed no indication of accuracy. If anything, the average sentiment was mostly representative of cable size and complexity (which makes sense, as the sentiment parser appears to down-weight complex sentences with positive words). None of the most negatively ranked cables I looked at could reasonably be interpreted as accurately classified. This, coupled with the fact that sentiment analysis is easily the most computationally intensive part of the language analysis, lead me to reluctantly abandon the strategy.

Sentiment analysis clearly has value, and sentiment-based predictors of everything from [music reviews to twitter messages](http://www.lct-master.org/files/MullenSentimentCourseSlides.pdf) already do very well. But pulling out emotional terms from 140 characters appears to be a much easier problem that annotating large, nuanced political documents.
