## Experiment: Effect of `max_length` and `stride`

In this experiment, we vary the `stride` parameter while keeping `max_length = 4`.

### Configuration 1
- max_length = 4
- stride = 4
- No overlap between windows
- Number of samples: (see output above)

Here, each window starts exactly where the previous one ends.  
The dataset is split into independent chunks with no shared context.

### Configuration 2
- max_length = 4
- stride = 2
- Overlapping windows
- Number of samples: (see output above)

Here, each new window shares part of the context with the previous one.

---

## Why Does the Number of Samples Change?

The approximate number of samples is:

\[
\frac{N - max\_length}{stride}
\]

Where:
- N = total number of tokens
- stride = how many positions we move forward each step

When we reduce `stride`, we move forward fewer tokens each time.  
This generates more overlapping windows, which increases the number of samples.

---

## Why Is Overlap Useful in LLM Training?

1. **Improves semantic continuity**  
   The model sees transitions between adjacent segments of text.

2. **Increases effective training data**  
   More training examples are generated from the same corpus.

3. **Reduces artificial text boundaries**  
   Without overlap, sentences may be cut at unnatural positions.

4. **Strengthens local dependency learning**  
   Nearby token relationships are reinforced across multiple training examples.

There is a tradeoff: smaller stride increases computational cost but improves contextual learning.

---

## Why Do Embeddings Encode Meaning, and How Are They Related to Neural Network Concepts?

Embeddings encode meaning because they are learned representations optimized through training.

An embedding layer is essentially a trainable matrix of size:

\[
(vocab\_size \times embedding\_dim)
\]

Each token corresponds to one row of this matrix.

During training:

- The model predicts the next token in context.
- Backpropagation updates embedding vectors to reduce prediction error.
- Tokens that appear in similar contexts receive similar gradient updates.
- Over time, this pushes semantically related tokens closer together in vector space.

This process is grounded in the **distributional hypothesis**:
> Words that appear in similar contexts tend to have similar meanings.

### Relation to Neural Network Concepts

Embeddings are directly connected to core neural network principles:

1. **They are trainable parameters**  
   The embedding matrix is optimized via gradient descent.

2. **They perform a learned projection**  
   They map discrete token IDs into a continuous vector space \( \mathbb{R}^d \).

3. **They act like a linear layer (lookup table)**  
   Selecting a token is equivalent to selecting a row of a weight matrix.

4. **Meaning emerges geometrically**  
   Semantic similarity corresponds to geometric proximity in vector space.
   Distance metrics (cosine similarity, dot product) measure semantic closeness.

5. **They enable generalization**  
   Continuous representations allow the model to interpolate between concepts rather than treating tokens as unrelated symbols.

---

## Final Insight

Embeddings transform symbolic language into structured numerical space.

Meaning is not explicitly programmed, it emerges from optimization.  
The geometry of the embedding space reflects semantic structure because the network is trained to model linguistic patterns.

Without embeddings, LLMs would not be able to reason, generalize, or capture semantic relationships.