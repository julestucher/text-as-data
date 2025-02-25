# Lost Connections and Found Communities: A Computational Look at Queer Identity and Interaction on Lex
### A Text as Data Research Blog

This blog will track the progress and exploration of a research project for DACSS 756: Text as Data.

## Blog Post 2: Feb 26th, 2024

By reverse engineering an API call from my mobile device, I successfully pulled posts, comments, user profiles, and user groups from the Lex app. I started by pulling posts from my Lex feed, ordered in reverse chronological order. The API call parameters included a location radius and a page number to pull. I pulled 250 pages of posts within a 50-mile radius, which resulted in all posts within a 50-mile radius of Amerherst, MA since March 30th, 2023. Total number of posts collected is 5,051. Each post returned an ID for the post and for the associated user. Using these ID fields and additional API functions `getUser` and `getComments`, I pulled user profiles for all users who posted (1,059 users) and all comments connected to posts (4,975 comments). Furthermore, associated with each user profile are the Lex group chats that active users belong to. The API function `groupsApi/group` retrieved data on 594 groups. Group chat logs are only visible to members, but a description and location are publically available to any user.

My main concern is not having enough data. The average number of tokens across documents in my posts corpus is about 40. I am not interested in increasing the distance radius because I believe that the app's usage varies regionally, especially between cities and more rural areas. By restricting the radius to Western MA, Southern VT, and the Hartford, CT area, I am capturing text from a somewhat local population. Expanding the radius would include Boston and/or New York, which would change the user sample and reduce the proportion of local users in the sample. I could repeat the data collection process and collect more than 250 pages of posts (i.e. more years of posts) if the amount of data is insufficient.

At this point in time, I have two main research questions:

1. What are people in the local area using the platform Lex for? What kinds of community and connections are people seeking and offering? Are users attempting to form connections (friendship, romantinc, activity-based, etc) or as a place to express themselves as individuals (i.e. posting rants, poetry, musings, etc)?

2. How do queer people use Lex to express themselves and identify online? Specifically, what identity-based language is used on the platform and how might it differ from mainstream identity-based language?

Basic summary statistics from the corpus, describing characteristics of the text. Ideas for this would include top features, document counts, or different patterns related to the metadata associated with the corpus.

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
|               nightstand |  24  |
|             summer-fling |  10  | 
 
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

## Blog Post 1: Feb 12th, 2024

Hi everyone, my name is Jules Tucher (they/them), and I'm a second-semester DACSS student. I graduated from Williams College with a degree in Math and Computer Science and an interest in applying data analysis skills to tackle social problems. I wrote an undergraduate honors thesis on Teacher-Student Race Match in California public schools, which looked at the association between school characteristics and the probability of students sharing a racial-ethnic identity with their teachers. I worked for two years as a Data Analyst at Mathematica Policy Research where I gained skills in statistical programming (R, Stata, and Python), data visualization (RShiny, Tableau), and project management. Last semester, I enjoyed working on a data engineering project about MA state election results on Question 2, which eliminates the MCAS graduation requirement for high school students, and a 602 research experiment about how factual information about gender-affirming healthcare for transgender minors impacts support for puberty blockers. I also wrote two research proposals, one for a research project looking at the association between exercise behaviors, gender-affirming care, and gender dysphoria among transmasculine individuals and an evaluation proposal for the Veritas Prep Early College gateway examination process. These projects represent my interest in K-12 education, Massachusetts policy issues, LGBT representation, and the experiences of transgender people.

I am curious about how queer and LGBT+ people use alternative online social media platforms to build connections in their local communities. What types of connections do people typically seek? What kinds of online personas/representations of themselves do queer and LGBT+ people create outside mainstream social networks like Twitter (X) and Instagram? What approaches do individuals and groups take to building community? What types of posts get the most interaction?

With permission from the app creators, I plan to pull posts and user profiles from the text-based LGBT community app Lex. The corpus will include posts and user profiles from a 50-mile radius of Amherst, MA. Posts are filtered by location (nearby radius) and age and are displayed on the app in a text-based format. The user's feed does not have an algorithm, but instead displays the filtered posts in reverse chronological order. Posts include username, a title, and a text-based content section. Users can react with emojis and comment on posts. Posts can also be tagged using Lex-provided tags, such as "Events", "New Here", "Friends", "Community", and "Missed Connections". User profiles are available by clicking on the username of a timeline post. User profile information contains a bio (name, age, pronouns, location, description, star sign), what the user is seeking (friends, dates, events, community), an "ask me about" section, an "I'd like to know" section, and a "teach me something about" section. Since there is no web version of this app nor publicly accessible APIs, I will reverse engineer the API calls that are made from my instance of the Lex app. I will use the software Fiddler Everywhere as an internet proxy to intercept API calls from the app on my mobile device. This will provide the GET request URL, parameters, and header credentials needed to recreate the API call in R. I have demoed this process but am waiting to hear back from the Lex team before I start collecting the data. Ideally, I would collect enough posts to build a substantial corpus.

This corpus will provide insight into how queer and LGBT people are self-identifying, self-disclosing, and being themselves online in their own words. As the app is location-based, the posts visible to each user reflect the posts of queer and LGBT people in their local communities, as opposed to other social media platforms whose algorithms are national or global. Users of Lex also self-identify as members of the LGBT community, which reduces the complexity of pulling data from another social media platform and having to determine which users are LGBT+ based on their profiles or post content. Text included in this corpus will not be limited to LGBT-related topics to be considered queer social media because the users are a self-selecting sample. Furthermore, since this app is relatively new (launched in 2019) and does not have a web version or public API, there is no precedent for computational social science methods applied to its data.
