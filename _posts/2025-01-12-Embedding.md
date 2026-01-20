# Embeddings

## Graph Embedding

So how does graph embedding actually work?

The short answer is: it cannot even begin without an assumption.
And among all possible assumptions, the most widely adopted one is homophily.

Homophily assumes that nodes which are similar to each other are more likely to be connected. Importantly, this is not a statement about what a graph is, but about how we believe the graph was generated. Once we accept this assumption, the edges in the graph immediately acquire meaning: a connection becomes evidence of similarity, while the absence of a connection suggests dissimilarity.

Under this lens, graph embedding becomes straightforward. We seek a vector representation for each node such that connected node pairs are close in the embedding space, and non-connected pairs are relatively far apart. In practice, this is implemented by optimizing an objective that contrasts positive pairs (connected nodes) against negative pairs (non-connected nodes), encouraging a distance-based separation between them.

By solving this optimization problem, we do not “recover” some ground-truth features hidden inside the graph. Instead, we obtain a set of latent representations that are most consistent with the assumed generative rule—in this case, homophily. These embeddings encode the structural bias we imposed, which is precisely why they tend to perform well on downstream tasks such as classification or link prediction.

In this sense, graph embedding is less about discovering structure, and more about making an assumption explicit and operational.
## Deeper

The above process seems works fine and infact it does works fine. But not many people dig deeper into it and we want know the reason behind it.

A question arise:1. why homophily? These can be broke down to two part: 1. the motivation. 2. the deeper mathematical tool.

first. why homophily. You might ask is there a possibility that if we assume a different rule, a measure other than similarity (repusive or other combinined verion) that brings us more powerful representation for downstream task. Most certainly! Because the real word connection are usually complex we can not believe that similarity is the only factor. First, rules differ from graphs. It is hard, and meanless to find and guess every perfect connection rule for each graph, and we want have the general rules that works well for most graph. Second, Why we choose similarity among all other rules. The main reason is that from biology and human socity, we oberserve the phnomeon that similiarity breeds connection, it is observed and proved from many aspect. So similarity naturally standout as an general assumption for graphs and it works well in most field.

And the second reason is that the way we calculate similarity is actually another form of generality, and that actually about how we calculate the similarity. like we said, their could be many other mechanism control the rule, and mathemathically, we could describe each mechanism as a kind of psedo-metric. The most well known is euclidean and cosine metric. And there are infinitely many psedo-metric that might descirbe the mechanism. For example, if some dimension is more important than other dimension, we can have m1=x1*y1+100x2*y2+x3y3
if our feature contain repusive force of some dimension and some other dimension, additive, the psedo-metric can be something like m2=3*x1y1-4*x2y2+5*(x3+y3). These can all be pseduo metric, and the import thing is, most these metrics can be converted. For example, we can approximate m1 by letting the learned x2 and y2 increse by 10 times using a dot product. More importantly, since we mostly using dot product for similarity calcuation, not only because it is convenient to compute,and And the amazing part of dot product is that it can estimate any positive kernel metric(see this paper https://www.ijcai.org/proceedings/2019/0699.pdf).

Similarity appears special not because all relations reduce to similarity, but because similarity provides a universal computational substrate. Many relational rules—semantic, causal, or structural—can be embedded into higher-dimensional spaces where their effects are simulated through geometric proximity or alignment. This does not make those relations inherently metric; it makes them computable.  Similarity is not a relation; it is the language in which many relations are expressed.

## Generalized Embedding
so this is just graph embedding. seems narrow huh? but what if I tell you the idea behind graph embedding appear more than you think? it implictly affect many famous algorithm. I am not saying they designed in this way. But they in fact, in natural conincide in the graph embedding idea. Let me make two examples, netflex collaborative filter. next, word embedding now foundation of LLM.
In fact the relations are so natural in our world and sometimes may not present as graph, we have to implict have them in mind, netflex, the relationship between product and customer is a biparte graph; in word embedding, we consider words in a senctence have strong correlation, thus a invisible edge. After knowing this, a fresh view of world appears to you.



