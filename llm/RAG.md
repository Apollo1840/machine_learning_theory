# Retrieval-Augmented Generation (RAG)

refer: https://chatgpt.com/share/674895ea-f480-8009-9203-431e70a8b479

Retrieval-Augmented Generation (RAG) is an IT system architecture designed around large language models (LLMs). 
To address the issue of hallucination in LLMs, relevant background knowledge is extracted from a database and incorporated into the query in a RAG system.

Key Concepts
- **Knowledge**: A vast corpus of text (or multimodal) data.
- **Knowledge Database (KDB)**: A vector database with an approximate nearest neighbor (ANN) index for efficiently retrieving similar embedding vectors (e.g., FAISS).
  Each vector is linked to a specific document. 
  The database is constructed by splitting the knowledge into chunks and embedding them using an LLM.
- **Chunk**: The original text corresponding to an embedding vector.
- **Support Chunks**: Chunks retrieved from the KDB to support a query.

## Tech details
### Split of the corpus
- Fix length of tokens
- Fix length with overlapping.
- Semantic segmentation (How to?)

### Elevate the speed of retrieving
- Approximate Nearest Neighbor (ANN) Search
- Clustering the embedding beforehand
- Compress the embedding. (eg. PCA)

### Define the number of support chunks
- Heuristic
- Dynamic based on similarity score threshold

## Related topics

### Query Augmentation

A simple calculation of similarity between the query and embeddings may not yield high-quality support chunks.

Solutions to Improve Support Chunk Retrieval:
- **Query Professionalization**:
When users use everyday language but the KDB contains professional or technical descriptions, the query should be transformed into a more formal format and enriched with relevant terminology.

- **Query Splitting**:
For complex queries that cover multiple aspects or a chain of tasks, the query should be analyzed and split into smaller, focused sub-queries. 
  These sub-queries can be processed in parallel to retrieve more comprehensive support chunks.

- **Context Augmentation**:
For queries that depend on contextual information, the query needs to be enhanced with additional dialoge context to improve retrieval accuracy.

These solutions often require the assistance of an LLM for effective implementation.