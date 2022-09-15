---
title: "How Accurate are Inferred Social Networks?"
date: 2021-08-08T12:00:00+01:00
draft: false
---
{{< katex >}}
In behavioural ecology, animal social networks are used to answer a wide variety of questions. However, unlike in the analysis of human social networks, we can’t ask animals what their social preferences are. Instead we have to estimate them based on observable events like spatial associations or interactions. This means we can never be fully certain in the estimated social preferences, and if very few observations are made, it is possible that the estimated social preferences could be quite inaccurate. We recently wrote a paper to tackle some of these issues [1].

## Binary and Count Data
Two very common types of data used to build animal social networks are binary data and count data. These are broad classifications that are important in understanding what the edges in social networks really mean. In binary data, observations are collected over a series of fixed sampling periods. Observations are simply the binary presence or absence of social events within each sampling period. The number of observed social events between a pair of individuals is X, and the number of sampling periods where a social event could have been observed between the pair is D. Network edges are calculated as the simple ratio index (SRI), which is defined as SRI = X/D. This means that the SRI is equivalent to the probability of seeing a social event in a randomly-selected sampling period.

Count data is where the count of social events that were observed between two individuals is recorded over the amount of time that a social event could have been observed between them. This type of data is usually used to build social networks by dividing the count by the time, giving the rate of social events occurring per unit time. In animal social network analysis, this value is known as the simple ratio index (SRI). Mathematically we define this as SRI = X/D, where X is the count of social events, and D is the total amount of time spent observing at least one of the two individuals.

In both of these types of data, we assume that the SRI is a useful estimate of the underlying social preference. This assumption is equivalent to assuming that in binary data, the count X is a draw from a binomial process with D trials and success probability equal to the SRI; and that in count data, the count X is a draw from a Poisson process with rate equal to D * SRI. Using these statistical processes to model binary and count data, we can estimate how accurate our estimated social networks are without making any additional assumptions than those already made when calculating the SRI.

Normalised probability distribution of SRI values for different amounts of time spent sampling. Under a lower sampling time, the probability distribution is much wider than the higher sampling case. In both cases the true SRI is 2. This shows that the amount of time spent sampling will impact the accuracy of estimated SRI values.

## Accuracy of Social Networks

Hal Whitehead recognised this in a 2008 paper and developed a method to estimate the accuracy of social networks constructed from binary data [2]. In our new paper, we have extended this method to count data [1].

The key notion behind the method is that the dissimilarity between the estimated social preference (SRI) and the underlying social preference will reduce towards zero as sampling (D) increases. As a result, the correlation between the estimated and underlying social preference is a good measure of the accuracy of the social network. This allows us to calculate the correlation between estimated and underlying social preference in terms of the ratio of variances for the estimated and underlying social preferences (see our paper for full details).

The full details can be found in the original papers, but in short, Whitehead found that the accuracy of social networks constructed from binary data can be estimated using the following equation:

where S is the coefficient of variation of social preferences (often referred to as social differentiation) and G is the mean number of observed social events per dyad.

For count data, we found in our paper that the accuracy of social networks constructed from this kind of data can be estimated by:

where S is again social differentiation, \\(\mu\\) is the mean rate of social events over all dyads in the networks, and H(D) is the harmonic mean of the sampling times of all dyads in the network.

These two equations can provide useful estimates of how representative a estimated social network is of its underlying social network, and can have consequences on the power of subsequent statistical analyses. This could be useful for determining whether or not sufficient data have been collected to carry out an analysis, for splitting up data into multiple intervals, or even just to validate the accuracy of networks. If you’d like to know a bit more about this, we explore these ideas further in our paper.

If you’re interested in using these methods in your study, for R implementations check out the social_differentiation function in the R package aninet (for binary data), and our R package pwrIRGP (for count data). Hal Whitehead’s original code in MATLAB is available in SOCPROG.

## References

[1] Hart, J. D., Franks, D. W., Brent, L. J., & Weiss, M. N. (2021). Accuracy and Power Analysis of Social Interaction Networks. bioRxiv.

[2] Whitehead, H. (2008). Precision and power in the analysis of social structure using associations. Animal Behaviour.