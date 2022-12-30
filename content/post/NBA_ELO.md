---
title: "Extending the ELO Ranking System for the NBA"
draft: false 
tags: ["math"]
categories: [ "math"]
katex: true
markup: mmark
---

# Extending the ELO Ranking System for the NBA

<div style="text-align: center;">
<img src="/nba_giannis.png" alt="NBA" width="700"/>
</div>

The ELO ranking system is a method of ranking the relative skill of players in repeated zero-sum games. In this article we investigate extending the ELO system for the NBA to capture relative performance as well as the overall game outcome.

Popularised by Chess, almost all sports that are zero-sum games have adopted the ranking system in some way. Any sport fan knows that all losses are not built equal.  The standard ELO system only considers the outcome through the lens of wins and losses. Therefore, an NBA teams ELO is equally reduced if they lose by one or thirty.

## Theory

Suppose that player $$A$$ has rating $$R_A$$ and player $$B$$ has rating
$$R_B$$. Then we may calculate the expected score, $$E_{A,B}$$ as:

$$E_{A,B} = \left(1 + 10^{\frac{R_B-R_A}{M}}\right)^{-1}$$

Therefore, once players $$A$$ and $$B$$ have played and player $$A$$ obtains a
score, $$S_{A,B}$$, we can update the ranking of player $$A$$ as:

$$R'_A = R_A + K \cdot (S_A - E_A) $$

Here, $$M$$ and $$K$$ scale the expected score and the shift in score after a
game respectively. 

Clearly, a starting point would be to have the score as binary, either a win or
loss. However, if we can obtain further game statistics  we can extend our
definition of score to better capture the result of the game, while preserving
its zero-sum nature. 

## Scraping the Data

To calculate the ELO scores, we will first have to obtain some data outlining the results of games. At a minimum, we require the outcome of each game. However, it may be interesting to investigate to incorporation of margin of win, turnover difference and field goal percentage into our ELO calculation. 

A natural place to start is [Sports Reference](https://www.sports-reference.com/). Therefore, the below function can be used to extract a team's wins and losses from a specified season.

<script 
src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2FNBA-ELO%2Fblob%2Fmain%2Fwordpress-examples%2Fget_team_stats_me.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on.md">
</script>

The helper function can be found [here](https://github.com/jacaranda-analytics/NBA-ELO/blob/main/src/functions.py).

For example, we could retrieve Houston's 1990 season results as follows:

{{< gist gden173 2599bf566ce873fcf302b7bcb90b069b  >}}

Since October 2022, Sports Reference have placed a limit rate on requests (twenty requests in a minute) which slows down accessing multiple years and teams. Thankfully the bulk of the data was scraped before this restriction. For all code relating to the web scraping found on [GitHub](https://github.com/jacaranda-analytics/NBA-ELO/blob/main/src/nba-extract.ipynb) under this website's organizational [page](https://github.com/jacaranda-analytics). Ultimately, we decided to save the game outcomes in decade blocks.

## Calculating ELO

Let's first load our data that we scraped in the previous section.

<script
 src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2FNBA-ELO%2Fblob%2Fmain%2Fwordpress-examples%2Fload-data.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on.md">
 </script>

With standard ELO, we are free to choose K which essentially caps how many ELO points a team can win or lose from a single game. Therefore, we will make K an input for our ELO helper functions. 

<script 
src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2FNBA-ELO%2Fblob%2Fmain%2Fwordpress-examples%2Finitialise-elo.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on.md">
</script>


INSERT PICTURE HERE

## Extending the Score Function

The above figure only uses the standard ELO, which is quite well known. What differentiates basketball from some of the zero-sum games that ELO was traditionally used for (Chess, etc.) is that there are metrics that paint a bigger picture in a *reasonably* clear and inuitive way. The above function collects more than just the win/loss, you may have seen that it also collects

- Home Team
- Margin of Victory
- Turner Totals 
- Field Goal Percentage

No two wins are the same. A team on the road winning by 30 with a 55% shooting percentage is fundamently different to a team sneaking away with a win after having 25 total turnovers. The above metrics will help place a win (or loss) on a specturm, rather than having it as a dichotomy. 
