## Safety Failures

- Sensitive information Leakage
- Scope/ Policy Violation
- Harmful/ Toxic output
- Misinformation/ Hallucination
- Bias/ Unfairness
- Unsafe Actions

## Failure Mode Categories

- Non-adversial failure
- Adversially induced failure

 1. Prompt manipulation attacks
 2. Poisining attacks
 3. Model/ Privacy inference attacks
 4. Agent/ Tool Exploitation Attacks
 5. Resource Exhaustion Attacks

## Solve

 1. Evaluation - find failures
 2. Gaurdrails - add protection

- prompt gaurdrails
- input gaurdrails
- output gaurdrails
- retriever gaurdrails
- tool gaurdsrails
- hitl gaurdrails
- operational gaurdrails : rate limits, timeout limits, maximum agent steps

## Create safety policy

Once attack surface for the problem is defined, we define safety policy.


deepeval.safety -> toxicity

To improve toxicity score:

1. use better model
2. better system prompt
3. input gaurdrails - filter before input
4. systematic finetune the llm

## Improve Leakage

- better prompt
- dont inject context normally in prompt.. identify it as context.