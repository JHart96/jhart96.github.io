---
title: "The Problem with Permutations"
date: 2022-03-12T12:00:00+01:00
draft: false
---
{{< katex >}}


This is a short blog post to complement our [paper](https://www.biorxiv.org/content/10.1101/2021.06.04.447124v2)  on non-independence and permutation tests in animal social network analysis. We submitted the paper to a journal last year and had some pretty mixed feedback. We feel there's a lot to unpack in our paper, so to make things more manageable we wanted to release a blog post to coincide with our resubmission to explain again the issues we cover in our paper in bite-sized chunks.



Before digging in to the paper, let's start off with some background. Permutations are non-parametric methods based on randomising/permuting data. The key motivation behind permutation methods is that under null hypotheses (e.g. <em>social structure is random</em> or there's <em>no association between age and network centrality</em>), data can be randomised in some way to simulate the null distribution of test statistics. The observed test statistic can then be compared to the null distribution to calculate p-values and conduct null hypothesis significance testing. In the paper we focus on regression scenarios rather than questions about non-randomness of social structure.



One of the main justifications for using permutation in network analysis is that they appear to control for non-independence that is assumed to be inherent in network data.



There are 3 main messages in our paper: 



1) Permutations don't control for non-independence.



2) In the type of analyses we're interested in, we don't need to worry about non-independence of network data.



3) We think parametric methods should be used instead of permutations. 



Let's address these messages one at a time.


## Permutations don't control for non-independence


The first main message is quite simple. If data are non-independent, and you can't use standard parametric models because of this, permutations won't be of any use either. This is because permutations make a very similar assumption to parametric models - namely that data points are exchangeable. Exchangeability is an assumption that for practical purposes is nearly identical to independence.



This is important because the historical justification for using permutations in network analysis is that they control for the inherent non-independence of network data. However, we showed that if there is inherent non-independence in network data, permutations are in the same boat as parametric models - they don't do anything to control for this non-independence.



This might seem really bad, but just how bad is it? Fortunately it turns out this isn't a problem at all. This is because of the type of analysis we're usually doing when using permutations with regression models.


## Network-derived non-independence isn't a problem


First let's be clear on what kind of analysis we're talking about here. We focus on regression analyses where either A) the relationships between node metrics and node traits are assessed using a regression analysis, or B) the relationships between dyad metrics and dyad traits are assessed using a regression analysis. Depending on context, non-independence in networks can be a major problem. But in particular, for these two types of analysis, the inherent non-independence of network data isn't a problem.



To explain this, assume that X and Y are node metrics and node traits, and we want to regress one against the other, like this: <em>Y ~ X </em>(note: it doesn't matter if the metric is the predictor or response). The question at the heart of this analysis is about the relationship (if any) between Y and X. The relationship between Y and X an emergent property of a complex set of biological and mathematical processes that gives a descriptive insight into how individuals organise within social groups. In an ideal world, there would be no variation in this relationship across the population, but there always is. There are many sources of variation, such as noise in measurement of traits, noise induced by proxy variables, complex intra-individual processes, and more. Fortunately in our analysis, these variations happen at the nodal (or dyadic) level. This means that differences in the relationships between X and Y over the population can be explained by an independent noise term, and that the data can be considered to be independent.



This revelation is really important, because it means that an assumption of independence is completely appropriate for this type of analysis. Any additional sources of non-independence like repeated measures will still need to be accounted for, but the apparent non-independence of network data isn't a concern anymore. This means we can use either standard parametric models or permutations to run these kinds of analysis. There are a few additional minor considerations for dyadic regressions, so we recommend reading the paper in full to learn more about the types of non-independence unique to dyadic regression.



Where does this leave us? Permutations don't control for non-independence, but they don't need to either. Should we carry on using them then? We think no.


## We should use parametric models instead of permutations


The previous two messages were purely factual, but this third and final message is just our opinion. So feel free to stop reading here if you really like permutations! But we think it's worth considering using parametric models instead of permutations for a number of reasons. Firstly, at a sociological level, most researchers already use parametric models for non-network data. This means there's virtually no learning curve to using parametric models for network data too. But there are also a number of issues with permutations that we think are compelling reasons to consider retiring them:



<ul><li>When controlling for additional effects in permutations, the main effect size isn't corrected, so it's possible to get incorrect effect sizes (sometimes with the wrong sign) using permutations (Franks et al. 2020).</li><li>Permutations are reliant on null hypothesis significance testing and p-values, making it difficult to adopt best practices for reliable science (Halsey 2019).</li><li>It can be easy to test the wrong null hypothesis with permutations (see Weiss et al. 2020).</li><li>Datastream permutations can have convergence issues (Hart et al. 2022).</li><li>Permutations are incompatible with Bayesian methods, leaving a whole realm of methodology unavailable to network analysis.</li><li>Null distributions generated from permutations can be unrepresentative of the true null when sample sizes are small, which could lead to spurious conclusions.</li><li>Standard diagnostic tests aren't available for permutations so it can be difficult to check assumptions, again leading to potentially spurious results.</li></ul>



We have no intention of making anyone use one approach over the other, but we definitely think it's worth considering using parametric models instead.



We hope this helps to clear things up a bit. Please do get in touch if you'd like to share any of your thoughts with us.


## References


Franks, D. W., Weiss, M. N., Silk, M. J., Perryman, R. J., &amp; Croft, D. P. (2020). Calculating effect sizes in animal social network analysis.



Halsey, L. G. (2019). The reign of the p-value is over: what alternative analyses could we employ to fill the power vacuum?



Weiss, M. N., Franks, D. W., Brent, L. J., Ellis, S., Silk, M. J., &amp; Croft, D. P. (2020). Common datastream permutations of animal social network data are not appropriate for hypothesis testing using regression models.



Hart, J. D. A., Franks, D. W., Brent, L. J., &amp; Weiss, M. N. (2022). Why datastream permutations need diagnostics.
