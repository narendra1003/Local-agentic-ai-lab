# Hardware Environment

This document describes the hardware environment used for experiments in the **Local Agentic AI Lab** project.

## System Configuration

| Component        | Specification                 |
| ---------------- | ----------------------------- |
| CPU              | Intel Core i5, 9th Generation |
| RAM              | 16 GB DDR4                    |
| GPU              | NVIDIA GeForce GTX 1650       |
| VRAM             | 4 GB                          |
| Operating System | Windows 11                    |

## Why Hardware Matters

Running Large Language Models locally requires balancing model capability against available hardware resources.

The available hardware directly affects:

* Which models can run locally
* Model size and quantization
* Available context length
* Inference speed
* RAM usage
* VRAM usage
* Ability to run multiple models simultaneously

This project focuses on understanding these trade-offs rather than simply selecting the largest available model.

## Primary Constraints

### Limited GPU VRAM

The NVIDIA GTX 1650 provides 4 GB of VRAM.

This limits the size of models that can be fully offloaded to the GPU and may require partial GPU acceleration or CPU-based inference.

### System Memory

The system has 16 GB of RAM.

RAM availability affects:

* The size of models that can run
* Context processing
* Multiple concurrent applications
* Ability to experiment with larger models

### Consumer Hardware

The system is not designed as a dedicated AI workstation.

Therefore, experiments focus on finding practical and usable workflows within realistic resource constraints.

## Experimentation Philosophy

The objective is not to identify the most powerful language model in general.

Instead, the project investigates the following question:

> Which combination of model size, capability, configuration, and workflow provides the most useful results on the available hardware?

For example, a smaller model may be preferable if it:

* Responds faster
* Uses fewer resources
* Reliably follows instructions
* Performs a specialized task effectively

A larger model may provide stronger reasoning or coding capability but may be impractical if it significantly impacts system performance.

## Hardware-Aware Evaluation

Models and workflows are evaluated with consideration for:

* Practical inference speed
* Memory requirements
* Stability
* Task completion reliability
* Capability for the intended task

## Current Status

Hardware testing and optimization are ongoing.
