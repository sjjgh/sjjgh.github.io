# Embeddings

## Graph Embedding

So how does graph embedding actually work?

The short answer is: it cannot even begin without an assumption.
And among all possible assumptions, the most widely adopted one is homophily.

Homophily assumes that nodes which are similar to each other are more likely to be connected. Importantly, this is not a statement about what a graph is, but about how we believe the graph was generated. Once we accept this assumption, the edges in the graph immediately acquire meaning: a connection becomes evidence of similarity, while the absence of a connection suggests dissimilarity.

Under this lens, graph embedding becomes straightforward. We seek a vector representation for each node such that connected node pairs are close in the embedding space, and non-connected pairs are relatively far apart. In practice, this is implemented by optimizing an objective that contrasts positive pairs (connected nodes) against negative pairs (non-connected nodes), encouraging a distance-based separation between them.

By solving this optimization problem, we do not “recover” some ground-truth features hidden inside the graph. Instead, we obtain a set of latent representations that are most consistent with the assumed generative rule—in this case, homophily. These embeddings encode the structural bias we imposed, which is precisely why they tend to perform well on downstream tasks such as classification or link prediction.

In this sense, graph embedding is less about discovering structure, and more about making an assumption explicit and operational.
## Deeper insights
The above process seems to work fine—and in practice, it indeed works remarkably well. However, relatively few discussions dig deeper into why it works, or what assumptions are quietly supporting it.

This naturally leads to a central question:

Why homophily?

The question is very natural be discussed rarely. There are so many different relationships in realworld. Why we choose similarity specifically? Why it works well? Can it goes wrong in some situations?

To answer these questions, we can discuss two closely related aspects:

1. Similarity is a broadly valid assumption across many real-world graphs.

2. The way we compute similarity is itself flexible and highly expressive.

### Homophily Is General in Real-World Graphs

One may reasonably ask: is it possible that by assuming a different rule—something other than similarity, such as repulsion or a more complex combination of mechanisms—we could obtain more powerful representations for downstream tasks?

The answer is almost certainly yes. Real-world connections are rarely governed by a single factor. Similarity is not the only force at play; complementarity, competition, hierarchy, and repulsion all appear in different contexts. Treating similarity as the sole mechanism would therefore be an oversimplification.

However, the goal of graph embedding is not to discover the exact, graph-specific rule that generates each individual network. Such a goal would be both impractical and conceptually questionable. Rules differ across graphs, and attempting to guess a “perfect” generative rule for every dataset is neither scalable nor meaningful.

Instead, what we seek is a general assumption—one that works reasonably well across many graphs and domains. From this perspective, similarity stands out. Across biology and human society, the phenomenon that similarity breeds connection has been repeatedly observed and empirically validated from many angles. While it is not universal, it is common enough to serve as a robust default assumption.

For this reason, homophily naturally emerges as a general modeling choice, and it has proven effective in a wide range of fields.

### Similarity as a universal metric

The second reason homophily works so well lies not only in the assumption itself, but in how similarity is computed.

As discussed earlier, there may be many different mechanisms governing connections. Mathematically, these mechanisms can often be described as some form of scoring function (or pseudo-metric, mathemathically) . The most well-known examples include Euclidean distance and cosine similarity, but in principle there are infinitely many such scoring function that could describe different relational mechanisms.

For example, if certain dimensions are more important than others, we might define a similarity score such as: m1=x1*y1+100x2*y2+x3y3. It doesn't have to be this form. If the relationship involves repulsive components or other mechanism across different dimensions, we might instead consider something like: m2=3*x1y1-4*x2y2+5*x3-8x1*y3. The specific form may vary, but the underlying idea is the same: different mechanisms correspond to different ways of measuring interaction.

In practice, the most commonly used similarity “metric” today is the dot product. It likely gained popularity initially due to its computational convenience. However, its importance goes far beyond efficiency. When jointly learned with model parameters, the dot product can approximate a wide range of similarity functions.

For instance, the weighted interaction in m1 can be approximated by scaling the learned representations—effectively increasing the magnitude of certain dimensions so that a simple dot product reproduces the desired behavior. More technically, it has been shown that dot-product similarity can approximate any positive-definite kernel metric under appropriate conditions (see, for example, the IJCAI 2019 paper: (https://www.ijcai.org/proceedings/2019/0699.pdf)). Dot products cannot represent all possible relations, but they are expressive enough to cover a remarkably large and useful class.

This brings us to a crucial insight.

Similarity appears special not because all relations reduce to similarity, but because similarity provides a universal computational substrate. Many relational rules—semantic, causal, or structural—can be embedded into higher-dimensional spaces where their effects are simulated through geometric proximity or alignment. This does not make those relations inherently metric; it makes them computable.

So back to our question. We choose similarity beacuse it is general enough, in the sense of both empirally observed and computational capcity. And Can it goes wrong? Of course, when other mechanism such as hierarchy or repulsion dominate and the way calculate similarity can not estimate the calculate (negative kernal metric, for example, mathematically speaking). But it is the most general choice we have. we can say:

**Similarity is not the only relation.**
**It is the language in which many relations are expressed.**

## Generalized Embedding
so this is just graph embedding. seems narrow huh? but what if I tell you the idea behind graph embedding appear more than you think? it implictly affect many famous algorithm. I am not saying they designed in this way. But they in fact, in natural conincide in the graph embedding idea. Let me make two examples, netflex collaborative filter. next, word embedding now foundation of LLM.
In fact the relations are so natural in our world and sometimes may not present as graph, we have to implict have them in mind, netflex, the relationship between product and customer is a biparte graph; in word embedding, we consider words in a senctence have strong correlation, thus a invisible edge. After knowing this, a fresh view of world appears to you.



