## Rag Triad

- faithfulness
- answer relevancy
- contexual relevancy

## Contexual Relevancy

use LLM a s a judge. Break context into claims. for each claim to check if the claim is relevant to the question. it is relevence free metric.


a retriever can give good recall and precision independently but may fail in pipeline - low contexual relevency. This may happen due to too much noise in the chunk.
 - So we can reduce chunk size.
 - try less overlapping. 
