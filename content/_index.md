---
title: The Social Network of Hip Hop Artists
layout: single
next: data-description
---
<style>
r { color: Red }
o { color: darkorange }
g { color: Green }
</style>


# **Hip Hop** 


# **Data**
This is the data secton

# **Network analysis**
## Directed graph
To get an overview of the relationship of hip hop artists, we investigated the statistics of the network. Looking at our 
data, the natural choice at first was to explore the structure of the directed network since it was 
collected in a way where there naturally were directed edges from one artist to another. The directed edges are made 
simply by stating that; if there is a hyperlink from artist A's wiki page referring to artist B's wiki page, then 
there is a directed edge going from the node representing artist A to the node representing artist B.


## Nodes, edges and density. 
Using this practice, the artist network has 2564 nodes and 34754 edges and the density of the network, meaning the 
number of edges divided by the possible number of nodes, is 0.0053.


## Degree
We will now look at how many connections, or links in network terminology, each artist has. This is done by looking at 
each artist's node in-degrees, and out-degrees, where in-degrees are how many artists' wiki pages refer to their wiki 
page, and their out-degrees are how many artists their wiki refer to. The distribution of the in- and out-degrees for 
all artists is shown in the figure below.

<img src="images/degrees.png" width="200" height="100">

_Distribution plot of the in-degrees and out-degrees for the artists. 
It should be noted that the axes are logarithmic._

The figure above shows that the number of degrees for the artists rapidly decreases. The figure shows that just 10% 
of the artists have five or more direct links to other artists. Kanye West is highlighted as an exciting person 
since he has the most in-degrees of all the artists, meaning that he is the one being refered to the most. Note 
that the distribution is roughly linear in the log-log scale, that means that the relation follows a power law. 
The table below shows some summary statistics on the distribution.

|            | **Mean** | **Median** | **Mode** |
|------------|----------|------------|----------|
| In-degree  | 13.55    | 5          | 1        |
| Out-degree | 13.55    | 9          | 4        |

It is evident that the mean of the two distributions, of course, is the same since it must be the case that the 
number of in- and outgoing links is the same. 

Looking at the degrees of the nodes in the network can tell quite a lot about the artist's popularity in the world 
of hip hop. The graph below is a scatter plot in logarithmic scale that displays the in-degree and out-degree for 
each artist. Try hovering over the points in the graph to see their names. Do you recognize any of them, and where 
do they primarily lie in the graph?

<img src="images/degrees_line.png" width="200" height="100">

_The red line is an equal number of in- and out-degree. Artists who lie above this line have more people who have 
attributed them than they have to others. You can also change the scale from log to linear, using the buttons_

Besides being an excellent way to visualise each artist's in- and out-degrees, the scatter plot also constitutes a 
great way to see the correlation between the in-degrees and out-degrees. Here it can be seen that for the famous 
artists, there are roughly twice as many wiki pages that refer to them as their wiki pages refer to others. 
This is primarily because many smaller artists often have references to famous artists since they have been an 
inspiration or did a small collab with them. In contrast, the famous artists' association with the small artist did 
not have significant importance to be recognised as being noteworthy on the famous artists' wiki page.


## Top artists by degree
Let’s take a look at the top 10 artists with the most in- and out-degrees in the table below. | 

|In Degree        |     | Out Degree       |     |
|------------------|----:|------------------|----:|
|            Jay-Z | 315 |           Eminem | 149 |
|        Lil Wayne | 306 |       Kanye West | 134 |
|       Kanye West | 303 |   Kendrick Lamar | 122 |
|           Eminem | 300 | Drake (musician) | 118 |
|       Snoop Dogg | 281 |            Jay-Z | 116 |
|          50 Cent | 240 |             T.I. | 116 |
|              Nas | 216 |      Chris Brown | 103 |
|     Busta Rhymes | 214 |    Missy Elliott | 100 |
| Drake (musician) | 213 |        Lil Wayne |  96 |
|   Kendrick Lamar | 188 |          50 Cent |  96 |

Most of these hip-hoppers, having either won a Grammy or at least been nominated for one, and are undoubtedly 
well-known folk. As hip hop is a lot about connections and who you collaborate with, it only makes sense that 
these people at the top of the game have made many connections throughout their careers.

# Undirected
Using an undirected network also prompts merit as it allows for community detection. Here we wished to enable 
communities to be found where artists have affected each other. Therefore an undirected edge will be created 
between two artist nodes only where both artists refer to each other, i.e. the nodes are strongly connected 
components. So only if artist A’s wiki page refers to artist B’s wiki page and artist B’s wiki page refers to 
artist A’s wiki page there will be an undirected edge between the nodes representing artist A and artist B.

When doing this, the graph lost 18% of its nodes since these artist nodes were not strongly connected components 
and, therefore, not really in a community. Furthermore, doing this, the graph lost 79% of its edges. As observed 
earlier, when looking at degrees, this is primarily because many smaller artists often have references to famous 
artists since they have been an inspiration or did a small collab together. In contrast, famous artists are not 
as affected by that small interaction. Hence the small artist did not have significant importance to be recognised 
as being in the famous artist's social circle. 

