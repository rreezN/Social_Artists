---
title: The Social Network of Hip Hop Artists
layout: single
next: data-description
---

{{< load-plotly >}}

<style>
r { color: Red }
o { color: darkorange }
g { color: Green }
</style>


_The world of music is filled with diverse people and genres. Each genre contains subcultures with its very own artists. 
Artists who speak together, perform together and create art together. They are social artists._ 

On this website, we wish to give you an insight into The Social Network of hip hop artists. This project has narrowed 
its focus on hip hop artists because they are very social in their work, doing a lot of collaborations and having 
relations with each other. As a result it is possible to demonstrate the strength of the tools in network science 
while giving the reader an i deep exposition of the complex and captivating relationships of hip hop artists. 

To accommodate the website we have created a <o> Jupiter notebook (see bottom)</o> which the technical reader might enjoy, as it contains
all the relevant analysis, which has been made in Python. In there you can find all the technical details of how 
everything has been implemented and calculated.

To get a sense of what website will offer, you can take a look at our project pitch which outlines the project
{{< youtube 412kVAbfoZg >}}

# **Hip Hop: a social-political movement** 
Hip-Hop is a music genre loved by many due to how it reflects upon some of the struggles, thoughts and circumstances that 
numerous young people are experiencing. Their ideas emerges from the state of the present and their art are fostering 
the future. With mere words and beats youth cultures are remolded, a generation's perspectives on sociopolitical matters
are recalibrated and the civilisation, our collective community, takes another small evolutionary step. As hip hop has 
such a big influence on the youth, which is equated with The Future, one must recognise that hip hop is a subject of 
interest when studying social science.  

That is why, we have chosen  to investigate the relations between the artists of hip hop using Wikipedia as a reference. 
Wikipedia is an interesting platform because it here that the common folk expound what they creditable accomplishment 
the artists have made. We can use the tools of network analysis to examine the social relationship between hip-hoppers 
in terms of raw numbers. Then we can answer questions like: who are the most central people in hip-hop? 
We hope that this website will give you a bit of insight into the hip hop music industry and the sociacl relations that 
binds it all together.

# **Data**
The data for this project was acquired by extracting information from the Wikipedia pages of a 
<a href="https://en.wikipedia.org/wiki/List_of_hip_hop_musicians" target="_blank">list of hip-hop musicians</a>.
This was done by using the
<a href="https://docs.python-requests.org/en/latest/" target="_blank">Wikipedia Python API library</a>
and by using the raw Wikipedia API and the request library. 

We went through all the subpages from the list of hop musicians to extract information about each of the artists. 
Following this procedure, we gathered data from approximately 2600 hip-hoppers. Hereof these six attributes were 
queried from the first API call:
- Title
- Content 
- Date of birth 
- Genres
- Links (URL)
- Artist links 
- Categories

The GIF below visualises where on the artists' Wikipedia pages each of these information bits were gathered.
<img src="https://i.imgur.com/35pX5is.gif" width="100%"/>


# **Network analysis**
## **Directed graph**
To get an overview of the relationship of hip hop artists, we investigated the statistics of the network. Looking at our 
data, the natural choice at first was to explore the structure of the directed network since it was 
collected in a way where there naturally were directed edges from one artist to another. The directed edges are made 
simply by stating that; if there is a hyperlink from artist A's wiki page referring to artist B's wiki page, then 
there is a directed edge going from the node representing artist A to the node representing artist B.


## **Nodes, edges and density** 
The number of nodes is equal to how many artists we 
have in our network, and the number of edges is equal to the number of connections we have between different artists.
Using the practice above, the artist network has 2564 nodes and 34754 edges and the density of the network, meaning the 
number of edges divided by the possible number of nodes, is 0.0053. 


## **Degree**
We will now look at how many connections, or links in network terminology, each artist has. This is done by looking at 
each artist's node in-degrees, and out-degrees, where in-degrees are how many artists' wiki pages refer to their wiki 
page, and their out-degrees are how many artists their wiki refer to. The distribution of the in- and out-degrees for 
all artists is shown in the figure below.

<img src="images/in_out_distribution.png" width="100%">

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


