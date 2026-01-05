# Graph Learning Renaissance (1) - basic aggreements
After I started working more closely with machine learning, I read and reviewed many papers related to graphs.

Many of them felt a bit odd to me—not because they were wrong, but because they often focused on inventing increasingly sophisticated tricks on graphs, without clearly explaining the intuition behind them. You often see phrases like “Better neighborhood modeling,” “enhance aggregation power,” “Structure-aware representations,” or “Expressive node representations.” They sound convincing, but I often find myself wondering what they really refer to beneath the surface.

Coming from a mathematics and physics background, I tend to care more about the reasoning behind a phenomenon rather than engineering a black-box method. For me, good intuition usually starts with a more basic question: what is a graph, and how should we think about it in machine learning?

I believe that doing machine learning with graphs should begin with a clearer understanding of the nature of graphs themselves, as well as how features and embeddings associcated with them.

During the first several years of my PhD, I spent a lot of time playing with graphs and embedding methods. Along the way, I gradually formed some perspectives that I rarely saw discussed explicitly. I felt they were worth writing down—and this series of articles is an attempt to do exactly that.

## What is graph
Informally speaking, a graph is a set of nodes and edges, usually denoted as (V,E). Any structure that can be described in this way can be called a graph—for example, a social network where nodes represent people and edges represent friendships, or a brain network where nodes are cells and edges represent neural connections.

Graphs are universal, but that is not what makes them interesting. What makes graphs powerful is that they provide a very efficient abstraction for representing relationships between entities.

These relationships are rarely governed by a single factor. In a social network, friendship may form because two people share similar hobbies, attend the same classes, live nearby, or simply interact frequently. In brain networks, connections between cells are more likely shaped by complex biological rules encoded in genes. In both cases, the observed graph is the outcome of many interacting influences.

## Graphs in Machine Learning

In practice—both in real applications and in machine learning—we are often given a graph, sometimes along with node features. Consider a simple and common setup: a social network where edges indicate friendships, and each node has features such as age, gender, or occupation.

What can we say about such a graph?

The first point I want to make explicit is this:

Edge generation is driven by complex, latent, and often unidentifiable mechanisms. Most of the time, we are neither able nor trying to recover these mechanisms.

For example, in a social network, the hidden “rule” behind friendship formation might look like a messy combination of factors， which might be something like: similar hobbies + different jobs + personality match + both enjoy outreach + age difference within four years → higher chance of friendship. And even that is still an oversimplification: in reality, the process is usually probabilistic rather than deterministic, and the factors interact in complicated ways.

If our goal is to predict something like whether a person owns a cat, we don’t actually care about the true rule that generated the edges. What we care about is predictive utility. Fully recovering the real mechanism is often impossible—and even if it were possible, it might not be the most useful thing for the task.

## From Graphs to Features

Machine learning works with features, not relations.

This leads to the second key point.
Although we do not attempt to recover the true mechanisms that generate a graph, we still need a way to turn relational structure into something a learning algorithm can use.

Since the underlying rules behind a graph are usually unknown, we are forced to make assumptions about how structure relates to similarity or relevance. Under such assumptions, we can construct features from a graph—most commonly through what is broadly referred to as embedding. I will leave the details of embedding methods to a separate article.

For now, the important point is this: the vectors produced by embedding do not correspond to explicit semantic attributes like age or occupation. They are not “real” features in that sense. Instead, they are abstract representations induced by our assumptions about the graph.

In other words, an embedding is not something we discover in the data. It is something we construct—a modeling choice shaped by both the graph structure **plus the assumptions we impose on it**.

<!--
The most common and reasonable assumption is homophily, which is implicitly used in most popular graph embedding methods.

Homophily assumes that nodes with similar characteristics are more likely to be connected. In social networks, this is often a reasonable approximation: people with similar backgrounds or interests tend to form friendships.

Under this assumption, we can assign each node a vector representation such that connected nodes are close in a vector space. From a geometric point of view, vectors that are close are interpreted as being more similar. This process is known as embedding.

Importantly, these vectors do not correspond to explicit semantic features like age or occupation. Instead, they are abstract representations induced by our assumptions. In this sense, an embedding can be viewed as a measure of similarity derived from the graph structure itself.

This leads to a second agreement:

The features obtained from a graph are assumption-dependent.
They may overlap with observed features, complement them, or reveal new structure that is not directly accessible from the original data.-->