This leaves the graph with the following statistics

|            | Nodes | Edges |
|------------|------:|-------|
| Directed   |  2564 | 34754 |
| Undirected |  2094 | 7363  |
| Fraction   | 0.817 | 0.212 |


## Clustering
We can use clustering analysis to determine if the hip-hoppers form local groups in the network with a higher density 
than expected. We would probably expect subgroups of the hip-hoppers to work together with the same but slightly 
different subgroups, i.e. if they work with a friend of a friend, etc. In this fashion, clusters arise in the graph.
The Local clustering coefficient is defined for each node as
$$C_i=\frac{2L_i}{k_i(k_i-1)}$$
Where $k_i$ is the number of neighbours (degree) and $L_i$ is the number of edges in relation to node $i$’s neighbours.
Taking the mean over this gives us the average clustering coefficient
$$\langle C \rangle= \frac{1}{N}\sum_{i=1}^{N}C_i$$
To compare if clusters are present, we compare it to its random graph counterpart as a null model. The random graph 
is created with the same number of nodes and edges as the original graph. Connections between the nodes are created with 
probability $p$ such that the number of edges is the same as the original graph. 
$$p=\frac{2L}{N(N-1)}$$
where L and N are the number of edges and nodes, respectively.

Based on these formulas, the average clustering coefficient for the hip-hop- and random networks are:
$$\langle C \rangle_{\text{hip-hop}} = 0.231$$
$$\langle C \rangle_{\text{random}} = 0.00429$$
Since the clustering coefficient for the hip-hop network is approximately 100x larger than the coefficient for the 
random network, we conclude that clusters are indeed present.

# Text
The text used for the text analysis is the content of each wiki page. There are 
between 239 and 110.250 words written about each artist, with the median being 4202 
words and the mean being 6944. The distribution of words is shown here:

| x                             |   x | x   |
|-------------------------------|----:|-----|
| Needs figure of distribution! |   x | x   |

This is a reasonable amount of words that can be used to analyse how the hip hop 
artists differ from each other. In this investigation, we will use term 
frequency-inverse document frequency visualised with WordClouds and some sentiment 
analysis to understand each artist better.

## Preparing the text
Before working with the text, it had to be prepared and preprocessed to become a more 
useful text that could provide better insights. Hence we made some alterations to the 
text. First, we removed all numbers, stop words and punctuation since commas, a "5", 
and non-essential words, such as "the" and "that", did not provide information about 
the intriguing life of the artists. Then we removed URLs, but not the text in the 
hyperlink. So if there were a hyperlink with the text "Tupac", the text "Tupac" would 
be saved but not the URL in the hyperlink. Then every word was set to lower case, and 
finally, the text was tokenised using `nltk. tokenise` such that words with the 
same stem were recognised as the same word

## Term Frequency–Inverse Document Frequency (TF-IDF)
The Term Frequency–Inverse Document Frequency (TF-IDF) is a fascinating numerical statistic when doing information 
retrieval of some documents. As the method's name implies, there are two main ideas behind this statistic; 
the frequency of the term in a document and how frequent documents contain the term. The equation for the 
Term Frequency (TF) has the following form:
$$\text{tf}(t,d) = \frac{f_{t,d}}{\Sigma_{t'\in d} f_{t',d}}$$
Where \\(f_{t,d}\\) is the number of times the term \\(t\\) appears in the document \((d)), hence the TF score is the 
ratio of the use of a word compared to all words in the document. 

The Inverse Document Frequency (IDF) has the equation:
$$\text{IDF}(t,d)=\log \left(\frac{N}{|\{ d\in D: t\in d\}|}\\right)$$
Where it becomes apparent, the terms which will get the highest score are the terms where only a few documents contain
that term, and the document has many instances of that term. 

Thereby this statistic can find the words that make a document (Wikipedia page) unique, and that is exactly what we 
wish to figure out. We want to find the defining words for each of our hip hop artists; the words that are unique to 
them and, therefore likely informative about their lives. 

Let us start by looking at the TF and TF-IDF scores for Drake.

|    | Word     |   TF score |
|---:|:---------|-----------:|
|  0 | drake    |  0.0424568 |
|  1 | album    |  0.012454  |
|  2 | music    |  0.0106142 |
|  3 | also     |  0.0106142 |
|  4 | released |  0.0100481 |

|    | Word    |   TF-IDF score |
|---:|:--------|---------------:|
|  0 | drake   |     0.0433637  |
|  1 | toronto |     0.00681557 |
|  2 | ovo     |     0.00437314 |
|  3 | graham  |     0.00330544 |
|  4 | hot     |     0.00316553 |

Unsurprisingly, Drake himself shows up as the top word in each case. However, the TF-score words are extremely 
irrelevant since they are just generic music terms that provide absolutely no information on him as a person. 
In contrast, the TF-IDF words are highly relevant. For example, the OVO music label which Drake owns, is shown.

