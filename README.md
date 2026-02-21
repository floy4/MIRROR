---
layout: default
title: MIRROR Project Page
---

<div align="center">

  <h1 style="font-size: 2.5em; font-weight: bold;">
    MIRROR: Multimodal Iterative Reasoning via Reflection on Visual Regions
  </h1>

  <div style="font-size: 1.2em; margin-bottom: 1em;">
    <span class="author-block">
      <a href="#">Haoyu Zhang</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Yuwei Wu</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Pengxiang Li</a><sup>2</sup>
    </span>
    <span class="author-block">
      <a href="#">Xintong Zhang</a><sup>2</sup>
    </span>
    <span class="author-block">
      <a href="#">Zhi Gao</a><sup>1,2</sup>
    </span>
    <span class="author-block">
      <a href="#">Rui Gao</a><sup>1,2</sup>
    </span>
    <span class="author-block">
      <a href="#">Mingyang Gao</a><sup>1</sup>
    </span>
    <span class="author-block">
      <a href="#">Che Sun</a><sup>2</sup>
    </span>
    <span class="author-block">
      <a href="#">Yunde Jia</a><sup>2</sup>
    </span>
  </div>

  <div style="font-size: 1.0em; margin-bottom: 1em;">
    <span class="author-block"><sup>1</sup>Beijing Key Laboratory of Intelligent Information Technology, School of Computer Science & Technology, Beijing Institute of Technology,</span>
    <span class="author-block"><sup>2</sup>Guangdong Laboratory of Machine Perception and Intelligent Computing, Shenzhen MSU-BIT University</span>
  </div>

  <div class="column has-text-centered">
    <div class="publication-links">
      <span class="link-block">
        <a href="#" class="external-link button is-normal is-rounded is-dark">
          <span class="icon">📄</span>
          <span>Paper</span>
        </a>
      </span>
      <span class="link-block">
        <a href="#" class="external-link button is-normal is-rounded is-dark">
          <span class="icon">💻</span>
          <span>Code</span>
        </a>
      </span>
      <span class="link-block">
        <a href="#" class="external-link button is-normal is-rounded is-dark">
          <span class="icon">📚</span>
          <span>ReflectV Dataset</span>
        </a>
      </span>
      <span class="link-block">
        <a href="#" class="external-link button is-normal is-rounded is-dark">
          <span class="icon">🤗</span>
          <span>Demo</span>
        </a>
      </span>
    </div>
  </div>

</div>

<br>

<div align="center">
  <img src="./static/images/teaser.pdf" width="85%" />
</div>
<div align="center" style="width: 80%; margin: 0 auto; text-align: justify;">
  <p>
    <strong>"Look Again" before you answer.</strong> Unlike standard VLMs that suffer from attention drift (e.g., missing the distant red car) or hallucination (e.g., miscounting dogs), <strong>MIRROR</strong> triggers a closed-loop visual verification process. It actively generates visual prompts (e.g., cyan points, green circles) to ground its reasoning in specific image regions, correcting its own initial errors.
  </p>
</div>

<hr>

<section class="section">
  <div class="container is-max-desktop">
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Abstract</h2>
        <div class="content has-text-justified">
          <p>
            Existing Multi-modal Large Language Models (MLLMs) often struggle with fine-grained perception and hallucination due to the lack of a self-correction mechanism grounded in visual evidence. To address this, we introduce <strong>MIRROR</strong>, a closed-loop framework that empowers MLLMs to "look again" when facing uncertainty.
          </p>
          <p>
            We construct <strong>ReflectV</strong>, a high-quality dataset synthesized via a multi-agent pipeline that transforms static QA into visual reflective trajectories. Leveraging this data, MIRROR learns to actively generate visual prompts (e.g., bounding boxes, points) to verify its hypotheses. Extensive experiments demonstrate that MIRROR significantly outperforms state-of-the-art models (e.g., Qwen2.5-VL, InternVL3) across comprehensive benchmarks, achieving <strong>92.00 on OCRBench</strong> and <strong>94.42 on POPE</strong>, effectively mitigating hallucinations while maintaining efficient inference.
          </p>
        </div>
      </div>
    </div>
  </div>
