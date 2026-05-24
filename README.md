<div align="center">
  <h1 style="margin:0; font-size:2.5em; font-weight:bold;">
    <img src="./static/images/icon.svg"
         width="40" height="40"
         alt="MIRROR logo"
         style="vertical-align:middle; margin-right:0.5rem;"/>
    Bridging Modality Disconnect in Self-Reflection via Closed-Loop Visually Grounded Verification
  </h1>

  <br>

  <!-- ArXiv link removed for anonymous review -->
  <a href="https://github.com/floy4/MIRROR/">
    <img src="https://img.shields.io/badge/-Code-black?logo=github" alt="Code">
  </a>
  <a href="https://huggingface.co/datasets/3nnui/Reflect-V">
    <img src="https://img.shields.io/badge/🤗 Dataset-ReflectV-purple" alt="Dataset">
  </a>
</div>

<br>

<span>
Anonymous Authors
<br />
<br />
Anonymous Institution <br />
</span>

<!-- # 🔥News
- [2026/02/21] We released the preprint and the **ReflectV** dataset samples.  -->

<br>


# Abstract

<div align="center">
<img src="static/images/teaser.png" alt="Teaser" width="100%">
</div>

Self-reflection has become a key mechanism for improving reasoning in Vision-Language Models (VLMs), yet this corrective mechanism often fails when resolving complex fine-grained regional ambiguities. This performance degradation stems from the issue of **modality disconnect in self-reflection**: most existing models execute self-reflection either within textual or latent space, lacking a mechanism to explicitly align textual reasoning with visual evidence.

In this paper, we propose **MIRROR**, a closed-loop visual reflection framework comprising four steps: initial response generation, error identification, region-based visual verification, and revision. In this cycle, the model first generates an initial response, identifies uncertain logical assertions that require visual verification, then grounds them in relevant image regions, and finally revises based on the visual evidence. We construct a multi-turn visual reflection dataset **ReflectV**, which empowers the model with such reflective capability.

Extensive experiments across 12 diverse multimodal benchmarks show that MIRROR achieves an average absolute improvement of **7.2 percentage points** over the base model, with particularly strong gains in hallucination mitigation (**+13.36 on HallusionBench**) and general reasoning (**+10.10 on MM-Vet**), demonstrating the advantage of transforming self-reflection from open-loop textual revision into closed-loop, visually grounded verification.

<br>

# MIRROR Framework

### Method: Closed-Loop Reasoning
![Figure 1: MIRROR Architecture](static/images/method.png)

MIRROR upgrades standard VLM inference into a closed-loop verification cycle consisting of drafting, critiquing, region-based verification, and revision to ensure all reasoning steps are anchored in concrete visual evidence.

### ReflectV Dataset
![Figure 2: ReflectV Dataset](static/images/dataset.png)
The ReflectV dataset is synthesized through a multi-agent pipeline that transforms static multimodal QA samples into 24k high-quality reflective trajectories using a rigorous dialogue filtering strategy and a self-reflective conversion mechanism.

<br>

# Experimental Results
## Quantitative Results
### **🏆 Comparison with Base Models**
MIRROR consistently outperforms its backbone (Qwen2.5-VL-7B) and other strong open-source VLMs across diverse benchmarks, particularly in reducing hallucinations and enhancing fine-grained perception. The best and second-best results are highlighted in **bold** and <u>underlined</u>, respectively.

Performance comparison on General Capabilities and OCR & Document Benchmarks.  

| Model                  | Param Size | MM‑Vet | MMStar | SeedBench‑2‑Plus | TextVQA‑Val | OCRBench | ChartQA‑Test |
|------------------------|-----------:|-------:|-------:|-----------------:|-------------:|----------:|-------------:|
| LLaVA‑OneVision        | 7B         | 48.80  | 61.70  | --               | 76.10       | 62.10    | 80.00        |
| InternVL3              | 2B         | 54.95  | 60.70  | 64.95            | 77.00       | 82.20    | 76.08        |
| InternVL3              | 8B         | <u>64.27</u> | 61.50  | 69.61            | 80.51       | 85.00    | 79.64        |
| Qwen2.5‑VL‑3B          | 3B         | 47.39  | 55.87  | 68.81            | 79.12       | 82.60    | 83.20        |
| Qwen2.5‑VL‑7B          | 7B         | 56.60  | 61.21  | <u>70.88</u>     | 84.90       | 83.20    | 86.08        |
| **MIRROR (w/o tool)**  | 7B         | 59.91  | <u>62.80</u> | 70.36            | <u>85.37</u> | <u>88.30</u> | <u>86.56</u> |
| **MIRROR (ours)**      | 7B         | **66.70** | **73.33** | **76.86**        | **86.62**   | **92.00** | **87.92**    |

