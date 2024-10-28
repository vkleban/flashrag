# FlashRAG

FlashRAG provides blazing-fast RAG responses by precomputing key-value caches for document chunks offline, slashing redundant computations and boosting inference speed. 

### Naïve RAG
Current Retrieval-Augmented Generation (RAG) systems retrieve documents relevant to a user’s query and concatenate them with the input context. This context is then passed to a generative model to generate the final output.

The model repeatedly computes self-attention across large concatenated texts, leading to quadratic growth in complexity. Each time similar documents are retrieved, it redundantly recalculates the key-value pairs, making the system inefficient.

It is slow, and time to first token is long.


### How FlashRAG Works?

Key-Value caches store intermediate representations of tokens used in a transformer’s self-attention mechanism. These caches include precomputed vectors (keys and values) for each token in the context. It allows to pause and resume generation.

FlashRAG computes KV-caches when new document is inserted into the database (offline). By precomputing and storing KV caches offline, FlashRAG eliminates the need to recompute these caches for every query. During inference, the model directly uses the precomputed caches, avoiding redundant work, reducing latency, and accelerating generation. 