</section>

<hr>

<section class="section">
  <div class="container is-max-desktop">
    <h2 class="title is-3 has-text-centered">Key Contributions</h2>
    <div class="content">
      <ul>
        <li>
          <strong>🔄 Closed-Loop Visual Reflection:</strong> Instead of relying on text-only speculation, MIRROR employs a "Think-then-Verify" mechanism. It actively queries the image with visual tools to validate its reasoning chain.
        </li>
        <li>
          <strong>📚 ReflectV Dataset & Rigorous Filtering:</strong> We introduce <strong>ReflectV</strong>, constructed via a pipeline that includes strict <em>Visual Verification Filtering</em>. Our ablation studies prove that <strong>Data Quality > Quantity</strong>—training on 24k filtered samples significantly outperforms 35k raw samples.
        </li>
        <li>
          <strong>🚀 SOTA Performance & Adaptability:</strong> MIRROR achieves state-of-the-art results on fine-grained perception and hallucination benchmarks. Crucially, it is <strong>adaptive</strong>: resolving ~98% of simple queries in one turn while engaging in deep reflection only for complex tasks.
        </li>
      </ul>
    </div>
  </div>
</section>

<br>

<section class="section">
  <div class="container is-max-desktop">
    <h2 class="title is-3 has-text-centered">Methodology: The MIRROR Framework</h2>
    
    <div align="center">
      <img src="./static/images/method.pdf" width="90%" />
      <p style="font-size: 0.9em; margin-top: 10px;">Figure 1: The architecture of MIRROR and the ReflectV data construction pipeline.</p>
    </div>

    <div class="content has-text-justified">
      <h3 class="title is-4">1. ReflectV Data Construction</h3>
      <p>
        To transform raw dialogue simulations into high-quality instruction data, we implement a rigorous curation pipeline. This process ensures logical convergence, visual grounding, and introspective alignment through three sequential stages:
      </p>
      <ul>
        <li><strong>Dialogue Filtering Strategy:</strong> We enforce strictly ascending scores and successful convergence to prune invalid reasoning paths.</li>
        <li><strong>Visual Grounding:</strong> We extract task-adaptive keywords and inject visual attribute descriptions to prevent text-only speculation.</li>
        <li><strong>Self-Reflective Conversion:</strong> We transform external "Teacher" corrections into internal "Student" introspection.</li>
      </ul>

      <h3 class="title is-4">2. Inference Mechanism</h3>
      <p>
        During inference, MIRROR identifies potential errors and generates task-adaptive visual prompts (e.g., <em>“check the red region”</em>) to re-attend to neglected details, effectively bridging the gap between symbolic reasoning and visual perception.
      </p>
    </div>
  </div>
</section>

<hr>

