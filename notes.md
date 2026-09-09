# Why LLMs need to be evaluated

- LLMs are Probabilistic models. So, for the same input, they can produce different outputs. This means that evaluating their performance is not straightforward and requires careful consideration of various metrics and methods. (This happens because of temperature settings, random seeds, and other factors that introduce variability in the output, even for the exact same input.)

- LLMs should be checked in multiple directions. For example, factuality, tonality, latency, cost etc - depends on the use case.

Topics to Cover:

1. LLM Evals as a Concept
2. LLM Evals Landscape
3. LLM Evaluation - Benchmarks
4. LLM Application Evaluation
5. Evaluation Pipeline
6. RAG Eval
7. Agent Based Evals
8. Safety Based Evals
9. Operation Evals - latency, system load etc.

# What are LLM Evals?

LLM evals are systematic , repetative tests used to judge an LLM or its application against clear criteria.

Systematic: Create proper dataset.

Repetable: The same eval should be runnable again even if we change model, prompt, retriever etc.

Clear Criteria: Well defined criteria.

- Eval is not a metric. It's a testing setup. It a complete process that includes dataset, prompts, evaluation metrics, and analysis.

# Model Evals

capabilities to be evaluated: Reasoning, Knowledge, Coding, Maths, Instructions following, Long Context, Multimodal understanding, Tool-use

Famous benchmarks: MMLU, BIG-Bench, HELM, AGIEval, C-Eval, GSM8K, HumanEval, MBPP, CodeXGLUE, LAMBADA, SQuAD, TriviaQA

# Application Evals

Component Eval or The entire system Eval. For example, RAG eval, Agent eval, Safety eval, Latency eval etc.

# How to Evaluate LLM Applications workflow:

1. Define task and target.
2. Define success criteria.
3. Build a dataset. - golden dataset
4. Define eval method. - Automated/ LLM/ Human
5. Run model. 
6. Evaluate output.
7. Anayze results and iterate. - Identify gaps, improve prompts, improve model, retriever etc.
8. Deploy and monitor. 
9. Production failures. - imporove golden dataset using failure cases. 

- One llm application can have multiple evals. For example, RAG application can have RAG eval, Safety eval, Latency eval etc.


Consider a RAG application as an example. It can have multiple evals: Retriever eval, Generator eval etc.

For retriever eval, we can use metrics like faithfulness, Recall@k, MRR, and F1-score to assess how well the retriever retrieves relevant documents. For generator eval, we can use metrics like BLEU, ROUGE, and METEOR to evaluate the quality of generated responses.

Suppose, Retriever and Generator both works well independently. But still the the system fails. In case of priority order of fetching the documents it may happen that. So we need to make a workflow level eval tha evaluates the working of retrieval and generation together. For example, we can do reranking. Suppose we implement this eval also. Does it gurantee that the entire workflow is working fine? No. For example , latency problem which is an application level problem. 

So failure can happen is three levels - Component, Workflow and Entire Application.

# LLM Application Eval - Risk Categories

- Application quality
- Safety
- Operational (cost, latency)

# LLM Application Eval - Methods

1. Programatic/ Deterministic
2. Human
3. LLM as -judge