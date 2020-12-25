# Twitter Followers & Benford's Law 


Benford's Law is an observation about the frequency distribution of leading digits in many real-life sets of numerical data. The law states that in many naturally occurring collections of numbers, the leading digit is likely to be small.

Benford's law tends to apply most accurately to data that span several orders of magnitude. As a rule of thumb, the more orders of magnitude that the data evenly covers, the more accurately Benford's law applies. 

### Benford's Distribution
![](image/slides/benford_dist.png)

This method can be used to test if a set of numbers may be artificial (or manipulated).

<br/>

### Applications Of Benford's Law
* Accounting fraud detection
* Scientific fraud detection
* Macroeconomic data
* Price digit analysis
* Genome data
* Election data
* Legal status

<br/>

## Motivation
In the recent years, Twitter has become one of the major forums of American political discourse, we started to hear more about bot farms, propaganda bots, and bots driving online discussions of current events. Here are few headlines to get a flavor of bots on Twitter:

[Russia's manipulation of Twitter was far vaster than believed - politico.com](https://www.politico.com/story/2019/06/05/study-russia-cybersecurity-twitter-1353543)

[Researchers: Nearly Half Of Accounts Tweeting About Coronavirus Are Likely Bots - npr.org](https://www.npr.org/sections/coronavirus-live-updates/2020/05/20/859814085/researchers-nearly-half-of-accounts-tweeting-about-coronavirus-are-likely-bots)

[The role of bot squads in the political propaganda on Twitter - nature.com](https://www.nature.com/articles/s42005-020-0340-4)

A Twitter user's numeric statistics such as follower count, friend count, favorites count, and statuses count should span several orders of magnitude, these counts can vary from zero to millions, therefore Benford's Law should be applicable. 

I wanted to see if applying Benford's Law to Twitter users' followers' numeric data can reveal unusual user activity , and if it has a possibility of bots detection. 

## Data Source 

I used [Tweepy](https://www.tweepy.org/) to access the Twitter API, and downloaded the 10,000 most recent followers for each of the 6 Twitter profiles I chose. 

I chose the 6 important political leaders in the U.S., they are:

1. President Donald Trump @realDonaldTrump 

2. President-Elect Joe Biden @JoeBiden

3. VP Mike Pence @VP

4. VP-Elect Kamala Harris @SenKamalaHarris

5. Senate Majority Leader Mitch Mcconell @senatemajldr

6. House Speaker Nancy Pelosi @SpeakerPelosi

From the 60,000 twitter user objects, I extracted the count of their followers, friends(following), favorites, and statuses. I also threw in the user creation date. 

<br/>

## Hypothesis Testing

Null Hypothesis: The 4 numeric statistics of the 10,000 followers of each user follow the Benford's Distribution

Alternate Hypothesis: The 4 numeric statistics of the 10,000 followers of each user don't follow Benford's Distribution

I used a Chi-Square test, and an alpha = 0.05

<br/>

## Findings
Note: count of 0's have been removed from the dataset, since 0 does not have a leading significant digit. 

I ran the chi-square test and graphed them with and without count = 1, and something interesting did emerge. 

As you can see below, if we exclude the data points that are equal to 1, the graphs look a lot different than if we include them. Meaning there are a lot of followers with only count of 1 in their statistics (1 follower, 1 favorited tweet, etc.)

<br/>

### Donald Trump's followers
Trump's followers, including count = 1
![](image/realDonaldTrump_include_1.png)

For reference, below graph excluded the count of 1's. We see a drop in leading digits of 1 compared to above graph, which tells us that there are a lot of followers that have count of 1 in their follower, favorites, and statuses counts. 

Trump's followers, not including count = 1
![](image/realDonaldTrump_ignore_1.png)

Below is the creation date of the 10,000 recent followers of @realDonaldTrump, majority of them were created in the 9 days of December 2020, which is a bit suspiscious to me. 

![](image/creation_date/realDonaldTrump_followers_creation_date.png)

<br/>

### Joe Biden's followers

Biden's followers, including count = 1

![](image/JoeBiden_include_1.png)

Biden's followers, not including count = 1

![](image/JoeBiden_ignore_1.png)

We are seeing a similar trend as Donald Trump's Followers, where a lot of the followers have only count of 1 for their follower, favorites, and statuses counts. 

Majority of Joe Biden's recent followers are also created in the 9 days of December 2020. 

![](image/creation_date/JoeBiden_followers_creation_date.png)

<br/>

### Mike Pence's followers

Pence's followers, including count = 1
![](image/VP_include_1.png)

Pence's followers, not including count = 1
![](image/VP_ignore_1.png)

Similar to Trump and Biden, Pence's followers also have too many leading digits of 1 when we include count of 1, and not enough 1 when we exclude count of 1.

The Majority of Pence's recent followers were created in 2020 before December. 

![](image/creation_date/VP_followers_creation_date.png)

<br/>

### Kamala Harris's followers

Harris's followers, including count = 1
![](image/SenKamalaHarris_include_1.png)

Harris's followers, not including count = 1
![](image/SenKamalaHarris_ignore_1.png)

Very similar to the 3 accounts we saw before, too many counts of 1. 

Majority of Harris's followers were created in the 9 days of December 2020, similar to Donald Trump's and Joe Biden's followers. 
![](image/creation_date/SenKamalaHarris_followers_creation_date.png)

<br/>

### Mitch Mcconell's followers
Mcconell's followers, including count = 1

![](image/senatemajldr_include_1.png)

Mcconell's followers, not including count = 1


![](image/senatemajldr_ignore_1.png)
Similar situation with count of 1 as previous users, but not as significant.

The creation date of recent followers are mostly in 2020 before December, and also before 2016. 
![](image/creation_date/senatemajldr_followers_creation_date.png)

<br/>

### Nancy Pelosi's followers

Pelosi's followers, including count = 1
![](image/SpeakerPelosi_include_1.png)

Pelosi's followers, not including count = 1
![](image/SpeakerPelosi_ignore_1.png)

These 4 statistics have a similar results as Mitch Mcconell's followers, where there is too many count of 1's, but not as significant as Trump, Biden, and Harris. 

The majority of Pelosi's followers are created in 2020 before December, followed by creation dates before 2016, and creation dates in the 9 days of December 2020. 
![](image/creation_date/SpeakerPelosi_followers_creation_date.png)


At this point, I was disappointed to find the chi-square test detected anomalies for all 4 statistics of the followers of all 6 politial leaders, I started to wonder if this really works. I didn't have time to request more data from Twitter, or I would like to test this on more users, not just political leaders. 



But wait, bonus round! 

@UnfollowTrump is a Twitter account that retweets everything @realDonaldTrump tweets, so people can read @realDonaldTrump's tweets without following his account. 

This is the only account where the chi-square test detected no anamoly in any of the 4 statistics. 

![](image/UnfollowTrump_include_1.png)

![](UnfollowTrump_followers_ignore_1.png)

The followers of this account also have the least suspiscious distribution of account creation date, majority of them were created before 2016, while we were seeing majority of followers of Trump, Biden, Harris are created in the 9 days of December 2020.

![](image/creation_date/UnfollowTrump_followers_creation_date.png)

Here are the bar graphs for the 6 accounts for comparison

![](image/creation_date/realDonaldTrump_JoeBiden_followers_creation_date.png)

![](image/creation_date/VP_SenKamalaHarris_followers_creation_date.png)

![](image/creation_date/senatemajldr_SpeakerPelosi_followers_creation_date.png)

# Conclusions

We discovered that when Benford's Law detects anomalies in the followers data, the creation dates of the followers tend to be more recent. 

A recently created user may or may not be a bot, we don't have enough evidence to conclude one way or another, but they do raise suspicions when tested against Benford's Law.

In the previous graphs of the 4 statistics for each user that we saw, we discovered that friend counts have the closest fit to Benford's Law in every run, and it's the most unaffected when removing the counts of 1. 

So at the current stage, I think Benford's Law can tell us about anomalies in data, but not exacly why the anomalies occurred, so it's not entirely useful in bot detection in my experiment, there may be other ways to use Benford's Law that can be more effective in bot detection. 




