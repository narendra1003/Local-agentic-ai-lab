# Model Evaluation

This document defines the approach used to evaluate local language models for AI-assisted coding and agentic workflows.

## Objective

The goal is not to determine which model is universally the best.

Instead, models are evaluated based on their suitability for specific tasks within the **Local Agentic AI Lab** workflow and their ability to operate effectively within the available hardware constraints.

## Evaluation Criteria

### 1. Instruction Following

Evaluates whether the model correctly understands and follows task requirements.

Questions considered include:

* Does the model follow multi-step instructions?
* Does it remain focused on the requested task?
* Does it introduce unnecessary actions?
* Does it correctly handle constraints?

### 2. Tool Calling

Evaluates the model's ability to interact with available tools.

Questions considered include:

* Can the model determine when a tool is required?
* Can it select an appropriate tool?
* Can it provide valid arguments?
* Can it correctly interpret tool results?

### 3. Code Understanding

Evaluates the ability to understand existing code.

Possible tasks include:

* Explaining code behaviour
* Identifying dependencies
* Following method calls
* Understanding relationships between files
* Identifying potential issues

### 4. Code Generation

Evaluates the ability to generate or modify code.

Possible considerations include:

* Correctness
* Relevance
* Ability to follow coding requirements
* Consistency with existing code

### 5. Repository-Level Analysis

Evaluates the ability to work across multiple files.

Possible tasks include:

* Identifying relevant files
* Following dependencies
* Tracing application flow
* Maintaining context across multiple files

### 6. Context Management

Evaluates how effectively the model can handle longer tasks and accumulated information.

This is particularly important for smaller local models with limited available context.

### 7. Resource Efficiency

Evaluates practical usability within the available hardware environment.

Considerations include:

* Response speed
* RAM usage
* VRAM usage
* System stability

## Model Evaluation Principle

Models should not be compared without considering their intended purpose.

For example, directly comparing a small coding-focused model with a general-purpose instruction model and declaring one universally superior may not provide meaningful results.

The evaluation focuses on identifying the most appropriate model for each task.

## Models Under Evaluation

The exact list will evolve as experimentation continues.

Models currently being explored or considered include:

* General-purpose instruction models
* Coding-focused models
* Small models optimized for local inference

Specific model names and configurations will be documented alongside experiment results.

## Evaluation Table

| Model | Primary Task | Instruction Following | Tool Calling | Code Understanding | Code Generation | Resource Efficiency | Notes |
| ----- | ------------ | --------------------- | ------------ | ------------------ | --------------- | ------------------- | ----- |
| TBD   | TBD          | TBD                   | TBD          | TBD                | TBD             | TBD                 | TBD   |

## Current Status

🚧 **Evaluation in Progress**

Results will be added based on repeatable practical experiments.
