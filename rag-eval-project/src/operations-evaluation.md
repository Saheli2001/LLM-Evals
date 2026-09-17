## Operation Evals

3 kinds of operation evals:

1. latency
2. cost
3. reliability

it answers - " is the deployed system actually behaving well? "

We should not wait until production to discover that the RAG pipeline is too costly or too slow.

### Latency

- measure latency by p50, p95 , not just mean latency
- measure component level latency, not just end-to-end latency
- measure TTFT seperately
- watch for cold starts
- repeat runs as externel APIs are noisy
- track failures seperately from latency
- throughput and latency to be measured separately

latency = how long one request takes
throughput = how many requests the system can handle in a given amount of time.


### Improve Latency

- Reduce generator time : Using a faster model, simpler model for simpler question (routing method), ask generator to give a concise answer

- reduce input context size
- analyze retriever more (embedding , vector DB, reranker)
- use caching: embed caching, retriever caching, reranker cache, prompt-prefix cache
- infrastructre distance


### Cost

Mainly LLM and VectorDB are costly, or paid reranker.

considerations:

1. measure cost per query
2. measure input output cost seperately
3. measure cost as a distribution
4. segment cost by query type
5. set a cost budget

### Reduce cost

1. reduce retrieved context size
2. use smaller chunks or contextual compression
3. use a cheaper model
4. use caching

- API uses caching 


### Reliability

To successfully serve requests without error, timeouts, crashes or broken pipeline.

- error rate
- timeout rate
- retry rate

considerations:

1. measure overall success or error rates
2. categorize failure instead of using one generic error rate.
3. use enough samples
4. use representative requests include different kinds of samples.