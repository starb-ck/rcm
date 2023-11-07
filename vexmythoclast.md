---
title: /vexmythoclast
layout: page
permalink: /vexmythoclast/
---

# The Legendary Vex Mythoclast: Containerization for Pseudo-Survival Analysis in R

I've been playing a lot of Destiny 2 lately. It's a fun game in the style of an MMOFPS. You level up, play in 'fireteams' with your friends, and compete in difficult challenges like the player-vs-player (PVP) Crucible or player-vs-enemy (PVE) raids and dungeons.

One of the most challenging PVE raids is called Vault of Glass. Said to be ["the most challenging experience that Bungie has ever created,"](https://www.youtube.com/watch?v=hRRKtkuOeig) even getting past the entrance in this raid can take 45 minutes. Teams of players have to push through a staggering multitude of computer-controlled enemies and punishingly tough bosses. This trial isn't without reward though; upon completion there's a small chance that players receive the legendary Vex Mythoclast weapon.

How small? Well, that's what we're going to figure out.

## Background

This analysis originates from work done by **u/Pinnkeyy** and **u/TBEMystify** on various Destiny subreddits. Both of these analyses were attempts at calculating the drop rate of Vex Mythoclast. The [first attempt](www.reddit.com/r/raidsecrets/comments/pp5zno/vex_mythoclast_drop_rate_survey/) consisted of a survey of Destiny players for how many VoG raids were completed before obtaining the weapon. The [second attempt](www.reddit.com/r/DestinyTheGame/comments/ppmbxu/vex_has_a_5_drop_rate_heres_proof/) was our first step into webscraping, leveraging API tools such as [raid.report](https://raid.report) and [braytech.org](https://braytech.org) in order to obtain higher data volume and reduce the responses bias towards Reddit users.

There are known limitations to both of these prior analyses, primarily due to the sample bias and manual nature of data collection. This made it difficult for either user to obtain truly conclusive evidence for the Vex Mythoclast drop rate. After discussing this with a few members of the **r/DestinyTheGame** community, we recognized an opportunity to query the Bungie API directly to collect a high volume of data.

The below analysis applies **u/TBEMystify**'s method at scale. We utilize HTML scraping and GET request tools in R to source approximately 1 million player records for VoG completions. We then take these records and query them against the Bungie API in a containerized application to determine whether or not the player possesses Vex Mythoclast. Finally, we analyze the likelihood that a player possesses Vex Mythoclast given a particular number of VoG completions. We propose that this relationship can be modeled in the second-order form:

$$  y = Ax^n + Bx + C $$

where $y$ is the probability of owning Vex Mythoclast, $x$ is the number of Vault of Glass completions, $A$ and $B$ are unknown coefficients, and $C$ is some arbitrary constant. Below is an in-depth explanation of the methodology for this anlaysis and how this model was determined.

## Method

Our first step is similar to **u/TBEMystify**'s method in that we will be accessing [raid.report](https://raid.report) in order to search for players who have completed the Vault of Glass raid at least one time. This was done by browsing through the website while examining my browser's developer tool and looking for the site's data source. Once the source is identified, scraping player records is simply a matter of iterating over HTML requests for pages of 100 players each. Because the first page shows the top leaderboard, our dataset will start with players with the most VoG completions. We'll set an upper limit of one million players (10000 pages of 100 players), as the response volume quickly skyrockets once we get down to five or less completions.

{% highlight r %}

results_master <- data.frame()

lowlim <- 0
uplim <- 10000
for(n in lowlim:uplim){
  
  skip_to_next <- FALSE
  
    url_stem <- "REDACTED"
    url_page <- as.character(n)
    url_pagesize <- "&pageSize=100"
    
    url_full <- paste0(url_stem,url_page,url_pagesize, sep="")
    
    tryCatch(
      results_temp <- read_html(url_full) %>% 
        html_nodes('body') %>% 
        html_text() %>% 
        list(),
      error = function(e) {skip_to_next <- TRUE})
    if(skip_to_next){next}
    
    results_df <- as.data.frame(fromJSON(results_temp[[1]])$response) %>% 
      select(2,1)

    results_add_page <- data.frame(results_df$entries.destinyUserInfo$displayName,
                                   results_df$entries.destinyUserInfo$membershipId,
                                   results_df$entries.destinyUserInfo$membershipType,
                                   results_df$entries.value,
                                   n)

    results_master <- rbind(results_master, results_add_page
}

head(results_master)

## # A tibble: 6 x 2
##   vog_username   vog_count
##   <chr>          <chr>    
## 1 Ninjah720      1508     
## 2 KING_ANUBIX    1331     
## 3 hallowdragonxx 1313     
## 4 xSwerve_88     1190     
## 5 jollys79       979      
## 6 Alan Sparks    977

{% endhighlight %}