{{< plotly json="images/in_out_scatter_plotly.json" height="550px" >}}

_The red line is an equal number of in- and out-degree. Artists who lie above this line have more people who have 
attributed them than they have to others. You can also change the scale from log to linear, using the buttons_

Besides being an excellent way to visualise each artist's in- and out-degrees, the scatter plot also constitutes a 
great way to see the correlation between the in-degrees and out-degrees. Here it can be seen that for the famous 
artists, there are roughly twice as many wiki pages that refer to them as their wiki pages refer to others. 
This is primarily because many smaller artists often have references to famous artists since they have been an 
inspiration or did a small collab with them. In contrast, the famous artists' association with the small artist did 
not have significant importance to be recognised as being noteworthy on the famous artists' wiki page.


## **Top artists by degree**
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

# **Undirected**
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

## **Clustering**
To get a sense of the network we investigated the clustering of artists in groups. 
We can use clustering analysis to determine if the hip-hoppers form local groups in the network with a higher density 
than expected. We would probably expect subgroups of the hip-hoppers to work together with the same but slightly 
different subgroups, i.e. if they work with a friend of a friend, etc. In this fashion, clusters arise in the graph.
The Local clustering coefficient is defined for each node as
$$C_i=\frac{2L_i}{k_i(k_i-1)}$$
Where \\(k_{i}\\) is the number of neighbours (degree) and \\(L_{i}\\) is the number of edges in relation to node \\(i\\)’s 
neighbours. Taking the mean over this gives us the average clustering coefficient
$$\langle C \rangle= \frac{1}{N}\sum_{i=1}^{N}C_i$$
To compare if clusters are present, we compare it to its random graph counterpart as a null model. The random graph 
is created with the same number of nodes and edges as the original graph. Connections between the nodes are created with 
probability \\(p\\) such that the number of edges is the same as the original graph. 
$$p=\frac{2L}{N(N-1)}$$
where L and N are the number of edges and nodes, respectively.

Based on these formulas, the average clustering coefficient for the hip-hop- and random networks are:
$$\langle C \rangle_{\text{hip-hop}} = 0.231$$
$$\langle C \rangle_{\text{random}} = 0.00429$$
Since the clustering coefficient for the hip-hop network is approximately 100x larger than the coefficient for the 
random network, we conclude that clusters are indeed present.

This primes us to believe that we can discover interesting relations between the artists, which will be useful when
finding hip hop communities later. But first lets dive into the text analysis of the artists.  

## **Assortativity text**
The assortativity and disassortivity of a network is the tendency of a network to be divided into hubs where each of 
the hubs can be connected to each other if it is assortative. Otherwise it is the case that the hubs avoid linking to 
each other but instead link to other small degree nodes there is disatortivity.

The 
<a href="https://en.wikipedia.org/wiki/Assortativity" target="_blank">assortativity coefficient</a>.
can be calculated as
$$r=\frac{\sum_{jk}kj(e_{jk}-q_jq_k)}{\sigma^2_q}$$
where \\(r\in[-1,1]\\)); \\(q_k\\) is the distribution of the remaining degree i.e. the edges leaving the node that do not 
connect the pair, it is expressed in terms of the degree distribution $p_k$ as shown further above; \\(\sigma_q\\) is the 
distribution of \\(q_k\\); \((e_{jk}\)) is the joint probability distribution of the remaining degrees of the two vertices _j_ 
and _k_ i.e. the fraction of edges connecting nodes of degree _j_ and _k_.

For our graph we get an assortativity coefficient 
$$r=0.357$$
This means that the hip-hop network is structured in such a way that the people who are “hubs” tend to connect to each other. 
This means that for instance the popular hip-hop hoppers tend to connect with other popular hip-hoppers who are also hubs. 
In this fashion, many of the groups only have sparse connections between them through the hubs.


# **Text**
Even though the pages of Wikipedia are inherently neutral by design, it is still relevant to study how the sentiment 
and wording of some hip-hoppers relate.

The text used for the text analysis is the content of each wiki page. There are 
between 239 and 110.250 words written about each artist, with the median being 4202 
words and the mean being 6944. The distribution of words in articles is shown here:

