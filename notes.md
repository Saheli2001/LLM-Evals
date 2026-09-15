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

# LLM Eval Methods

Programmatic/ Deterministic - for example, in case of a Retrieval system an eval method can be recall@k. Improvements over retrieval : Better Embedding Model, Query Expansion (by an LLM), increase k, reranking.

Human - Multiple humans carry out evaluation pipeline. For example helpfulness of a chatbot.Red training, A/B Testing, Direct grading/ rating, HITL.

LLM as a judge - Given arubric, it ranks the output of the model.

# Reference based vs Reference free Evals

# Offline Eval vs Online Eval

purposes of offline eval : pre-release testing -> a gating mechanism, if the pipeline checks certain criteria it goes to the production otherwise not, version comparison -> make two versions of the software and compare the model/ prompts keeping other things same, regression testing -> sometimes improving one component can affect other components, to test this we use regression testing. 

Post-deployment problems: 

1. unanticipated inputs (lik e half questions, mixing hindi and english)

2. Emergent/ systematic failures (huge latency for huge number of users, inherent bias towards certain users)

3. Drift (offline testing becomes obsolute, happens over the years if the software is not continously evolved)

# Online Evals

evaluating the system on live production traffice, after deployment when real users uses it. Live production dosent have a golden dataset.

Offline eval tells whether the system is correctly running and online eval tells whether the system is normally running.

correctness cannot be checked in online eval. but we can check the normalcy by checking the distribution of the evaluation whether it remains the same over time. create a baseline distribution and treat it as baseline.

Online Evaluation Pipeline:

A. Logging

1. Conversation id, turn id, user id, timestamp etc.
2. Input
3. Retrieved context
4. output
5. operational telemetry -> latency, prompt tokens, derived cost, error status etc
6. downstream user signals -> thumbs up/down, excalation to support etc.

logging should be quereble, late-signal attachment etc.

B. Observibility ( Langsmith )

create dashboard - latency over time, error rate, rephrase rate etc. Create alert setups if it crosses a particular threshold. This is for the captured logging.

For computed logs ( like faithfulness, halluciation etc)
create evaluator - sample random outputs from a huge pool of outputs and feed them into a LLM (judge) with the defined rubric and compare whether the output is some hallucination or not. judge gives a hallucination rate and put it in a dashboard, then create alerts.

Is random sampling a good strategy? 

Not all conversation are same, we divide conversation into categories and create stratified sampling. 

LANGSMITH GIVES IS A EVALUATION FRAEWORK.

The self improving loop - stores failure cases from online and makes it a part of the offline dataset ( langsmith also gives the ability of annotate failure cases)

# Model Evals

- to compare different models fairly based on the necessity
- to track whether newer odels are actually improving
- to decide the safety for release
- cost decisions

# What are model evals

every model eval should follow :

- decide what to measure
- get a test set
- run the model under a fixed protocol
- score and interpret

Test type:

- a public benchmark - helps checking specific tasks of the llm like reasoning, coding etc.
- your own evaluation set - 

# Need for an Eval Harness

we need to handle:

- Extract the answer correctly
- Scoring answers using benchmarks exact methods
- sending millions of questions efficiently in a batch
- retrying failed API requests
- Handling rate limits

library : lm-evaluation harness, Inspect, HELM