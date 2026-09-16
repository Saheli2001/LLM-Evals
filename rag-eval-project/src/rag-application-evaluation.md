## Application Eval

Sometimes instead of Count based approach we need Judgement based approach. For example checking style of answer. Judgement of either huan or llm.

In case of llm as judge, llm scores can have high variance for a particular query only, llm is probabilistic. So this approach is not very reliable.

To solve this problem, we use G-Eval. (read paper)

### G-Eval

specify the metric + criteria -> Lock the evaluation steps (fixed rubric, same for evry run) -> Make a system prompt -> Probability weighted score (corresponding log (normalized probability) as weight to top k output tokens, here, scores, and take weighted average) -> Normalize, threshold and explain

G-Eval innovates:
1. Chain of Thought criteria
2. Weighted probability score

from deepeval.metrics import GEval


### 1. Quality


### 2. Completeness


### 3. Style