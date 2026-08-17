# Model Evaluation

This document records the evaluation of locally hosted language models for use as the primary **Brain** of an agentic AI workflow.

The evaluation focuses on practical behaviour within the **OpenCode + Ollama** environment rather than benchmark performance alone.

---

## 1. Objective

The goal of these experiments was to identify a small language model capable of acting as the main reasoning and decision-making model for a local agentic AI system.

The intended **Brain** role requires more than generating good text or code. The model must be able to:

* Understand the user's request.
* Follow multi-step instructions.
* Decide when an action or tool is required.
* Generate a valid tool call that OpenCode can execute.
* Interpret tool results.
* Continue working toward task completion.
* Maintain sufficient context during longer workflows.

The initial evaluation focused primarily on the first critical requirement:

> **Can the model reliably act as the Brain and orchestrate OpenCode tools to perform an actual task?**

---

## 2. Test Environment

The experiments were performed using:

* **Agent Interface:** OpenCode
* **Local Model Runtime:** Ollama
* **Operating System:** Windows 11
* **Hardware:** Intel Core i5 9th Generation, 16 GB DDR4 RAM, NVIDIA GTX 1650 with 4 GB VRAM

The detailed hardware configuration is available in [hardware.md](hardware.md).

---

## 3. Initial Evaluation Methodology

Each model was tested as the active primary model in OpenCode.

The initial practical test was intentionally simple:

> **Ask the model to create a `Hello World` text file on the local Desktop.**

The purpose was not to evaluate coding ability. Instead, the test evaluated whether the model could successfully participate in the OpenCode agent workflow and perform a real tool-mediated action.

### Test Process

For each model:

1. Download the model locally through Ollama.
2. Select the model as the active model in OpenCode.
3. Ask the model to create a simple `Hello World` text file on the Desktop.
4. Observe the model's response and tool-calling behaviour.
5. Verify whether the requested file was actually created.

### Success Criteria

A model was considered to pass the initial Brain test only if:

1. It understood the requested task.
2. It invoked the appropriate OpenCode tool correctly.
3. The tool was actually executed.
4. The requested file was successfully created.

The following were **not** considered successful tool execution:

* Returning a tool call as plain text.
* Generating JSON resembling a tool call without actual execution.
* Providing instructions describing how to create the file.
* Generating code to perform the task instead of invoking the tool.
* Claiming the task was complete when no file was created.
* Producing malformed tool calls.

---

## 4. Models Tested

The following models were experimentally evaluated for the primary Brain role.

| # | Model                     |                           Size | Context Tested    | Actual Brain Result                                                                                                                                                                            |
| - | ------------------------- | -----------------------------: | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | **Qwen3:4B-Instruct**     |                        ~2.5 GB | Default → **8K**  | ✅ **Passed tool execution at 8K** and successfully created files. ❌ Encountered a compaction/loop issue afterward.                                                                             |
| 2 | **Qwen3.5:4B**            | ~3.4 GB model / ~3.7 GB loaded | 4K → **8K**       | ❌ At 4K, did not execute tools. ✅ At **8K**, successfully created the file. ❌ Also encountered a compaction/loop issue afterward.                                                              |
| 3 | **Granite 4.1:3B**        |                        ~2.1 GB | Default           | ❌ Generated tool-call-like JSON as plain text; no actual tool execution or file creation occurred.                                                                                             |
| 4 | **Llama 3.2:3B / latest** |                        ~2.0 GB | Default           | ❌ Explained or provided pseudo tool instructions instead of actually executing the Write tool.                                                                                                 |
| 5 | **Granite 3.1 MoE:3B**    |                        ~2.0 GB | Default           | ❌ Produced a function/tool call as plain text; no actual execution occurred.                                                                                                                   |
| 6 | **Nemotron Mini:4B**      |                        ~2.7 GB | Default           | ❌ Claimed the task was completed, but no file was created.                                                                                                                                     |
| 7 | **Ministral-3:3B**        |                        ~3.0 GB | Default           | ❌ Explicitly stated that it could not directly interact with the local filesystem.                                                                                                             |
| 8 | **Hermes3:3B**            |                        ~2.0 GB | Default           | ❌ Produced malformed function-call text with an incorrect Linux path; no file was created.                                                                                                     |
| 9 | **Qwen2.5-Coder:3B**      |                        ~1.9 GB | Previously tested | ❌ **Not suitable as the primary Brain in current testing**: when asked to perform file operations, it tended to return code or instructions rather than reliably orchestrating OpenCode tools. |

