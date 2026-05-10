# BeyondUncertainty
Beyond Self‑Knowledge: Propagating Uncertainty Across Reasoning and Retrieval in LLMs

Research objectives and questions

This project investigates how uncertainty propagates across reasoning steps and influences retrieval decisions in large language model (LLM)‑based question‑answering (QA) systems. Building on recent work on adaptive retrieval and uncertainty propagation, we aim to address three research questions:

RQ1 – correlation between reasoning‑step uncertainty and retrieval decisions: How does uncertainty measured at individual reasoning steps relate to retrieval actions? Adaptive retrieval methods seek to retrieve external knowledge only when the model lacks information. We will measure step‑level uncertainty for each reasoning step and analyze how high‑uncertainty steps correlate with retrieval calls.
RQ2 – impact on efficiency and QA performance: What is the impact of uncertainty propagation on QA accuracy, efficiency and retrieval usage? Prior work evaluated adaptive retrieval methods using metrics such as In‑Accuracy, EM, F1, retriever calls and LLM calls. We will assess whether propagating uncertainty across reasoning steps can reduce the number of retrieval and LLM calls while maintaining or improving QA performance.
RQ3 – adaptive decision‑making strategies: Can step‑level uncertainty propagation enable strategies such as dynamic retrieval triggering, early stopping of reasoning or answer abstention? We will explore whether propagated uncertainty can be used to decide when to retrieve external knowledge, when to halt reasoning and when to abstain from answering.
