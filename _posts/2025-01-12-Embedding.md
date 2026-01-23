# Embeddings

## Graph Embedding

Most conversations about embedding start in the middle—right at the algorithms. MDS, Laplacian eigenmaps, skip-gram losses, contrastive objectives… We debate architectures and hyperparameters as if the ground beneath them were solid and universal.

But like we discussed, embedding cannot even begin without an assumption.

People build embeddings every day, yet rarely name the assumption that makes the whole enterprise coherent. It’s like discussing interior design without ever checking whether the house stands on bedrock, sand, or a swamp.

Now look at what “graph embedding” usually does in practice. No matter the method—spectral, probabilistic, or loss-based—it tends to enforce the same geometry: connected nodes should end up close, and (implicitly) unconnected nodes should not.

This geometry is not a mathematical inevitability. It is a worldview.

That worldview is homophily: the belief that similar nodes are more likely to be connected. And here is the subtle but crucial point: homophily is not a statement about what a graph is. It is a statement about how we believe the graph was generated.

Once you accept homophily, edges immediately acquire semantic weight.
- A connection becomes evidence of similarity.
- The absence of a connection becomes evidence of dissimilarity—or at least, “less similar than those who are connected.”
Under this lens, graph embedding becomes almost obvious: find a vector for each node so that observed edges correspond to short distances, and non-edges correspond to longer distances.

Notice what we did not do. We did not “recover” hidden ground-truth attributes embedded inside the graph like fossils waiting to be excavated. Instead, we produced latent representations that are maximally consistent with a chosen generative story—in this case, homophily.

That is how embeddings work: they don’t merely compress structure; they operationalize a bias. They turn an assumption into a geometry that a classifier can exploit.

In this sense, graph embedding is less about discovering structure, and more about making an assumption explicit, then cashing it out as an optimization problem.


## Think deeper on the assumpiton
Now we know what kind of base our house of embedding was built on, but someone might ask: Why this base, is it solid?

Specifically, why we use homophily as our assumption? is it reliable? Can it goes wrong in some situations?

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