<img src="images/distribution_document_length_before.png" width="100%">

This is a reasonable amount of words that can be used to analyse how the hip hop 
artists differ from each other. In this investigation, we will use term 
frequency-inverse document frequency visualised with WordClouds and some sentiment 
analysis to understand each artist better.

## **Preparing the text**
Before working with the text, it had to be prepared and preprocessed to become a more 
useful text that could provide better insights. Hence we made some alterations to the 
text. First, we removed all numbers, stop words and punctuation since commas, a "5", 
and non-essential words, such as "the" and "that", did not provide information about 
the intriguing life of the artists. Then we removed URLs, but not the text in the 
hyperlink. So if there were a hyperlink with the text "Tupac", the text "Tupac" would 
be saved but not the URL in the hyperlink. Then every word was set to lower case, and 
finally, the text was tokenised using `nltk. tokenise` such that words with the 
same stem were recognised as the same word.

After preparing the text the distribution of words have changed to this. 
<img src="images/distribution_document_length_after.png" width="100%">

It can be noticed that the amount of words in the articles on the x-axis has be reduced 10-fold, as it now only conatins
words which are relevant for our study. The change can be seen in the table below.

|         | Mean | Median | Maximum | Minimum |
|:--------|-----:|-------:|--------:|--------:|
| Before  | 6945 |   4202 | 110.250 |     239 |
| After   |  650 |    394 |    9993 |      21 |


## **Term Frequency–Inverse Document Frequency (TF-IDF)**
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

<table>
<tr><th>TF result</th><th>TF-IDF result</th></tr>
<tr><td>

|    | Word     | TF score |
|---:|:---------|---------:|
|  0 | drake    |   0.0425 |
|  1 | album    |   0.0125 |
|  2 | music    |   0.0106 |
|  3 | also     |   0.0106 |
|  4 | released |   0.0100 |

</td><td>

|    | Word    | TF-IDF score |
|---:|:--------|-------------:|
|  0 | drake   |       0.0434 |
|  1 | toronto |       0.0068 |
|  2 | ovo     |       0.0044 |
|  3 | graham  |       0.0033 |
|  4 | hot     |       0.0032 |

</td></tr> </table>



Unsurprisingly, Drake himself shows up as the top word in each case. However, the TF-score words are extremely 
irrelevant since they are just generic music terms that provide absolutely no information on him as a person. 
In contrast, the TF-IDF words are highly relevant. For example, the OVO music label which Drake owns, is shown.

We believe it would be interesting for the reader to look at these hip hop artists' word clouds.

|                                                                                                                                       Drake                                                                                                                                        |                                                                                                                                       Eminem                                                                                                                                       |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                                                                                <img src="images/Drake (musician).png" width="100%">                                                                                                                |                                                                                                                     <img src="images/Eminem.png" width="100%">                                                                                                                     |
| <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6DCZcSspjsKoFjzjrWoCdn?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> | <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7lQ8MOhq6IN2w8EYcFNSUk?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> |
|                                                                                                                                      Dr. Dre                                                                                                                                       |                                                                                                                                      Cardi B                                                                                                                                       |
|                                                                                                                    <img src="images/Dr. Dre.png" width="100%">                                                                                                                     |                                                                                                                    <img src="images/Cardi B.png" width="100%">                                                                                                                     |
| <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/503OTo2dSqe7qk76rgsbep?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> | <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6KBYefIoo7KydImq1uUQlL?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> |
|                                                                                                                                       Jay-Z                                                                                                                                        |                                                                                                                                     Snoop Dogg                                                                                                                                     |
|                                                                                                                     <img src="images/Jay-Z.png" width="100%">                                                                                                                      |                                                                                                                   <img src="images/Snoop Dogg.png" width="100%">                                                                                                                   |
| <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2igwFfvr1OAGX9SKDCPBwO?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> | <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/2NBQmPrOEEjA8VbeWOQGxO?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> |
|                                                                                                                                    Nicki Minaj                                                                                                                                     |                                                                                                                                   Kendrick Lamar                                                                                                                                   |
|                                                                                                                  <img src="images/Nicki Minaj.png" width="100%">                                                                                                                   |                                                                                                                 <img src="images/Kendrick Lamar.png" width="100%">                                                                                                                 |
| <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/5eqiMMbaeUZ32Q7sS00H35?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> | <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7KXjTSCq5nL1LoYtL7XAwS?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> |
|                                                                                                                                     Kanye West                                                                                                                                     |                                                                                                                                      50 Cent                                                                                                                                       |
|                                                                                                                   <img src="images/Kanye West.png" width="100%">                                                                                                                   |                                                                                                                    <img src="images/50 Cent.png" width="100%">                                                                                                                     |
| <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4EWCNWgDS8707fNSZ1oaA5?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> | <iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/7iL6o9tox1zgHpKUfh9vuC?utm_source=generator" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe> |

