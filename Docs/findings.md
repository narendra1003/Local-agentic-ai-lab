# Findings and Lessons Learned

This document records key observations and conclusions derived from experiments in the **Local Agentic AI Lab** project.

Findings are based on practical experimentation and may change as the project evolves.

## Key Questions

The project is currently investigating:

1. Can consumer hardware support useful local AI-assisted coding workflows?
2. Which tasks can smaller local models perform reliably?
3. Should different models be specialized for different tasks?
4. How reliable is tool calling on smaller models?
5. How does context window size affect long-running workflows?
6. Can structured context management improve agent performance?

---

## Finding 001 — Local AI Workflows Are Possible on Consumer Hardware

The initial OpenCode and Ollama setup demonstrates that useful local AI experimentation can be performed without dedicated high-end AI hardware.

However, available hardware resources strongly influence:

* Model selection
* Response speed
* Context capacity
* Workflow design

### Current Conclusion

Local experimentation is practical, but workflow design must account for hardware limitations.

---

## Finding 002 — Model Selection Should Be Task-Specific

Different models may be better suited to different tasks.

A coding-focused model may not necessarily be the best model for:

* Tool calling
* General task interpretation
* Planning

Similarly, a general-purpose model may not be the most suitable model for code generation.

### Current Conclusion

Model selection should consider the specific role a model performs within the workflow rather than relying on a single universal ranking.

Further experiments are required.

---

## Finding 003 — Context Management Is a Critical Challenge

Long-running agentic tasks can accumulate substantial amounts of information.

This may include:

* User objectives
* Previous actions
* Tool outputs
* File contents
* Intermediate results
* Task progress

When the available context is limited, the workflow risks losing important information.

### Current Conclusion

Context management is likely to be a major challenge for building reliable local agentic workflows.

Potential approaches requiring further investigation include:

* Context compaction
* Structured summaries
* Persistent task state
* Selective context retrieval

---

## Findings Under Investigation

The following areas require additional experimentation:

* Reliable tool calling with small models
* Model specialization
* Multi-model workflows
* Context compaction
* Long-running task management
* Repository-level analysis

## Important Principle

This project does not treat early observations as final conclusions.

Findings will be updated or revised when new experiments provide stronger evidence.

## Current Status

🚧 **Experiments Ongoing**
