# Text as Data: Research Blog

This blog will track the progress and exploration of a research project for DACSS 756: Text as Data.

## Blog Post 1: Feb 12th, 2024

Hi everyone, my name is Jules Tucher (they/them), and I'm a second-semester DACSS student. I graduated from Williams College with a degree in Math and Computer Science and an interest in applying data analysis skills to tackle social problems. I wrote an undergraduate honors thesis on Teacher-Student Race Match in California public schools, which looked at the association between school characteristics and the probability of students sharing a racial-ethnic identity with their teachers. I worked for two years as a Data Analyst at Mathematica Policy Research where I gained skills in statistical programming (R, Stata, and Python), data visualization (RShiny, Tableau), and project management. Last semester, I enjoyed working on a data engineering project about MA state election results on Question 2, which eliminates the MCAS graduation requirement for high school students, and a 602 research experiment about how factual information about gender-affirming healthcare for transgender minors impacts support for puberty blockers. I also wrote two research proposals, one for a research project looking at the association between exercise behaviors, gender-affirming care, and gender dysphoria among transmasculine individuals and an evaluation proposal for the Veritas Prep Early College gateway examination process. These projects represent my interest in K-12 education, Massachusetts policy issues, LGBT representation, and the experiences of transgender people.

I am curious about how queer and LGBT+ people use alternative online social media platforms to build connections in their local communities. What types of connections do people typically seek? What kinds of online personas/representations of themselves do queer and LGBT+ people create outside mainstream social networks like Twitter (X) and Instagram? What approaches do individuals and groups take to building community? What types of posts get the most interaction?

With permission from the app creators, I plan to pull posts and user profiles from the text-based LGBT community app Lex. The corpus will include posts and user profiles from a 50-mile radius of Amherst, MA. Posts are filtered by location (nearby radius) and age and are displayed on the app in a text-based format. The user's feed does not have an algorithm, but instead displays the filtered posts in reverse chronological order. Posts include username, a title, and a text-based content section. Users can react with emojis and comment on posts. Posts can also be tagged using Lex-provided tags, such as "Events", "New Here", "Friends", "Community", and "Missed Connections". User profiles are available by clicking on the username of a timeline post. User profile information contains a bio (name, age, pronouns, location, description, star sign), what the user is seeking (friends, dates, events, community), an "ask me about" section, an "I'd like to know" section, and a "teach me something about" section. Since there is no web version of this app nor publicly accessible APIs, I will reverse engineer the API calls that are made from my instance of the Lex app. I will use the software Fiddler Everywhere as an internet proxy to intercept API calls from the app on my mobile device. This will provide the GET request URL, parameters, and header credentials needed to recreate the API call in R. I have demoed this process but am waiting to hear back from the Lex team before I start collecting the data. Ideally, I would collect enough posts to build a substantial corpus.

This corpus will provide insight into how queer and LGBT people are self-identifying, self-disclosing, and being themselves online in their own words. As the app is location-based, the posts visible to each user reflect the posts of queer and LGBT people in their local communities, as opposed to other social media platforms whose algorithms are national or global. Users of Lex also self-identify as members of the LGBT community, which reduces the complexity of pulling data from another social media platform and having to determine which users are LGBT+ based on their profiles or post content. Text included in this corpus will not be limited to LGBT-related topics to be considered queer social media because the users are a self-selecting sample. Furthermore, since this app is relatively new (launched in 2019) and does not have a web version or public API, there is no precedent for computational social science methods applied to its data.
