# Experiment Log

This document records experiments performed as part of the **Local Agentic AI Lab** project.

The purpose of the experiment log is to document practical observations, failures, improvements, and conclusions while building a local AI-assisted coding workflow.

## Experiment Methodology

Each experiment should document:

* **Objective** — What is being tested?
* **Environment** — Relevant hardware and software configuration
* **Model** — Model used for the experiment
* **Task** — The task or scenario being tested
* **Expected Behaviour** — What should ideally happen?
* **Result** — What actually happened?
* **Observations** — Important behaviours, failures, or limitations
* **Conclusion** — What was learned?

---

# Experiment 001 — OpenCode and Local Model Setup

## Objective

Configure OpenCode to work with locally hosted language models through Ollama and verify that the environment can successfully process requests.

## Environment

* Operating System: Windows 11
* Model Runtime: Ollama
* AI Coding Interface: OpenCode
* Hardware: See [hardware.md](hardware.md)

## Task

Configure OpenCode to connect with Ollama and execute requests using a locally hosted language model.

## Result

The basic OpenCode and Ollama integration was successfully configured, allowing local models to be used within the OpenCode environment.

## Observations

The initial setup established a working foundation for further experimentation with:

* Different models
* Instruction following
* Tool usage
* Coding tasks
* Multi-step workflows

## Conclusion

The OpenCode and Ollama integration provides a functional environment for testing local AI-assisted coding workflows.

Further experiments will focus on evaluating model behaviour and limitations.

---

# Experiment 002 — Model Selection for Agentic Workflows

## Objective

Evaluate whether different models should be used for different tasks within the local AI workflow.

## Status

🚧 Ongoing

Models under consideration include models designed primarily for:

* General instruction following
* Reasoning
* Coding
* Tool calling

## Current Question

> Should a single model be responsible for all tasks, or can specialized models provide better results for specific stages of an agentic workflow?

## Initial Observations

Different model families may demonstrate different strengths.

For example:

* A coding-focused model may perform better when generating or modifying code.
* An instruction-focused model may perform better at interpreting user requests.
* A model with reliable tool-calling capability may be more suitable for task execution.

Further testing is required before drawing conclusions.

---

# Experiment 003 — Context Window Limitations

## Objective

Investigate the impact of context window limitations on local AI-assisted coding and agentic workflows.

## Status

🚧 Ongoing

## Problem Being Investigated

Complex coding tasks may require the model to maintain awareness of:

* The original user objective
* Previous reasoning
* Files already analyzed
* Tool outputs
* Intermediate results
* Current task progress

A limited context window may cause important information to be lost during long-running workflows.

## Current Question

> How can an agentic workflow maintain continuity when the available context window is limited?

Potential approaches being explored include:

* Context compaction
* Summarization
* Structured memory
* Task state tracking
* File-specific context retrieval

## Conclusion

This experiment is ongoing.

Context management appears to be a critical area for enabling reliable multi-step agentic workflows on smaller local models.