The word clouds above are based on the TF-IDF scores of the terms on each artist's Wikipedia page. We know that the 
TF-IDF score is used to visualise and find the unique words for each artist. 

Take, for instance, Drake. In his word cloud, we see words that specifically describe him, e.g. OVO (a record label 
founded by Drake in 2012), Canadian and Toronto, billboard, etc. All these words are related to where he is from, 
what he does, and the fact that he has won multiple billboard rewards. Words such as lawsuit are also prominent for Drake, 
relating to some of the controversies and legal issues. 

The same is evident for artists such as Kanye West, where we see Kardashian relating to his ex-wife, Rocawear for Jay-Z 
relating to a 
<a href="https://www.thesportsman.com/style/how-jay-z-built-rocawear-the-hip-hop-fashion-line-worth-more-than-half-a-billion" target="_blank">hip hop fashion line worth more than half a billion dollars</a>.
he founded. Especially interesting is Dr. Dre, an old-school hip hop producer and rapper. His word cloud is filled with 
the names of other artists such as Eminem, 50 Cent, Snoop Dogg, Ice Cube and more, where most of them relate to back 
when he produced music under the record labels Deathrow and Aftermath Entertainment etc.

## **Sentiment analysis**
We wanted to do a sentiment analysis of the hip hop artists, but given that Wikipedia is notoriously neutral in their 
writing, the results of just doing it on all their content would be uninteresting. Instead, we thought it would be 
interesting to look at each artist's top 100 words from the TF-IDF scores. In that way, the considered words hold 
much more weight and can better describe the artist's true sentiment.

{{< plotly json="images/dist_of_happiness_score.json" height="550px" >}}

It can be seen that the around the average sentiment which is due to inherently neutral. They all have a sentiment score 
above 5, which is neutral, but only slightly deviates from that. 
Nevertheless, we will now try  and look deeper at the two ends of this spectrum of sentiment and create word clouds for 2 artists.


|                   Corey Jackson                   |                   C-murder                   |
|:-------------------------------------------------:|:--------------------------------------------:|
| <img src="images/Corey_Jackson.png" width="100%"> | <img src="images/C-murder.png" width="100%"> |

In the two word clouds above, two artists who belong to the two extremes in terms of sentiment score, 
respectively. Try to see whether you can figure out which one has the most negative score. The first thing 
that comes to one's attention when looking at the word clouds is how different the words are in each word cloud. 
These words lead Corey Jackson to have a sentiment score of 6.31 and C-Murder a sentiment score of 5.16.

Corey Jackson uses words that often are categorised as inspirational, e.g. motivational, donations, thanksgiving etc., 
whereas C-Murder's word cloud includes words such as convict, trial, deadlock, death victim etc. Where one uses positively 
connotated words, the other has words used in the context of criminals.

In addition, we explored how the sentiment used to describe artists differ for atists at different ages. This can be seen
in the plot underneath. 

{{< plotly json="images/age_scatter_plotly.json" height="550px" >}}

This show that there are 0.23 pearson correlation between the sentiment and the age. That hints that there is a weak
positive correlation, where younger artists tend to be looked upon as a tad more positive. That might just be
because younger artists have not yet made the controversies that many older hip hop artist have.