Performance comparison on Hallucination, Fine-grained Perception, and Reasoning Benchmarks.

| Model                  | Param Size | POPE   | HalluBench | HRBench‑4K | MME‑RW | VStarBench | MathVision |
|------------------------|-----------:|-------:|-----------:|-----------:|-------:|------------:|-----------:|
| LLaVA‑OneVision        | 7B         | 78.10  | 31.60      | 63.00      | --    | 72.30      | 18.30      |
| InternVL3              | 2B         | 89.60  | 42.50      | 61.75      | 43.88 | 68.59      | 21.71      |
| InternVL3              | 8B         | <u>90.37</u> | 49.90      | <u>70.00</u> | <u>48.83</u> | 68.06      | 20.39      |
| Qwen2.5‑VL‑3B          | 3B         | 86.21  | 63.09      | 50.25      | 42.15 | 72.77      | 25.66      |
| Qwen2.5‑VL‑7B          | 7B         | 86.45  | <u>68.66</u> | 68.87      | 44.29 | 75.39      | 23.36      |
| **MIRROR (w/o tool)**  | 7B         | 87.95  | 68.24      | 69.13      | 46.01 | <u>76.44</u> | <u>27.30</u> |
| **MIRROR (ours)**      | 7B         | **94.42** | **82.02**  | **72.88**  | **51.49** | **83.77**  | **28.29**  |

### **⚔️ Comparison with Reasoning Paradigms**
MIRROR addresses the inherent limitations of existing reasoning paradigms by incorporating a closed-loop verification process. All methods are fine-tuned on Qwen2.5-VL-7B for fair comparison.

Performance comparison with SOTA reasoning methods, which are all fine-tuned on Qwen2.5-VL-7B. The best and second-best results are highlighted in **bold** and <u>underlined</u>, respectively.

| Method                 | OCRBench | POPE   | MME-RW | MM-Vet |
|------------------------|----------|--------|--------|--------|
| *Text Reflection*      |          |        |        |        |
| VL-Rethinker           | 85.40    | 84.19  | 47.21  | 56.19  |
| *Visual Reflection*    |          |        |        |        |
| LookBack (Solution)    | 87.50    | 88.20  | 49.80  | 63.50  |
| LookBack (Semantic)    | <u>88.60</u> | <u>89.80</u> | 50.40  | 65.10  |
| *Thinking with Images* |          |        |        |        |
| PixelReasoner-SFT      | 76.35    | 80.01  | 44.73  | 47.68  |
| PixelReasoner          | 82.10    | 86.03  | 49.70  | 52.98  |
| DeepEyes               | 88.10    | 87.70  | 49.50  | 60.28  |
| Adaptive-CoF-SFT       | 85.62    | 82.53  | 50.10  | 62.73  |
| Adaptive-CoF           | 86.00    | 89.30  | <u>50.90</u> | <u>66.21</u> |
| **MIRROR (ours)**      | **92.00** | **94.42** | **51.49** | **66.70** |

<br>

## Qualitative Results
![Figure 3: Real Case](static/images/real_case.png)

* **Spatial Reasoning:** In object counting, standard models often miss small or cluttered items. MIRROR identifies its own counting error, triggers a **blue circle** on the neglected "green cylinder," and corrects the final count.
* **Object Identification:** To mitigate hallucinations, MIRROR actively queries the image with a **cyan point** to confirm the presence of a chair, ensuring the response is grounded in actual pixels rather than linguistic priors.

<br>

<!-- Citation removed for anonymous review -->