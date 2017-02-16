---
layout: post
title:  "Options Predictability"
date:   2017-02-16 12:00:00 -0500
categories: [Options]
---

Apparently, there is a [Brevan Howard Centre for Financial Analysis](https://wwwf.imperial.ac.uk/business-school/research/brevan-howard-centre-for-financial-analysis/), which I didn't know existed until yesterday.  To anyone who has ever wondered why someone might like to think about vol rather than just delta-one assets (like stocks and bonds), the Brevan Howard Centre for Financial Analysis presents an interesting point for consideration.

The researchers [Cao, Bing, Tong, and Zhan (2016)](http://ink.library.smu.edu.sg/cgi/viewcontent.cgi?article=5906&context=lkcsb_research) consider 12 firm-level statistics (log market value, log book to market, 1m return, 2-12m return, regression residuals, etc.) and find that for almost two decades through 2012, delta-hedged option returns have been significantly predictable by a subset of these statistics.  Interestingly, this stands in contrast to evidence from [Chordia, Subrahmanyam, and Tong (2014)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2029057) which uses a Vector Autoregressive model to show that stock return (not options) predictability from a similar set of statistics has declined with the explosion of hedge fund AUM and a fall in transaction costs.

Now, anyone who has been around the asset management space has probably heard a few conflicting views on options trading.  Some lament that trading options requires guessing many variables correctly, rather than just one (most options expire at a fixed time, and so a buyer of an option must have an opinion not just on the direction of an asset, but also on how much and how quickly it can move), some view options as extremely dangerous, and still others think they're the path to success in markets ("Sell the prem, live the dream" --Folk legend). One would guess that options strategies should have suffered similar declines in profitability, but it's also well known that volatility exhibits many persistent properties that aren't evident in underlying stocks (volatility returns auto-correlate, and in some sense volatility mean-reverts). As an asset, therefore, vol is very different from things like bonds and stocks, and perhaps it (and other higher-order derivatives).  It's a shame a lot of the data powering the Cao et al. paper isn't freely available (as far as I know) to all, but Cao et al. suggests there's a wealth of value to be found in such datasets.

By the way, anyone who is interested the quant features that power a surprising amount of asset allocation should consider reading both of the above papers.
