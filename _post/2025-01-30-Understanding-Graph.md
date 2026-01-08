# Graph Learning Renaissance (1) - basics
After I started working more closely with machine learning, I read and reviewed many papers related to graphs.

Many of them felt a bit odd to me—not because they were wrong, but because they often focused on inventing increasingly sophisticated tricks on graphs, without clearly explaining the intuition behind them. You often see phrases like “Better neighborhood modeling,” “enhance aggregation power,” “Structure-aware representations,” or “Expressive node representations.” They sound convincing, but I often find myself wondering what they really refer to beneath the surface.

Coming from a mathematics and physics background, I tend to care more about the reasoning behind a phenomenon rather than engineering a black-box method. 

I believe that doing machine learning with graphs should begin with a clearer understanding of the nature of graphs themselves, as well as how features and embeddings associcated with them.

During the first several years of my PhD, I spent a lot of time playing with graphs and embedding methods. Along the way, I gradually formed some perspectives that I rarely saw discussed explicitly. I felt they were worth writing down—and this series of articles is an attempt to do exactly that.

## What is graph
Informally speaking, a graph is a set of nodes and edges, usually denoted as (V,E). Any structure that can be described this way can be called a graph—for example, a social network where nodes represent people and edges represent friendships, or a brain network where nodes are cells and edges represent neural connections.

What makes graphs powerful is that they provide a simple and efficient abstraction for relational structure. Whenever there are objects and relationships among them, a graph offers a compact way to represent those relationships.

However, graphs do not appear out of nowhere. In most real-world settings, a graph is the result of some underlying process that determines which nodes are connected.

A common modeling assumption is that each node has certain properties, and that connections are formed according to rules—explicit or implicit—that depend on these properties. These rules give rise to the observed graph structure.

Such rules are rarely governed by a single factor. In a social network, friendships may form because people share similar hobbies, attend the same classes, live nearby, or simply interact frequently. In brain networks, connections between cells are shaped by complex biological mechanisms encoded in genes. In both cases, the observed graph reflects the combined effect of many interacting influences.

## Graphs in Machine Learning

In machine learning, a common scenario is that we are given a graph, sometimes along with node features, and asked to perform a downstream task. Consider a simple and familiar setup: a social network where edges indicate friendships, and each node comes with features such as age, gender, or occupation.

At first glance, this setup already reveals a tension. Machine learning models are designed to operate on features, while a graph encodes relations. Features can be directly fed into a model; a graph, by itself, cannot. This naturally raises a question: what information can we extract from the graph and turn into something a learning algorithm can actually use?

A straightforward intuition is to try to find out the rule that generates the edges, and then infer the hidden attributes that drive these connections. If we understood the connection rule, perhaps we could reconstruct the missing information behind the graph.

However, this intuition quickly breaks down. Edge generation is driven by complex, latent, and often unidentifiable mechanisms. Most of the time, we are neither able nor trying to recover these mechanisms. In practice, fully explaining why two nodes are connected is both infeasible and unnecessary for most predictive tasks.

For example, in a social network, the hidden “rule” behind friendship formation might look like a messy combination of factors，which might be something like: similar hobbies + different jobs + personality match + both enjoy outreach + age difference within four years → higher chance of friendship. And even that is still an oversimplification: in reality, the process is usually probabilistic rather than deterministic, and the factors interact in complicated ways.

Good thing is that we don't have to recover or infer these (in most tasks).

If our goal is to predict something like whether a person owns a cat, we don’t actually care about the true rule that generated the friendship edges (for now). What we care about is predictive utility. Fully recovering the real mechanism is often impossible—and even if it were possible, it might not be the most useful thing for the task.

## From Graphs to Features

Machine learning methods likes features, not relations. 

Graphs encode relations, while machine learning models operate on features. Without attempting to recover the true mechanisms that generate a graph, we still need a way to turn relational structure into representations that a learning algorithm can use.

Since the underlying rules behind a graph are usually complex and hard to identify, we rely on assumptions about how structure relates to similarity or relevance. Under these assumptions, we can construct node representations—typically in the form of vectors—by solving an optimization problem that enforces a simple idea: if the representation respects the assumed rule, the observed edges should become explainable. This process is commonly referred to as embedding. I will leave the details of embedding methods to a separate article.

The important point here is this: the vectors produced by the embedding process do not correspond to explicit semantic attributes like age or occupation. They are not “real” features in that sense. Instead, they are abstract representations induced by the assumptions we make about the graph.

From another perspective, these representations may still contain information related to real attributes—but in a highly entangled way. A single dimension of an embedding vector might mix factors such as age, location, or activity level, making them difficult to interpret directly. What ends up being encoded, and how, ultimately depends on the assumptions we impose and the optimization process used to enforce them.

In short, an embedding is not something we discover in the data. It is something we construct—a modeling choice shaped by both the graph structure **and the assumptions we impose on it**.

<!--
The most common and reasonable assumption is homophily, which is implicitly used in most popular graph embedding methods.

Homophily assumes that nodes with similar characteristics are more likely to be connected. In social networks, this is often a reasonable approximation: people with similar backgrounds or interests tend to form friendships.

Under this assumption, we can assign each node a vector representation such that connected nodes are close in a vector space. From a geometric point of view, vectors that are close are interpreted as being more similar. This process is known as embedding.

Importantly, these vectors do not correspond to explicit semantic features like age or occupation. Instead, they are abstract representations induced by our assumptions. In this sense, an embedding can be viewed as a measure of similarity derived from the graph structure itself.

This leads to a second agreement:

The features obtained from a graph are assumption-dependent.
They may overlap with observed features, complement them, or reveal new structure that is not directly accessible from the original data.-->
