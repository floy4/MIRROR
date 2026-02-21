<div align="center">

  <h1 style="font-size: 2.5em; font-weight: bold;">
    MIRROR: Multimodal Iterative Reasoning via Reflection On Visual Regions
  </h1>

  <div style="font-size: 1.2em; margin-bottom: 1em;">
    <span class="author-block">
      <a href="#">Haoyu Zhang</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Yuwei Wu</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Pengxiang Li</a><sup>1</sup>,
    </span>
    <span class="author-block">
      <a href="#">Xintong Zhang</a><sup>1</sup>,
    </span>
    <span class="author-block">
      <a href="#">Zhi Gao</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Rui Gao</a><sup>1,2</sup>,
    </span>
    <span class="author-block">
      <a href="#">Mingyang Gao</a><sup>1</sup>,
    </span>
    <span class="author-block">
      <a href="#">Che Sun</a><sup>1</sup>,
    </span>
    <span class="author-block">
      <a href="#">Yunde Jia</a><sup>2</sup>
    </span>
  </div>

  <div style="font-size: 1.0em; margin-bottom: 1em;">
    <span class="author-block"><sup>1</sup>Beijing Key Laboratory of Intelligent Information Technology, BIT,</span>
    <span class="author-block"><sup>2</sup>Shenzhen MSU-BIT University</span> [cite: 14, 15]
  </div>

  <div class="column has-text-centered">
    <div class="publication-links">
      <span class="link-block">
        <a href="https://mirror.github.io/" class="external-link button is-normal is-rounded is-dark">
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
  <img src="./static/images/teaser.png" width="85%" />
</div>
<div align="center" style="width: 80%; margin: 0 auto; text-align: justify;">
  <p>
    <strong>"Look Again" before you answer.</strong> Unlike standard VLMs that suffer from hallucinations or logic errors (e.g., missing specific visual details) [cite: 6, 20], <strong>MIRROR</strong> triggers a closed-loop visual verification process[cite: 9, 61]. It actively generates visual prompts (e.g., yellow points, purple ellipses) to ground its reasoning in specific image regions, correcting its initial errors through iterative reflection[cite: 60, 62].
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
            Existing Vision-Language Models (VLMs) often produce plausible yet ungrounded answers because their reasoning is detached from image evidence[cite: 7, 24]. To address this "modality disconnect," we propose <strong>MIRROR</strong>, a framework for multimodal iterative reasoning via reflection on visual regions[cite: 8, 23]. 
          </p>
          <p>
            We construct <strong>ReflectV</strong>, a visual reflective dataset for multi-turn supervision that explicitly contains reflection triggers and region-based verification actions[cite: 10, 63]. MIRROR is formulated as a closed-loop process comprising draft, critique, region-based verification, and revision[cite: 9, 104]. Extensive experiments show that MIRROR improves correctness and reduces hallucinations, achieving <strong>92.00 on OCRBench</strong> [cite: 248, 330] and <strong>94.42 on POPE</strong> [cite: 250, 330], proving that reflection should be an evidence-seeking process rather than a purely textual revision step[cite: 11, 66].
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
          <strong>🔄 Closed-Loop Visual Reflection:</strong> MIRROR transforms open-loop text generation into a closed-loop grounded verification process, inspired by the human cognitive instinct to "look again" when detecting ambiguity[cite: 26, 27, 28].
        </li>
        <li>
          <strong>📚 ReflectV Dataset & Multi-Agent Pipeline:</strong> We implement a novel multi-agent pipeline to curate <strong>ReflectV</strong> (~24k samples), transforming static QA pairs into rich correction histories with precise visual cues[cite: 63, 71, 171].
        </li>
        <li>
          <strong>🚀 SOTA Performance & Efficiency:</strong> MIRROR outperforms strong baselines (e.g., Qwen2.5-VL, InternVL3) across diverse benchmarks[cite: 73, 266]. It balances efficiency and rigor, resolving <strong>80.2% of samples in the first turn</strong> while engaging in deep reflection only when necessary[cite: 674, 694].
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
      <img src="./static/images/method.png" width="90%" />
      <p style="font-size: 0.9em; margin-top: 10px;">Figure 1: The MIRROR framework architecture and the closed-loop verification process[cite: 104, 144].</p>
    </div>

    <div class="content has-text-justified">
      <h3 class="title is-4">1. ReflectV Data Construction</h3>
      <p>
        To teach models how to reflect visually, we transform external feedback into self-reflection using a rigorous curation pipeline[cite: 64, 171, 220]:
      </p>
      <ul>
        <li><strong>Dialogue Filtering Strategy:</strong> We preserve trajectories only if they show strictly ascending scores ($s_{t+1} > s_t$) and successful convergence to a perfect score[cite: 226, 227].</li>
        <li><strong>Visual Grounding:</strong> We ground the introspective process with task-adaptive keywords, injecting visual attribute descriptions (e.g., "indicated by the red point") back into the reflection text[cite: 230, 233].</li>
        <li><strong>Self-Reflective Conversion:</strong> External corrections (e.g., "Your answer is incorrect") are rewritten into a first-person reflective thought process[cite: 237, 238].</li>
      </ul>

      <h3 class="title is-4">2. Inference Mechanism</h3>
      <p>
        MIRROR follows a four-step loop: (i) draft an initial answer; (ii) self-reflection to identify potential errors; (iii) visual verification using a tool-augmented generator to mark task-relevant regions; and (iv) refinement based on the updated visual evidence[cite: 104, 105, 106].
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
        MIRROR consistently outperforms its base model (Qwen2.5-VL-7B) across various benchmarks, particularly in reducing hallucinations and enhancing fine-grained perception[cite: 266, 318].
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
        <strong>Analysis:</strong> MIRROR achieves significant gains over the base models, specifically a <strong>+8.8%</strong> improvement on OCRBench [cite: 248] and a <strong>+13.36%</strong> improvement on HalluBench[cite: 318].
      </p>
    </div>

    <br>
    <div class="content">
      <h3 class="title is-4">⚔️ Comparison with Reasoning Paradigms</h3>
      <p>
        MIRROR addresses the inherent limitations of <strong>Text Reflection</strong> (which suffers from speculation) and <strong>Thinking with Images</strong> (which lacks a feedback loop)[cite: 331, 332, 333].
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
                <th>Efficiency (Time s/sample)</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Text Reflection</td>
                <td>VL-Rethinker</td>
                <td>85.40</td>
                <td>84.19</td>
                <td>5.56</td>
              </tr>
              <tr>
                <td>Thinking w/ Images</td>
                <td>Adaptive-CoF</td>
                <td>86.00</td>
                <td>89.30</td>
                <td>4.02</td>
              </tr>
              <tr style="font-weight: bold; background-color: #e6fffa;">
                <td>Closed-Loop (Ours)</td>
                <td>MIRROR</td>
                <td>92.00</td>
                <td>94.42</td>
                <td>3.73</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <p>
        <strong>Efficiency Insight:</strong> MIRROR reduces inference time by <strong>32.9%</strong> compared to VL-Rethinker [cite: 722] and outperforms Adaptive-CoF while consuming fewer tokens[cite: 721, 725].
      </p>
    </div>
  </div>
</section>
