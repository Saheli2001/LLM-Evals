## Failure Cases

- missed the right contexts. - recall
- chooses right contexts. But there are noisy contexts. - precision

## Tradeoff netween recall and precision

- to increase recall we can increase k. increasing k means increasing recall. this also makes precision lower as we may bring more noisy contexts.

STEP 1: 

Golden dataset. col1: question, col2: doc/chunk ID. Creating this dataset is very tidious and lengthy process. Also, to increase recall one can improve chunking strategy and makes the golden dataset created earlier irrelevant. we again have to make a new dataset.

New type of Golden dataset: col1: question, col2: ideal answer (based on the transcript and not any other sources). - in this way the metric we use is " context recall" (DeepEval). Fro calculating precision we use LLM-as-a-judge. Each chunk, retrived by the retriever, passed into the LLM with a prompt like " Is the chunk able to answer this question " and as a output we get a yes or no. Precision also incorporates ranking of the chunks. Suppose two retriever has same precision but right chunks from retriever 1 has lower rank compared to the right chunks of retriever 2. We will definitely want retriever 1. DeepEval computes "context precision (ranking aware)"

To improve recall we can tweak chunking strategy. To improve precision we can use reranking. Also an improvement is changing embedding model, better reranker.

## Retruever Golden Dataset

- Hand Authored
- LLM assisted and Human Review
- DeepEval Synthesizer and Human Review
- Production log mining
