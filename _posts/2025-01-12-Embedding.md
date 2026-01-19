# Embeddings

## Graph Embedding

So how does graph embedding proceed? Like we said, we first need an assumption. And the most widely used assumption is the assumption homophily. The homophily assumes node similar to each other have big chance to be connected. with this assuption we can conveniently embed a graph by looking at the pairs connected and want the vector represent them to be close where those not connected far away, in the embedding space. Formally speaking, we can minmize an objective function like d(x,y)-d (x,z) for x,y connected, x,z not connected. By sovling this optimization problem. We are able to get the most possible feature sets governed by the assumpted rule that generate the graph. And these features can be used for our downsteams tasks.

## Deeper (you could skip this if too complicatd)

The above process seems works fine and infact it does works fine. But not many people dig deeper into it and we want know the reason behind it.

two questions arise:1. why homophily 2. what is d(x,y) used in this process, and why?

The two question are actually related. first. why homophily. You might ask is there a possibility that if we assume a different rule, a measure other than similarity (repusive or other combinined verion) that brings us more powerful representation for downstream task. Most certainly! Because the real word connection are usually complex we can not believe that similarity is the only factor. First, rules differ from graphs. It is hard, and meanless to find and guess every perfect connection rule for each graph, and we want have the general rules that works well for most graph. Second, Why we choose similarity among all other rules. The main reason is that from biology and human socity, we oberserve the phnomeon that similiarity breeds connection, it is observed and proved from many aspect. So similarity naturally standout as an general assumption for graphs and it works well in most field.

And the second reason is that the way we calculate similarity is actually another form of generality, and that actually related to our second question.

Similarity appears special not because all relations reduce to similarity, but because similarity provides a universal computational substrate. Many relational rules—semantic, causal, or structural—can be embedded into higher-dimensional spaces where their effects are simulated through geometric proximity or alignment. This does not make those relations inherently metric; it makes them computable.  Similarity is not a relation; it is the language in which many relations are expressed.

## Generalized Embedding
so this is just graph embedding. seems narrow huh? but what if I tell you the idea behind graph embedding appear more than you think? it implictly affect many famous algorithm. I am not saying they designed in this way. But they in fact, in natural conincide in the graph embedding idea. Let me make two examples, netflex collaborative filter. next, word embedding now foundation of LLM.
In fact the relations are so natural in our world and sometimes may not present as graph, we have to implict have them in mind, netflex, the relationship between product and customer is a biparte graph; in word embedding, we consider words in a senctence have strong correlation, thus a invisible edge. After knowing this, a fresh view of world appears to you.



