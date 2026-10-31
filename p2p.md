# Problem Statement: P2P Mobile Mesh Inference

## Objective
Build a web application that runs distributed text generation for a **Byte-Level Micro-Transformer** across **two physical mobile phones** connected over a local peer-to-peer network.

The forward inference pass must be split across both phones in real time so that both devices actively participate in generating every single byte.

---

## Target Architecture & Exact Parameter Specification
To ensure strict fairness, all participants must use the exact same architecture, dimensions, and weights:

* **Architecture:** Vanilla Causal Decoder Transformer (GPT-style)
* **Vocab Size:** `256` (Direct ASCII / UTF-8 bytes `[0..255]`; no BPE/tokenizer needed)
* **Context Length (`max_seq_len`):** `512`
* **Layers (`n_layers`):** `6` (Phone 1 runs Layers 0–2, Phone 2 runs Layers 3–5)
* **Hidden Dimension (`d_model`):** `384`
* **Attention Heads (`n_heads`):** `6` (Head dimension = `64`)
* **Feed-Forward Dimension (`d_ff`):** `1536` ($4 \times d_{model}$)
* **Total Parameters:** **Exactly 11,040,768 parameters (~11.04M)** (~44.16 MB in FP32)

### Deterministic Weights Generation:
Weights are generated using PyTorch with a fixed random seed:
```python
import torch

torch.manual_seed(42)
# Generated weights must be exported to weights.bin (FP32)
```
Because weights are initialized with seed `42`, every team uses identical weights. At `temperature = 0.0`, all implementations must output the exact same deterministic byte sequence.

---

## Target Environment & Universal Device Rule
* **Devices:** Any two stock consumer smartphones (iOS Safari or Android Chrome).
* **Compute Target:** Web CPU only (JavaScript / WebAssembly on CPU).
* **Zero Installation Mandate:** **Strictly zero app installations.** No native apps, no APK sideloading, no TestFlight builds, no developer profiles, and no custom browser flags/experimental toggles. 
* **Judges' Device Rule:** **Judges will use two random phones of their own choice** to open your web app URL, pair the devices, run the benchmark, and measure throughput. Your solution must run universally out-of-the-box on standard mobile browsers.

---

## Hard Requirements
1. **P2P Split Execution:** The model weights and forward pass must be partitioned across the two mobile phones (3 layers per phone). Neither phone may execute the full model alone.
2. **Local Transport:** All intermediate communication (activation tensors, byte tokens) during inference must travel directly between the two phones over a local peer-to-peer channel (WebRTC DataChannel).
3. **Standalone Runtime:** Once the web application is loaded into the mobile browsers, all text generation must run completely offline/locally across the two phones.

---

## Strictly Prohibited
* **NO Installations or Sideloading:** No native apps, APKs, TestFlight, or custom configuration profiles. Must run in stock mobile Safari/Chrome.
* **NO WebGPU or WebGL shaders.** Compute must run strictly on the Web CPU.
* **NO Native Mobile Applications or OS-level Frameworks** (no Swift, Kotlin, CoreML, NNAPI, or native binaries). Everything must run inside a standard mobile web browser.
* **NO Cloud or Remote Backends.** No offloading compute, activations, or byte generation to a remote server, external API, or third-party host during inference.
* **NO Centralized Data Relays.** No routing tensor activations through an external server or centralized TURN relay during inference.
