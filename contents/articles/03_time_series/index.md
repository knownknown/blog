---
title: WL3 - Time Series
author: author
date: 2014-04-29
template: article.jade
---

*Examining the distribution of cables and entities over time provides important context and identifies a small number of well-documented entities that are likely to be important. However, we're still not capturing the direct relationships between these entities.*

<span class="more">

*This post is part #3 in an ongoing series describing data analyses of the Wikileaks cables.*

In the previous post, a naive list of highly occurring entities provided some sense of the diversity of this data as well as a condensed "Top 10" of the people, locations, and organizations discussed in the cables. One dimension that's entirely missing from that approach is that of time. Each cable has been coded with a time-stamp for when it was sent, allowing us to look at the frequency of communication across the available time-frame. To get a birds eye view of all cables, I've plotted their number over consecutive 10-day periods, with the year breaks indicated:

<figure class="full">
![time-series total](time_ser.total.png)
</figure>

It's immediately obvious that the bulk of the cables were gathered from 2006-2010. We can similarly zoom in on cables mentioning specific entities and examine their time series. As an example, let's take a look at occurrences over time for two of the previously identified common words "Saakashvili" (the president of Georgia) and "South Ossetia" (the disputed, formerly Georgian, territory). The representation is the same as before, but I've also highlighted the explicit start of the Russo-Georgian War in August, 2008:

<figure class="full">
![time-series South Ossetia example](time_ser.example.png)
</figure>

Lo and behold, we see a substantial up-tick in mentions of both entities at the start of the war. This visualization makes it clear that the great number of Saakashvili mentions is almost entirely explained by events of late 2008. We can also see that both entities were mentioned regularly but infrequently in the preceding years, and that the increase in mentions subsided almost entirely by the start of 2009, particularly for Saakashvili. That the spike in mentions happened in the same week as the deceleration of war (even though tensions between Georgia and Russia had been high since at least April) suggests that US diplomats were not unusually focused on the issue prior to military escalation. Just looking at these occurrences over time has provided a great deal of context.

Similarly, we can look at common entity occurrence surrounding the March, 2008 election of pint-sized president Dimitri Medvedev:

<figure class="full">
![time-series Medvedev example](time_ser.example2.png)
</figure>

In this instance, the increase in mentions of Medvedev preceded his election by months (starting around the time of his nomination in January, 2008), indicative of some advanced knowledge. On the other hand, the nearly complete lack of mentions prior to 2008 suggests that he had not recently been a key diplomatic figure. In comparison, Putin is discussed consistently throughout the entire analysed period and his stature is largely unaffected after being replaced by Medvedev.

###Broader trends

Looking at a small number of entities is clearly informative, but somewhat unrealistic; in the above examples we started with a known event and looked at it in relation to certain known entities. What we actually want is the complete opposite: start with a pile of unknown data and have the analyses reveal both the important entities _and_ the events they are linked with. This turns out to be more difficult that it first seemed. If we simply look at the most mentioned entities in each month, we tend to see individuals that appear consistently throughout the time-line or their administration. As in the Putin example above, discussion of these individuals (Medvedev, Lavrov, Obama, etc.) doesn't vary much over time, and so the time-dimension becomes uninformative. At best, we'll know when someone big has come into office; at worst, we'll just have a messier version of the "Top 10" list. We can deal with this by normalizing each entity by their total number of occurrences and then look for monthly peaks, but that shifts the data too much in the direction of minorities. After normalization, someone who gets 1,000 mentions in Jan. and Feb. ranks below someone who gets 2 mentions in Jan. only, so individual blips get hugely inflated.

The working solution is to use a hybrid of the two strategies: first the blips are weeded out, then the remaining important entities are normalized and compared. For every month, we identify all entities that are the most mentioned - these are important enough to show up frequently _at some point in time_.  We can then tune the monthly inclusion threshold to select the desired number of entities in total. After selecting this set of core individuals we normalize them and examine their occurrences over time. The approach is _ad hoc_ in the inclusion, but that will primarily effect the overall number of samples viewed.

Below is the horizon plot for LOCATION entities:

<figure class="full">
![LOCATION distribution](time_ser.LOCATION.png)
</figure>

Fundamentally, this is not much different from a heat-map or "small-multiples" chart, but it provides more granularity than the former while still being very efficient. One concern is that the _ordering_ of individual rows can affect the interpretation, and here they have been grouped using simple hierarchical clustering. This tends to place similar trend-lines together so that correlations are easier to pick out by eye (though it is far from perfect). Continuing from the previous example, we see that "South Ossetia", "Abkhazia", and "Georgia" all cluster together and are driven by a peak around the August '08 War.

We can similarly examine the time series of top PERSON entities:

<figure class="full">
![PERSON distribution](time_ser.PERSON.png)
</figure>

Several general time-related topics are starting to emerge. We can clearly see the changing administrations in 2009 as the mentions of Secretary Rice are replaced by Barack Obama, Hilary Clinton, and Rose Gottemoeller (Assistant Secretary of State for the Bureau of Arms Control, Verification and Compliance). We also see a 2007 cluster of Bosnian politicians (Ivanic, Tihic, Silajdzic) likely related with Ahtisaari, the UN envoy for the Kosovo status process. Also interesting is the consistent presence of Milorad Dodik. Dodik was one of the surprising entities at the top of all cables, and it's clear now that this was not a fluke or due to a single key date.

###Discussion

Looking at the data across time also makes clear it that we're still missing *a coherent, time-coded context for each of the well-represented entities*. Many context-specific questions remain unanswered: What is being discussed in the flurry of cables on Milorad Dodik at the end of 2008? Are the punctuated entities (e.g. Elisabeth Millard and Stephen D Krasner) co-occurring by chance or do they have a relationship? In short, does each of these rows represent an individual event or just one strand from a complex, correlated community? We've gained some intuition by looking at occurrences over time, but these questions can only be answered by broadening our analysis to *co-occurrences* of entities within cables and across time.