# **Communities: finding relations in the network**
Hip hop artists are of course not all alike. They rap about different topics, care about different issues and have 
different music styles. Especially music style is something that deviates in hip hop with some artists singing 
pop-rap others sing lofi-hiphop and then there are those who are gangster rappers. It has already been evident that 
there are forms of clusterings between the artists from the preliminary study of the data.
To investigate the structure of the network we created communities based on the hip-hop artists “other genres”.
A lot of the artists are not only singing the genre hip hop, but have several other genres they perform in, which can be seen here. 
By using a Wikipedia site with lists of music genres and styles, it was possible to give each subgenre one of the 14 general genres. 

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

The result of this created the communities with the follow amount of members

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


## **Modularity** 
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
algorithm that partitions the nodes in communities that are favourable for getting high modularity. 

Let us take a look at the network graphs that encapsulates these communities. 

<o> Figure of genre partitioning with a modularity of 0.1379

### (To insert "iframe..." code make < > around it)
### We also need to write what the modularity is!!!! 

iframe align=middle id="serviceFrameSend" width="95%" height="700px" frameborder="0" scrolling="no" src="/network/secondary/index.html"></iframe

<o> Figure of Louvain partitioning with a modularity of 0.6008

iframe align=middle id="serviceFrameSend" width="95%" height="700px" frameborder="0" scrolling="no" src="/network/community/index.html"></iframe

The communities found by the Louvain algorithm provide a different way to partition the network compared to the 
partitioning given by the subgenres initially offered. In some ways, the community partition makes more sense, hence 
it has a higher modularity, which likely is due to that  hip hop artists tend to have relations with not only those with 
the same subgenres of music but rather those who have the same viewpoints as themselves. 
We can observe one large cluster in the middle, and there are also 
many medium-sized closeness at least groups communities halfway to the edge in the graph, which is how you might expect 
a community to arise. We will investigate these communities soon.

We can measure whether the modularity when using the genre partitioning is significant by comparing it to a random 
network configuration and then simulating it 1000 times. Here we have a histogram of the results of these simulations.

<img src="images/modularity_experiment.png" width="100%">

The simulations show that the genre partition modularity is significantly different from the random network results.
This means that there are definitely 

# **Tying the network and text together (might need other title) ¡NOT DONE!**
What we deemed very interesting to do now was to explore the communities found using the Louvain partitioning—combining 
the insights gained from the network analysis with the text analysis methods made this possible. We created a document 
for each of the 61 Louvain communities we found, prepared the text, and used TF-IDF to get their unique terms. We now 
had the most relevant and unique words for each community, so the TF-IDF word clouds gave a good impression of what the 
communities revolved around. This made it possible for us to acquaint ourselves with why the communities were assembled 
as they were and how artists formed social groups. 

Let us first look at one of the most significant communities, which we call the famous club. 

<img src="images/billboard.png" width="100%">

This community consists of  many famous artists, which can be seen in the word cloud, with artists such as Kanye "West", 
"Eminem", Kid "Cudi" and "Drake". 
It is, therefore, no coincidence that some of the words in their TF-IDF word cloud are "grammy", "billboard", 
and "awards" because these artists are often receivers and are familiar with such first-class honours. The observation 
that the famous artists form a group goes perfectly in line with what we saw with the Assortativity and Disassortativity 
investigation, where it became clear that there was a tendency toward more prominent artists working together.

Another exciting community to look at was one we classified to be the community for UK artists with African origins. 

<img src="images/UK.png" width="100%">

This community has several threads to locations in "Africa" such as "Nigeria", "Lagos and "ghana". However, we also see 
"British" tendencies with words such as "UK" and the music genre "grime" which emerged in London. Of course, what binds 
these entities together is the artist in the community. The word "KSI" refers to the British YouTuber and newly hip hop 
artist with Nigerian roots, and "Davido" is one of the biggest artists from Nigeria. Along with other artists in the 
community, "Dizzie" and. "Stormzy" sings grime music, hinting that genre has an influence; however, it does not seem 
to be the main driver.

Now it is your turn to be the social scientist! What do you think ties the artists together in the communities below?

<img src="images/korea.png" width="100%">

<img src="images/clown.png" width="100%">

# **Conclusion stuff** 

So bla bla bla 



