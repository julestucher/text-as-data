# Lost Connections and Found Communities: A Computational Look at Queer Identity and Interaction on Lex in Western Massachusetts
### A Text as Data Research Blog

This blog will track the progress and exploration of a research project for DACSS 756: Text as Data.

## Blog Post 4: Apr 9th, 2025

1. A summary of your research progress, noting your research question, your dataset, and how you are addressing your question.

In my previous blog post, I summarized my second wave of data collection, as well as initial attempts at answering my first research question using LDA and Naive Bayes. My research questions for this project are:

	1. What are seeking from and offering to their queer and LGBT community on the alternative social media platform Lex?
 
 	2. What language do queer and LGBT people use to describe themselves in queer-only spaces, and does it differ from mainstream references to queer/LGBT people?

Both research questions center the data I have collected from the social media app [Lex](https://www.lex.lgbt/). The app is billed as by the queer community for the queer community to dicover events and make connections with people in their local communities. My scraped dataset includes almost 15,000 text-based posts from 3,032 users. 

To answer my first research question, I am interested in using a combination of supervized and unsupervized machine learning methods to explore tagged and latent categories in text posts. Since users have the option to add tags to their posts, a subset of the post corpus is user-labeled. By training supervized models on this labeled data, we can predict what categories of posts are most prevalent in the untagged data.

To answer my second research question, I will use text extracted from the `About Me` section of the users' profiles. I plan to use unsupervized models to review any latent categories in user self-identification. I also hope to apply word embedding models to explore semantic meaning and differences of self-identification words. 

I am also very motivated to quantify and understand what topics each user is posting about on the platform as it connects to my research project for Professor Song's Network Inference class. In that project, I am exploring the likelihood that users comment on each other's posts, and being able to classify latent topics and themes for each user could help me explore whether or not shared topic interest is a predictor for tie formation in the network.

In the two weeks since my last blog post, I have also looked for examples of research that uses text-as-data approaches to social media comments to understand best practices as well as what techniques have not yet been applied. Since there is no existing research that uses the Lex app as a source for data, I have to make connections to how researchers have used other, similar sources (tweets, YouTube comments, etc).

3. Your findings so far. What are the most compelling takeaways from your work at this point?

The metadata offers some descriptive statistics. Northampton has the highest number of users and posts. The inner quantile of users' age is 24-34. Almost all users have self-identified on their profiles that they are looking for friends and community. `Community` is the most often used post tag, followed by `friends` and `events`.

Findings from LDA. Discernable categories were associated with looking for housing, advertizing events happening, and people looking for people to meet up with and talk to. Thus far, I have only applied text methods to the post-based corpus and have not explored the comments or user profiles. In my initial blog post, I expressed interested in answering the research question: "How are local queer and LGBT people self-identifying on the alternative social media platform Lex?". I am still interested in investigating this question, so I have begun to clean and create a text corpus from the user profile data. With this data set, each document represents the text found on a user's Lex profile, subset to the relevant sections: About Me, pronouns, gender identify, sexuality, and relationship style. LDA on user data. Categories that include sexual/relationship style preferences, but also dis/ability status and hobbies.

In my last blog post, I described a supervized Naive Bayes model that predicted around 80% of posts could be appropriately tagged as `community` posts, as opposed to `dating` posts. Obviously, the `community-dating` polarity is a falsely imposed binary on the source data. However, Naive Bayes can also be fit to a multinomial categorical outcome instead of a binary outcome. So, instead of collapsing the most common tags to a community/dating binary, I split out the top 7 most common tags: community, dating, event, friends, hookup, missed-connection, and new-here. One issue with this model is that posts can have multiple tags and belong to more than one category. In my pre-processing, I let less frequent tags dictate the outcome variable (i.e. if post is tagged with community and event, the outcome variable tag would be set to event). The Naive Bayes model trained on this multinomial version of the tags variable has an accuracy of 56.1% across the 7 categories, an improvement of almost 20 points on the no-information rate of 38%. 

The below confusion rate from the Naive Bayes model shows that `community` posts are most often misclassified as `event` or `friends` posts, `dating` posts are most often misclassified as `friends` posts, and `hookup` posts are more often misclassified as `dating` or `friends` posts than correctly classied. 

I also extracted the feature estimates for all features in the Naive Bayes model. Then, row-normalized the estimates to provide a measure of which features stand out as distinct predictors of each category. Without normalization, top estimates show very commonly used words in the corpus. The top 10 row-normalized feature estimates for each of the 7 categories are displayed below (hookup excluded for profanity's sake):

| community | dating | event | friends | missed-connection | new-here |
|----------|----------|-------|--------|-------------------|----------|
|housing|date|sign|☁️|seconds|alex|
|tattoo|dates|7pm|friends|westfarms|name's|
|boxes|dating|7|gym|lantern|binge|
|resources|poly|drag|pals|foods|sims|
|wix|serious|doors|buddy|seemed|mich|
|barber|romance|18|become|didn't|latina|
|harm|fall|10forward|chess|seem|weeb|
|pca|likes|saloon|i've|y'all|✌🏻|
|roommate|relationships|masks|lonely|dark|paganism|
|recommendations|valentine's|scale|buddies|gas|martin|

Interestingly, since housing is not included as one of the top 7 tags, `housing` and `roommate` make it into the top predictors for `community`. Other top `community` feature estimates relate to mutual aid requests and resource recommendations. Top features for `dating` that are less related to the other categories are fairly straightforward, and we note relationship type (`poly`) as the top feature with a different lemma from the category word. This category reveals that the dataset may benefit from some lemmatization in the preprocessing steps. Top features that distinguish the `event` category include times and place (`10forward` and `saloon` are both references to local queer venues). Features that distinguish the `friends` tag are mostly synonymous with friends: pals, buddy, buddies. In the top `new-here` features, we get a sense of people introducing themselves, their identities, and hobbies.

4. Your plan for the final project. What remains to be done? What approach are you planning for the final project, and what issues are your most concerned about heading into the stretch run?

For the final project, I would like to present exploration of both of my research questions in a poster format. 

Structural topic modeling and clustering to find better latent categories. Since SVM can only be used to predict binary outcomes, train multiple SVM using one-hot outcomes for each of the top tags in the data.

Use of word embeddings to find similarities or relationships between identity words that users use to describe themselves. 

## Blog Post 3: Mar 26th, 2025

In my third blog post, I will address updates to my corpus, initial data cleaning steps and realizations about data limitations, and results from priliminary unsupervised and supervised learing models. As a refresher, last month I collected text-based posts from the LGBT alternative social media app Lex to explore what queer people in the local area using the platform for. My primary research question is: What kinds of community and connections are people seeking and offering on Lex?

In my previous data collection effort, I was concerned about having too little data to work with. So, I repeated my data collection methods over a longer period of time. I retained the 50-mile radius constraint, but collected as many posts as I could without receiving a refresh error. This was in total 730 pages of posts, or 14,594 total posts that date back to June 2021. Although I also collected text from comments and user profiles, for this blog post I will be focusing on the post data which makes up the bulk of the text-based content on the app.

Because my data was collected in R, the data is stored locally on my device in an RDS data file, so loading it into a new R script was trivial. I completed several data cleaning steps before attempting any analysis, but I am curious how additional pre-processing steps would improve my results. First, I filtered out posts with `type == "advertisement"` because I only want to include user-generated content in my corpus. Then, I removed common English stopwords. I have some concerns that domain-specific stopwords will later need to be removed, but for now, I am just removing common English stopwords. I also set the `remove_symbols` paramter to `True` because I noticed that emoji usage seemed quite common.

During my initial data cleaning process, I noticed many spelling inconsistencies and errors across users' posts. I have found in the past that users of Tiktok and other social media platforms have become concerned that their content will get "shadowbanned" (deprioritized and hidden from viewers by the algorithm that disseminates content) due to use of innaprorpriate language (drug references, sexual content, etc). In response, users will replace letters with numbers (i.e. w33d instead of weed) or use alternate spellings (i.e. jenohside instead of genocide). This poses a unique challenge for text-as-data analysis because these replacements are not consistent and difficult to computationally ingest. I noticed some of the posts in my dataset using these filter-avoiding spellings, but for now, alternate spellings of words or phrases will be considered as separate words in the document feature matrix.

To being exploring my data, I was curious about the topics underlying the posts in my corpus. I used the `text2vec` package to tokenize the post corpus. I then created an token iterator object to create a vocabulary. I then pruned the vocabulary to only include words that were in at least 10 documents and in no more than 5% of posts. With `n_topics` set to 10, the top 10 words in each topic are as follows:

![lda_categories](/img/lda_categories.png)

The below sample document has the following distribution of topics. We can see a throughline between the topic that includes words related to housing requests (topic 7) and the topic with the highest proportion in the sample text:

```
Putting out a feeler… If anyone is looking for a roommate starting this summer and extending until  next year, I am also looking :) Would love to find a place in the surrounding WMass area that is clean and quiet. I can tell you more about myself, just DM :)) 
```
![bar_plot](/img/lda_barplot.png)

Moving on to address my first research question, I found that a small portion of the posts in my corpus have been tagged by the user. Here is an updated table of tag counts in my updated corpus:

|                     Tag  | Freq |
|--------------------------|------|
|                community | 1199  |
|                  friends | 969  |
|                    event | 591  |
|                   hookup | 524  |
|                   dating | 505  |
|                  new-here | 418  |
|                   missed-connection | 395  |
|                      random | 393  |
|                 iso | 356  |
|                     t4t | 326  |
				
I noted that of the top 5 most prevalent tags, there are two primary categories: dating and community. Because the text-based app is billed as an app for queer people to make connections, we expect to see users interested in both romantic- and community-oriented types of connections. Since only 32% of posts are tagged, this does not help us answer questions about usage overall. However, if we train a supervised learning model on the user-tagged data, we could apply this model to the untagged data and get a sense of trends across the entire corpus, as well as words that are commonly associated with community and dating on the app. 

Since the supervised learning models we have explored so far require a binary outcome, I recategorized the top 5 tags into either community (community, friends, event) or dating (dating, hookups). Posts tagged with any other tags or not tagged at all were pulled out as hold out data. This left 2,603 posts to create our training and test splits. Because community-based posts are overrepresented in the corpus, I created a test set by undersampling the community posts and oversampling the dating posts with replacement. Finally, I fit a Naive Bayes model to the training data to estimate the new tag variable ("theme"). The `summary` command provided 50% probability for the class priors, as well as estimated feature scores for features in the first two posts:

![nb_model](/img/naive_bayes_model.png)

I noted that some features were scored much higher in community posts--small, anyone, and friends-- while other features scored much higher in dating posts--someone, likes, and wanna. I used the test set of user-tagged posts to create a confusion matrix and assess how well the model would perform on unseen data.

![conf_matrix](/img/nb_conf_matrix.png)

First note the class imbalance in the test set, where community posts are much more prevalent. However, the model correctly classifies 93% of posts, with a no information rate of 85%. Overall, this model performs okay, although it does not include the complexities of topics covered in user posts. It performs well enough that I was interested to see how it would handle the hold out data. Of 11,971 untagged posts, the Naive Bayes model predicted 80.4% of them were community posts, which is 4 percentage points higher than the labeled sample. This makes sense because the mean predicted probability of community posts was 84.7%, meaning that the model will much more often predict that a post is community-based than dating, which is consistent with base sample probabilities. I would be curious better ways to evaluate the model's performance on the hold out data.

In the next steps, I would like to return to unsupervised clustering methods and see if I can get a model to converge. I would also be interested in exploring structural topic models to see if there are better topics present in the data. It may also be prudent to return to the data cleaning steps and eliminate additional stop words or experiment with n-grams, as there are many small words in the corpus that may be part of significant phrases of interest. Finally, to continue using supervised learning strategies, it would be useful to fit a multinomial model that could capture more than two post categories to include people looking for resources/support, using the app for self-expression, and whatever other use cases.

## Blog Post 2: Feb 26th, 2025

By reverse engineering an API call from my mobile device, I successfully pulled posts, comments, user profiles, and user groups from the Lex app. I started by pulling posts from my Lex feed, ordered in reverse chronological order. The API call parameters included a location radius and a page number to pull. I pulled 250 pages of posts within a 50-mile radius, which resulted in all posts within a 50-mile radius of Amherst, MA since March 30th, 2023. Total number of posts collected is 5,051. Each post returned an ID for the post and for the associated user. Using these ID fields and additional API functions `getUser` and `getComments`, I pulled user profiles for all users who posted (1,059 users) and all comments connected to posts (4,975 comments). Furthermore, associated with each user profile are the Lex group chats that active users belong to. The API function `groupsApi/group` retrieved data on 594 groups. Group chat logs are only visible to members, but a description and location are publically available to any user.

My main concern is not having enough data. The average number of tokens across documents in my posts corpus is about 40. I am not interested in increasing the distance radius because I believe that the app's usage varies regionally, especially between cities and more rural areas. By restricting the radius to Western MA, Southern VT, and the Hartford, CT area, I am capturing text from a somewhat local population. Expanding the radius would include Boston and/or New York, which would change the user sample and reduce the proportion of local users in the sample. I could repeat the data collection process and collect more than 250 pages of posts (i.e. more years of posts) if the amount of data is insufficient.

At this point in time, I have two main research questions:

1. What are people in the local area using the platform Lex for? What kinds of community and connections are people seeking and offering? Are users attempting to form connections (seeking friendship, romantinc, activities/events, etc) or just expressing themselves as individuals (i.e. posting rants, poetry, musings, etc)?

2. How do queer people use Lex to express themselves and identify online? Specifically, what identity-based language is used on the platform and how might it differ from mainstream identity-based language?

A brief exploration of the main post metadata attributes reveals the following distribution of post type. Notably, only the first two pages of posts returned any advertisements, which is consistent with the in-app experience (after about 50 posts, ads disappear).

|     Category | Freq |
|--------------|------|
| advertisement| 21   |
|group-promotion | 65 |
| missedConnection | 125 |
| personal | 4840 |

Furthermore, about half of the posts in the dataset are tagged with official Lex tags, which appear with the following frequency:

|                     Tag  | Freq |
|--------------------------|------|
|                community | 720  |
|                  friends | 444  |
|                    event | 385  |
|                   hookup | 296  |
|                   dating | 252  |
|                      iso | 241  |
|                   random | 176  |
|                      t4t | 166  |
|                 new-here | 148  |
|                     vent | 144  |
|                   advice | 141  |
|        missed-connection | 125  |
|                      art | 100  |
|                    music | 92   |
|                  housing |  90  |
|                    group |  65  |
|           lex-after-dark |  58  |
|                 for-free |  53  |
|              pride-plans |  44  |
|                hot-takes |  41  |
|                    bipoc |  24  |
 
Finally, users posted from the following nearby locations, with Northampton as the most common location:

| Location | Freq |
|----------|------|
|Northampton, MA|	1394	|		
|Amherst, MA|	552			|
|Easthampton, MA|	405	|		
|Holyoke, MA|	383			|
|Greenfield, MA|	367	|		
|Springfield, MA|	248		|	
|Montague, MA|	152			|
|Belchertown, MA|	118		|	
|South Hadley, MA|	116		|	
|Chicopee, MA|	108	|

After removing common English stop words and punctuation, the top 20 features of the post corpus are as follows.

```
looking   queer    just  anyone    like     can    want     get    know    need    love     new  people 
    849     812     748     744     736     698     665     615    527     518     498     494     452 
friends   trans      go    make someone    time    come 
    436     410     399     394     380     360     359
```

The top 50 most frequent words in the posts corpus can also be visualized in a word cloud.
![word cloud](/img/worldcloud1.png)

I also created a smalled document feature matrix that included only the 30 most frequnetly occurring words to create a feature co-occurence matrix. Below is the resulting textplot network of this 30-element feature network.
![word cloud](/img/fcm_network.png)

## Blog Post 1: Feb 12th, 2025

Hi everyone, my name is Jules Tucher (they/them), and I'm a second-semester DACSS student. I graduated from Williams College with a degree in Math and Computer Science and an interest in applying data analysis skills to tackle social problems. I wrote an undergraduate honors thesis on Teacher-Student Race Match in California public schools, which looked at the association between school characteristics and the probability of students sharing a racial-ethnic identity with their teachers. I worked for two years as a Data Analyst at Mathematica Policy Research where I gained skills in statistical programming (R, Stata, and Python), data visualization (RShiny, Tableau), and project management. Last semester, I enjoyed working on a data engineering project about MA state election results on Question 2, which eliminates the MCAS graduation requirement for high school students, and a 602 research experiment about how factual information about gender-affirming healthcare for transgender minors impacts support for puberty blockers. I also wrote two research proposals, one for a research project looking at the association between exercise behaviors, gender-affirming care, and gender dysphoria among transmasculine individuals and an evaluation proposal for the Veritas Prep Early College gateway examination process. These projects represent my interest in K-12 education, Massachusetts policy issues, LGBT representation, and the experiences of transgender people.

I am curious about how queer and LGBT+ people use alternative online social media platforms to build connections in their local communities. What types of connections do people typically seek? What kinds of online personas/representations of themselves do queer and LGBT+ people create outside mainstream social networks like Twitter (X) and Instagram? What approaches do individuals and groups take to building community? What types of posts get the most interaction?

With permission from the app creators, I plan to pull posts and user profiles from the text-based LGBT community app Lex. The corpus will include posts and user profiles from a 50-mile radius of Amherst, MA. Posts are filtered by location (nearby radius) and age and are displayed on the app in a text-based format. The user's feed does not have an algorithm, but instead displays the filtered posts in reverse chronological order. Posts include username, a title, and a text-based content section. Users can react with emojis and comment on posts. Posts can also be tagged using Lex-provided tags, such as "Events", "New Here", "Friends", "Community", and "Missed Connections". User profiles are available by clicking on the username of a timeline post. User profile information contains a bio (name, age, pronouns, location, description, star sign), what the user is seeking (friends, dates, events, community), an "ask me about" section, an "I'd like to know" section, and a "teach me something about" section. Since there is no web version of this app nor publicly accessible APIs, I will reverse engineer the API calls that are made from my instance of the Lex app. I will use the software Fiddler Everywhere as an internet proxy to intercept API calls from the app on my mobile device. This will provide the GET request URL, parameters, and header credentials needed to recreate the API call in R. I have demoed this process but am waiting to hear back from the Lex team before I start collecting the data. Ideally, I would collect enough posts to build a substantial corpus.

This corpus will provide insight into how queer and LGBT people are self-identifying, self-disclosing, and being themselves online in their own words. As the app is location-based, the posts visible to each user reflect the posts of queer and LGBT people in their local communities, as opposed to other social media platforms whose algorithms are national or global. Users of Lex also self-identify as members of the LGBT community, which reduces the complexity of pulling data from another social media platform and having to determine which users are LGBT+ based on their profiles or post content. Text included in this corpus will not be limited to LGBT-related topics to be considered queer social media because the users are a self-selecting sample. Furthermore, since this app is relatively new (launched in 2019) and does not have a web version or public API, there is no precedent for computational social science methods applied to its data.