<section class="section">
  <div class="container is-max-desktop">
    <h2 class="title is-3 has-text-centered">Experimental Results</h2>

    <div class="content">
      <h3 class="title is-4">🏆 Main Results on Benchmarks</h3>
      <p>
        We compare MIRROR with SOTA MLLMs (e.g., Qwen2.5-VL, InternVL3). MIRROR consistently outperforms its backbone across three key dimensions: <strong>General Capabilities</strong>, <strong>OCR & Document Understanding</strong>, and <strong>Hallucination Mitigation</strong>.
      </p>
      <div class="table-container">
        <table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
          <thead>
            <tr style="background-color: #f5f5f5;">
              <th>Model</th>
              <th>Param</th>
              <th>OCRBench</th>
              <th>POPE</th>
              <th>HalluBench</th>
              <th>MathVision</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Qwen2.5-VL</td>
              <td>7B</td>
              <td>83.20</td>
              <td>86.45</td>
              <td>68.66</td>
              <td>23.36</td>
            </tr>
            <tr>
              <td>InternVL3</td>
              <td>8B</td>
              <td>85.00</td>
              <td>90.37</td>
              <td>49.90</td>
              <td>20.39</td>
            </tr>
            <tr style="font-weight: bold; background-color: #e6fffa;">
              <td>MIRROR (Ours)</td>
              <td>7B</td>
              <td>92.00</td>
              <td>94.42</td>
              <td>82.02</td>
              <td>28.29</td>
            </tr>
          </tbody>
        </table>
      </div>
      <p style="font-size: 0.9em;">
        <strong>Analysis:</strong> MIRROR achieves a <strong>+5.5%</strong> gain on OCRBench and <strong>+13.3%</strong> on HalluBench compared to the backbone, proving the efficacy of visual grounding in reducing hallucinations.
      </p>
    </div>

    <br>
    <div class="content">
      <h3 class="title is-4">⚔️ Comparison with Reasoning Paradigms</h3>
      <p>
        We benchmark MIRROR against two distinct paradigms: <strong>Text Reflection</strong> (e.g., VL-Rethinker) and <strong>Thinking with Images</strong> (e.g., DeepEyes).
      </p>
      <div class="columns is-centered">
        <div class="column is-three-quarters">
          <table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
            <thead>
              <tr style="background-color: #f5f5f5;">
                <th>Paradigm</th>
                <th>Method</th>
                <th>OCRBench</th>
                <th>POPE</th>
                <th>Weakness Identified</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Text Reflection</td>
                <td>VL-Rethinker</td>
                <td>85.40</td>
                <td>84.19</td>
                <td>Hallucination Accumulation</td>
              </tr>
              <tr>
                <td>Thinking w/ Images</td>
                <td>DeepEyes</td>
                <td>88.10</td>
                <td>87.70</td>
                <td>Lack of Feedback Loop</td>
              </tr>
              <tr style="font-weight: bold; background-color: #e6fffa;">
                <td>Closed-Loop (Ours)</td>
                <td>MIRROR</td>
                <td>92.00</td>
                <td>94.42</td>
                <td>None (Addresses both)</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <p>
        <strong>Insight:</strong> Text-only reflection risks degenerating into speculation (low POPE score). Visual augmentation methods lack targeted error correction. MIRROR's closed-loop mechanism bridges these gaps.
      </p>
    </div>

    <br>
    <div class="content">
      <h3 class="title is-4">📊 Dynamic Adaptability</h3>
      <div align="center">
        <img src="./static/images/adaptability_chart.png" width="60%" />
      </div>
      <p>
        <strong>Efficiency vs. Rigor:</strong> MIRROR adaptively adjusts its reasoning depth. For straightforward tasks like ChartQA, <strong>98.7%</strong> of samples are resolved in Round 1. For complex tasks like MME-RealWorld, it triggers multi-turn reflection, ensuring computational resources are used only when necessary.
      </p>
    </div>

  </div>
</section>

<hr>

<section class="section">
  <div class="container is-max-desktop">
    <h2 class="title is-3 has-text-centered">Qualitative Analysis</h2>
    <div class="columns is-vcentered">
      <div class="column has-text-centered">
        <img src="./static/images/case_study_1.png" alt="Counting Case" width="100%"/>
        <p><strong>Case 1: Fine-grained Counting.</strong> Baseline sees 3 dogs; MIRROR reflects, marks points, and correctly counts 2.</p>
      </div>
      <div class="column has-text-centered">
        <img src="./static/images/case_study_2.png" alt="Attribute Binding Case" width="100%"/>
        <p><strong>Case 2: Attribute Binding.</strong> Baseline misses the car; MIRROR zooms in/marks the distant region to identify the red car.</p>
      </div>
    </div>
  </div>
</section>

<hr>

<section class="section" id="BibTeX">
  <div class="container is-max-desktop content">
    <h2 class="title">BibTeX</h2>
    <pre><code>@article{mirror2026,
  title={MIRROR: A Closed-Loop Visual Reflection Framework for Multi-modal LLMs},
  author={User, and Collaborators},
  journal={arXiv preprint arXiv:2602.xxxxx},
  year={2026}
}</code></pre>
  </div>
</section>

<footer class="footer">
  <div class="container">
    <div class="content has-text-centered">
      <p>
        This website is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
        Template adapted from <a href="https://github.com/nerfies/nerfies.github.io">Nerfies</a>.
      </p>
    </div>
  </div>
</footer>