Without going in-depth with them, we believe it might also be interesting to look at these hip hop artists.  
### Insert Word Clouds
### Insert Word Clouds

## Sentiment analysis
We wanted to do a sentiment analysis of the hip hop artists, but given that Wikipedia is notoriously neutral in their 
writing, the results of just doing it on all their content would be uninteresting. Instead, we thought it would be 
interesting to look at each artist's top 100 words from the TF-IDF scores. In that way, the considered words hold 
much more weight and can better describe the artist's true sentiment 
### Show sentiment figure 
### Show sentiment vs age
The figure above the sentiment on the y-axis and the age on the x-axis **this needs to be elaborated on to be included**


# Communities
Hip hop artists are of course not all alike. They rap about different topics, care about different issues and have 
different music styles. Especially music style is something that deviates in hip hop with some artists singing 
pop-rap others sing lofi-hiphop and then there are those who are gangster rappers. To investigate the structure of 
the network we created communities based on the hip-hop artists “other genres”. A lot of the artists are not only 
singing the genre hip hop, but have several other genres they perform in, which can be seen here. By using a Wikipedia 
site with lists of music genres and styles, it was possible to give each subgenre one of the 14 general genres. 

The 14 genres are:
1. Art (classical)
2. Avant-garde and experimental
3. Punk
4. Metal
5. Rock 
6. R&B and soul 
7. Pop 
8. Jazz 
9. Hip hop 
10. Contemporary folk 
11. Electronic 
12. Easy listening 
13. Country 
14. Blues
(We need to visualise this) 

Then we counted the occurrences of each sub-genre. As these artists are hip-hoppers, it was no surprise that their 
subgenres often were under the general genre of hip hop; however, we are interested in their main secondary genre. 
So the genre which got the most counts besides hip hop was then given to the artist as a new node attribute - if a tie 
occurred, they were assigned randomly. If they happened to have no genres out of the hip hop domain, they were given 
“pure hip hop” as a secondary genre, as these artists indeed were pure hip-hoppers. We will now consider that the 
artists who have the same secondary genre are in a community with each other, which we will explore shortly. 


## Modularity 
Now we will look at the modularity of the network, which determines whether there is a significant community structure 
in the social network of hip hop artists. In a random network, it can be expected that there are no local density 
fluctuations, where there are groups of nodes that have more edges between them than in other places. However, these 
local densities can definitely be expected in a real social network! This is simply due to the fact that if two people 
know each other, they are likely to know more of the same people, just as you and a close friend are more likely to 
have mutual acquaintances than you are a total stranger. The modularity is thereby a value that tells the strength of 
the community structures for the network, which then should be compared to a random configuration of the graph to 
examine whether the modularity is significant. 

Given the communities we just created using their second genres, we can now evaluate how good of a partitioning it is 
for the social network. Additionally, we will also use the Louvain algorithm, which is a modularity optimization 
algorithm that partitions the nodes in communities that are favourable for getting high modularity
### Figure of genre partitioning
### Figure of Louvain partitioning

We can measure whether the modularity when using the genre partitioning is significant by comparing it to a random 
network configuration and then simulating it 1000 times. Here we have a histogram of the results of these simulations.
### Figure of modularity simulations

The simulations show that the genre partition modularity is significantly different from the random network results.

# Tying the network and text together (might need other title) ¡NOT DONE!
What we found very interesting to do now was to combine what we found in the network analysis with the methods we used 
in the sentiment analysis. This was done by using the TF-IDF statistic for the ??(41)?? groups and compare them to 
each other and see if there were any apparent groupings and characteristics in their word clouds. 

Wordclouds for the communities found by the louvain algorithm

(This needs to be be written)...


## Network graph
<img src="images/Network_graph.png" width="200" height="100">
Their number of links determines the size of the nodes in the graph, and the secondary genre decides the colour. 
The colour order is the same as the secondary genre.

| **Subgenre**                 | **Count** |
|------------------------------|----------:|
| Country                      |         7 |
| Blues                        |       154 |
| Pure hip hop                 |      1497 |
| Rock                         |        73 |
| Metal                        |        16 |
| Avant-garde and experimental |         1 |
| Pop                          |       117 |
| Art (classical)              |         2 |
| Contemporary folk            |         2 |
| Jazz                         |        16 |
| Electronic                   |       569 |
| Punk                         |         6 |
| R&B and soul                 |       103 |

|                   Emi 1                    |                   Emi 2                    |
|:------------------------------------------:|:------------------------------------------:|
| <img src="images/Eminem.svg" width="100%"> | <img src="images/Eminem.svg" width="100%"> |
|                   Emi 3                    |                   Emi 4                    |
| <img src="images/Eminem.svg" width="100%"> | <img src="images/Eminem.svg" width="100%"> |

## Project pitch
This brief video which outlines the project
{{< youtube 412kVAbfoZg >}}