# Findings and Lessons Learned

This document records the key observations and conclusions derived from experiments conducted as part of the **Local Agentic AI Lab** project.

The findings are based on practical experimentation with locally hosted language models in an **OpenCode + Ollama** environment. They are not intended to represent universal model rankings or benchmark results.

Findings may be updated as additional experiments are performed.

---

## Finding 1 — Tool-Like Output Is Not Tool Execution

Most of the tested models appeared capable of recognizing that the task involved a file operation.

However, several models failed at the critical transition from understanding the required action to successfully participating in OpenCode's tool-execution workflow.

Observed failure patterns included:

* Tool-call JSON generated as normal text.
* Function calls generated as plain text.
* Pseudo instructions instead of actual tool invocation.
* Code generation instead of task execution.
* Malformed function calls.
* Incorrect file paths.
* False claims of successful completion.

This revealed an important distinction:

> **Knowing what action should be performed is not the same as reliably invoking the required tool through an agent framework.**

For the primary Brain role, reliable orchestration is a mandatory requirement.

---

## Finding 2 — Context Size Can Affect Practical Agent Behaviour

The clearest evidence came from Qwen3.5:4B.

The same model failed to execute tools at **4K** but successfully completed the file-creation task at **8K**.

Qwen3:4B-Instruct also successfully demonstrated tool execution at **8K**.

Based on the current experiments:

> **Context configuration can materially affect whether a small model successfully performs tool-mediated tasks within the agent workflow.**

This finding is currently limited to the tested configurations and should not yet be generalized to every model.

---

## Finding 3 — Two Models Passed the Initial Brain Test

Among the tested models, only the following successfully completed the initial practical tool-execution test:

1. **Qwen3:4B-Instruct**
2. **Qwen3.5:4B**

Both successfully created the requested file at an **8K context configuration**.

These are currently the strongest candidates for further experimentation as the primary Brain.

However, passing a simple tool-execution test does not establish that a model is suitable for all agentic tasks.

---

## Finding 4 — Tool Execution and Long-Running Agent Behaviour Are Separate Problems

The experiments initially focused on identifying a model capable of successfully executing tools.

This problem was partially solved with Qwen3:4B-Instruct and Qwen3.5:4B at 8K.

However, continued experimentation exposed a second problem:

> **Compaction and looping during longer workflows.**

Both successful models encountered issues after the initial tool-execution stage.

This indicates that a viable primary Brain requires at least two capabilities:

1. **Reliable tool orchestration**
2. **Reliable context and state management during extended workflows**

Successfully passing the first requirement does not guarantee success on the second.

---

## Finding 5 — The Evaluation Focus Shifted From Model Selection to Context Management

The initial question was:

> **Which small local model can act as the Brain and execute OpenCode tools?**

The experiments identified two promising candidates.

The next major question became:

> **How can a local agentic workflow preserve sufficient context and task state during longer execution without entering compaction or execution loops?**

This shifted the project's focus toward investigating:

* Context compaction
* Context-window limitations
* Task-state management
* Structured summaries
* Context persistence
* Selective retrieval of relevant information
* Long-running agent workflows

---

## Current Direction

The initial model-selection phase identified **Qwen3:4B-Instruct** and **Qwen3.5:4B** as the current leading candidates for the primary Brain role based on their ability to successfully execute tools at an 8K context configuration.

The project is now moving into the next phase of experimentation:

> **Investigating how context can be managed, compacted, and preserved to support reliable long-running agentic workflows on resource-constrained local hardware.**

Future findings will be added as new experiments are completed.
