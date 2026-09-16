# RAG EVAL

Q: How do you evaluate a RAG App

suppose we have a rag doubt solver chatbot.

### Evaluation Strategy

1. Component Level : Each part in isolation
-- Retriever: Recall, Precision
-- Generator: Faithfulness, relevance, citation accuracy
2. Pipeline : the wired handoff (RAG triad)
-- context relevance, faithfulness, answer relevance
3. Application : the whole product
-- correctness, completeness, style, safety, operations

### Regression - an activity, not new metrics

to compare version 1 vs version 2.
- experiment tracking log (MLFlow/ Weights and Bias)
- dashboarding
- CI (github actions) - a gating mechanism (deploys when the new change is better than the previous one) (See LLMOps course)

Library: DeepEval - SOTA eval library

### Online - monitor in production

- observibility (langsmith)
- faithfulness (llm-as-judge)
- drift 

### self-improving loop





