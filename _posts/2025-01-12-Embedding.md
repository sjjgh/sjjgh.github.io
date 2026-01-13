# Embeddings

## Graph Embedding

So how does graph embedding proceed? Like we said, we first need an assumption. And the most widely used assumption is the assumption homophily. The homophily assumes node similar to each other have big chance to be connected. with this assuption we can conveniently embed a graph by minmize d(x,y) for x,y connected. By sovling this optimization problem. We are able to get the simulated features control by our assumpted rules.

## Deeper (you could skip this if too complicatd)

I dont know if the process makes sense to you but we need to go a little bit deeper to that. two questions arise:1. why homophily 2. what is d(x,y) used in this process, and why?

Similarity appears special not because all relations reduce to similarity, but because similarity provides a universal computational substrate. Many relational rules—semantic, causal, or structural—can be embedded into higher-dimensional spaces where their effects are simulated through geometric proximity or alignment. This does not make those relations inherently metric; it makes them computable.  Similarity is not a relation; it is the language in which many relations are expressed.

## Generalized Embedding
so this is just graph embedding. seems narrow huh? but what if I tell you the idea behind graph embedding appear more than you think? it implictly affect many famous algorithm. I am not saying they designed in this way. But they in fact, in natural conincide in the graph embedding idea. Let me make two examples, netflex collaborative filter. next, word embedding now foundation of LLM.
In fact the relations are so natural in our world and sometimes may not present as graph, we have to implict have them in mind, netflex, the relationship between product and customer is a biparte graph; in word embedding, we consider words in a senctence have strong correlation, thus a invisible edge. After knowing this, a fresh view of world appears to you.



