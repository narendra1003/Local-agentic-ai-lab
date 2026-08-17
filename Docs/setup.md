# Setup Documentation

This document describes the local environment and software setup used for the **Local Agentic AI Lab** project.

## Objective

The objective of this setup is to explore whether a consumer-grade computer can run useful local AI-assisted coding and agentic workflows.

The experiments focus on:

* Running language models locally
* AI-assisted coding
* Instruction following
* Tool calling
* File and code analysis
* Multi-step task execution
* Exploring agentic workflows

## Core Components

The current setup consists of:

* **OpenCode** — AI coding agent interface
* **Ollama** — Local language model runtime
* **Locally hosted language models** — Used for experimentation and task execution
* **Windows 11** — Operating system

## High-Level Architecture

```text
User Request
     |
     v
 OpenCode
     |
     v
 Ollama
     |
     v
Local Language Model
     |
     +--------------------+
     |                    |
     v                    v
Code Analysis        Tool Execution
     |                    |
     +---------+----------+
               |
               v
         Response / Output
```

## Initial Setup

### 1. Install Ollama

Ollama is used to download and run supported language models locally.

After installation, models can be pulled and made available for local inference.

### 2. Install OpenCode

OpenCode is used as the coding-agent interface for interacting with local models.

The objective is to allow the model to work with coding tasks, project files, and available tools.

### 3. Configure OpenCode

OpenCode is configured to communicate with the locally running Ollama instance.

The local provider is configured using the Ollama API endpoint.

Example architecture:

```text
OpenCode
   |
   | Local API Request
   v
Ollama Server
   |
   v
Selected Local Model
```

## Current Workflow

The initial workflow being explored is:

1. Provide a task or instruction to OpenCode.
2. OpenCode sends the request to the selected local model.
3. The model analyzes the available context.
4. OpenCode provides access to relevant tools or files when required.
5. The model generates a response or performs the requested task.

## Areas Under Investigation

The setup will continue to evolve while exploring:

* Different language models
* Context window limitations
* Tool-calling reliability
* Model specialization
* Coding capability
* Repository-level analysis
* Multi-step workflows
* Agentic workflow design

## Current Status

🚧 **Work in Progress**

The local environment has been configured and experimentation with models and workflows is ongoing.