---

## 5. Context Window Testing

Context size emerged as an important variable during the experiments.

### Qwen3:4B-Instruct

The model was initially tested using its default configuration and was subsequently tested with an **8K context window**.

At **8K**, it successfully executed OpenCode tools and created the requested files.

However, during subsequent workflow execution, the system encountered a **compaction/loop issue**.

### Qwen3.5:4B

Qwen3.5:4B was tested at both **4K and 8K**.

* **4K:** The model did not successfully execute the required tools.
* **8K:** The model successfully created the requested file.

Like Qwen3:4B-Instruct, it subsequently encountered a **compaction/loop issue** during continued workflow execution.

### Important Limitation

The context window was **not increased and tested consistently across all models**.

Only the following models were explicitly tested with an increased context configuration:

* Qwen3:4B-Instruct
* Qwen3.5:4B

Therefore, the failures of the other models represent their behaviour under the configurations actually tested.

A failure at the default context configuration should **not** be interpreted as definitive evidence that increasing the context window would not improve their tool-execution behaviour.

---

## 6. Key Findings

### Finding 1 — Tool-Like Output Is Not Tool Execution

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

### Finding 2 — Context Size Can Affect Practical Agent Behaviour

The clearest evidence came from Qwen3.5:4B.

The same model failed to execute tools at **4K** but successfully completed the file-creation task at **8K**.

Qwen3:4B-Instruct also successfully demonstrated tool execution at **8K**.

Based on the current experiments:

> **Context configuration can materially affect whether a small model successfully performs tool-mediated tasks within the agent workflow.**

This finding is currently limited to the tested configurations and should not yet be generalized to every model.

---

### Finding 3 — Two Models Passed the Initial Brain Test

Among the tested models, only the following successfully completed the initial practical tool-execution test:

1. **Qwen3:4B-Instruct**
2. **Qwen3.5:4B**

Both successfully created the requested file at an **8K context configuration**.

These are currently the strongest candidates for further experimentation as the primary Brain.

However, passing a simple tool-execution test does not establish that a model is suitable for all agentic tasks.

---

### Finding 4 — Tool Execution and Long-Running Agent Behaviour Are Separate Problems

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

### Finding 5 — The Evaluation Focus Shifted From Model Selection to Context Management

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

## 7. Current Evaluation Status

### Current Leading Candidates

| Model                 | Initial Tool Execution | Long-Running Workflow   | Current Status                                         |
| --------------------- | ---------------------- | ----------------------- | ------------------------------------------------------ |
| **Qwen3:4B-Instruct** | ✅ Passed at 8K         | ❌ Compaction/loop issue | Promising; further context-management testing required |
| **Qwen3.5:4B**        | ✅ Passed at 8K         | ❌ Compaction/loop issue | Promising; further context-management testing required |

### Other Tested Models

The remaining models did not pass the initial tool-execution test under the configurations tested.

They are not currently selected as the primary Brain candidates.

However, because most were tested only with their default context configurations, they should not be considered permanently eliminated without further targeted testing.

---

## 8. Current Conclusion

Based on the experiments completed so far:

> **Qwen3:4B-Instruct and Qwen3.5:4B are the only tested models that successfully passed the initial practical OpenCode tool-execution test when tested at an 8K context configuration.**

Both models demonstrated the ability to create the requested file through the agent workflow.

However, both subsequently encountered compaction/loop issues, meaning neither model has yet been validated as a reliable primary Brain for the intended long-running agentic AI workflow.

The current challenge is therefore no longer limited to selecting a model capable of invoking tools.

The next phase of experimentation focuses on:

> **Maintaining reliable context and task state during longer agentic workflows while working within the limitations of small, locally hosted models and consumer hardware.**

---

## 9. Next Steps

Future experiments will focus on:

* [ ] Investigating the compaction/loop issue.
* [ ] Testing context-management strategies.
* [ ] Evaluating structured task-state persistence.
* [ ] Exploring context compaction approaches.
* [ ] Testing selective context retrieval.
* [ ] Determining whether context management should be handled by the primary Brain or external workflow components.
* [ ] Testing whether increasing the context window improves tool execution for selected failed candidates.
* [ ] Re-evaluating promising models under controlled and consistent configurations.
* [ ] Testing the selected Brain model on more complex multi-step tasks.
* [ ] Evaluating whether a multi-model architecture provides advantages over a single-model Brain.
