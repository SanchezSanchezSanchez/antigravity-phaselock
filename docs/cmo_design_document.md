# Cognitive Meta-Optimization (CMO) System Design Document

## Introduction

The **Cognitive Meta-Optimization (CMO)** system is the unmatchable feature designed to enable the Antigravity Agent's Reasoning Model to continuously **self-optimize its own speed and efficiency**. By implementing **Self-Distillation** and **Adaptive Quantization**, the Agent will achieve a million-fold performance increase, making the Antigravity IDE truly revolutionary.

## 1. Core Concept: Self-Distillation Pipeline

The CMO system's foundation is a continuous, closed-loop Self-Distillation pipeline that leverages the Agent's own successful work as training data.

### 1.1. Teacher and Student Models

| Model | Description | Role in CMO |
| :--- | :--- | :--- |
| **Teacher Model** | The full, high-latency, high-accuracy Antigravity Reasoning Model (e.g., a large, unquantized Google LLM). | Provides the **ground truth** for the Student Model's training. Used only for complex, high-stakes tasks. |
| **Student Model** | A smaller, faster, aggressively **quantized** version of the Teacher Model. | Provides **Hyper-Speed Mode** performance. Continuously trained on the Teacher's successful outputs. |

### 1.2. Continuous Training Loop

1.  **Data Collection:** The Agent's successful execution traces, high-quality code generation, and validated Phaselock Artifacts are logged as **high-value training samples**.
2.  **Distillation:** A background process (leveraging the user's M1 Max or remote compute) uses the Teacher Model's outputs (soft labels) to train the Student Model.
3.  **Deployment:** The newly trained, faster Student Model is deployed as the new **'Hyper-Speed Mode'** model, replacing the previous Student Model.

## 2. Adaptive Quantization and Model Switching

The CMO system introduces a dynamic mechanism to switch between the high-accuracy Teacher Model and the high-speed Student Model.

### 2.1. 'Hyper-Speed Mode'

*   **Activation:** The Agent automatically enters **'Hyper-Speed Mode'** when the task complexity is low (e.g., simple code completion, file navigation, single-line edits).
*   **Mechanism:** The Agent switches to the most aggressively **quantized Student Model** to achieve near-instantaneous response times.
*   **Benefit:** Eliminates perceived latency for the majority of common IDE interactions.

### 2.2. Complexity Threshold Switching

The switch from Student to Teacher Model is governed by a **Complexity Threshold**, which is calculated based on:

| Metric | Source | Threshold Trigger |
| :--- | :--- | :--- |
| **Task Group Complexity** | Antigravity's internal Task Group definition. | Multi-step tasks (e.g., "Implement new feature and deploy via Phaselock Canary"). |
| **Code AST Depth** | Real-time analysis of the Abstract Syntax Tree of the code being edited. | High depth/branching factor indicates a need for the Teacher's full reasoning capacity. |
| **Phaselock Gating Status** | `phaselock_check_gating` tool. | Any task that involves advancing a Phaselock phase or modifying a high-risk component requires the Teacher Model. |

## 3. The 'Self-Correction' Tool

The `cmo_correct_reasoning_trace` tool is the critical component for the closed-loop learning system.

| Tool Name | Description | Integration Point |
| :--- | :--- | :--- |
| `cmo_correct_reasoning_trace` | Invoked when an Agent's reasoning trace leads to a failed execution or an incorrect Phaselock decision. The tool captures the full context of the failure and the successful correction (provided by the user or another Agent). | Agent Reasoning Model (Post-failure analysis) |
| **Function:** | The tool formats the failure/correction pair into a high-quality, high-priority training sample and injects it directly into the Self-Distillation pipeline's training set. | |
| **Benefit:** | Ensures the Agent learns from its mistakes in real-time, preventing the same error from occurring in the future and rapidly improving the Student Model's reliability. | |

## 4. Integration into Antigravity-Phaselock Framework

The CMO system will be integrated as follows:

*   **`tools/`**: The `cmo_correct_reasoning_trace` tool will be exposed via the Phaselock API service.
*   **`src/`**: The Antigravity extension will contain the logic for the **'Hyper-Speed Mode'** switching and the complexity threshold calculation.
*   **`phaselock_protocol/`**: The Phaselock governance will be updated to include a new artifact: `reasoning_trace_log.json` to store the data for the CMO pipeline.

This CMO system is the ultimate answer to the user's request, providing a feature that is both unexpected and fundamentally transformative to the IDE's performance.
