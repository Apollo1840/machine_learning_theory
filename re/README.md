# Recommendation Engine
The task of Recommendation Engine(RE) is to finding finding most preferable information from a large collection of data.

P.S. It is very similar to the concept of "Retrieval" (see `retrieval.md`).

- Content-based Filtering (recommend similar items)
- (UI) Collaborative Filtering
- (UI) Matrix Factorization
- Reinforcement learning
(UI: user-item matrix)
  
## Prerequisites

### User-iterm matrix

| User ID | Movie A | Movie B | Movie C | Movie D | Movie E |
|---------|--------|--------|--------|--------|--------|
| 1       | 5      | 3      | 0      | 1      | 4      |
| 2       | **---**      | 0      | 5      | 2      | 0      |
| 3       | 0      | 2      | **---**      | 5      | **---**      |
| 4       | 2      | 5      | 0      | 3      | 1      |
| 5       | **---**      | 0      | 4      | **---**      | **---**      |

Values are ratings given by users to items (on a scale of 0-5).

## Category of methods

- Traditional
    - Content-based filtering(CBF)： Focus on **feature** extraction of items.
    - Collaborative filtering(CF): Based on UI matrix. 
        - Item-based CF
        - User-based CF
        - Matrix Factorization
- Deep learning based
    - Rating/CTR prediction
    - Ranking (in-direct rating prediction) 
    - Sequential motion prediction
    - Graph-based recommendation(Social, related items).
    

## Deep learning RE

- Neural Collaborative Filtering
- AutoRec Collaborative Filtering
- Sequential Recommendation
- DeepFM
- DIN, DIEN
