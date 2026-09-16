---
layout: null
title: NLP Systems Portfolio
---
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{{ page.title }} | Talha Mushtaq</title>
  <meta name="description" content="NLP, RAG, GenAI evaluation, and machine learning portfolio by Talha Mushtaq.">
  <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
</head>
<body>
  <header class="shell topbar">
    <a class="brand" href="{{ '/' | relative_url }}">TM / NLP SYSTEMS</a>
    <nav class="nav" aria-label="Main navigation">
      <a href="#work">Work</a>
      <a href="#method">Method</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <div class="shell desktop-icons" aria-label="Desktop shortcuts">
    <a class="desktop-icon" href="#work"><span class="icon-art">▣</span><span>My Projects</span></a>
    <a class="desktop-icon" href="https://github.com/tmushtaq12/analytics-portfolio"><span class="icon-art">▤</span><span>Code Repo</span></a>
    <a class="desktop-icon" href="#method"><span class="icon-art">?</span><span>Read Me</span></a>
  </div>

  <main>
    <section class="hero">
      <div class="shell">
        <div class="eyebrow">Applied NLP · GenAI · Evaluation</div>
        <h1>Reliable language systems, measured in the open.</h1>
        <p class="lede">I build practical experiments around NLP safety, retrieval, model evaluation, and production-minded AI workflows. Every project has a dataset, a runnable baseline, measurable results, and a clear next step.</p>
        <div class="actions">
          <a class="button primary" href="#work">Explore the work</a>
          <a class="button" href="https://github.com/tmushtaq12/analytics-portfolio">View code on GitHub</a>
        </div>
        <div class="signal-grid" aria-label="Portfolio metrics">
          <div class="signal"><strong>0.72</strong><span>Test macro F1</span></div>
          <div class="signal"><strong>84.5%</strong><span>RAG Recall@5</span></div>
          <div class="signal"><strong>85.6%</strong><span>QA token F1</span></div>
          <div class="signal"><strong>173ms</strong><span>Mean QA latency</span></div>
        </div>
      </div>
    </section>

    <section class="section" id="work">
      <div class="shell">
        <div class="section-heading">
          <h2>Selected work</h2>
          <p>Small, honest systems that show how I think: define the risk, build a baseline, measure it, inspect failures, and design the production path.</p>
        </div>
        <div class="projects">
          <article class="card featured">
            <div class="number">01 / SAFETY</div>
            <h3>Offensive-speech detection</h3>
            <p>A class-balanced TF-IDF and logistic-regression safety baseline on the real TweetEval benchmark, with PII masking and error visibility.</p>
            <div class="tags"><span class="tag">NLP</span><span class="tag">F1</span><span class="tag">PII</span></div>
            <a class="card-link" href="{{ '/projects/nlp-safety/' | relative_url }}">View my work →</a>
          </article>
          <article class="card">
            <div class="number">02 / RETRIEVAL</div>
            <h3>RAG retrieval evaluation</h3>
            <p>A transparent SQuAD retrieval baseline that measures whether answer-bearing context reaches the generator at rank 1 and rank 5.</p>
            <div class="tags"><span class="tag">RAG</span><span class="tag">Recall@k</span><span class="tag">TF-IDF</span></div>
            <a class="card-link" href="{{ '/projects/rag-retrieval/' | relative_url }}">View my work →</a>
          </article>
          <article class="card">
            <div class="number">03 / GENAI</div>
            <h3>Evaluation lab</h3>
            <p>A real Hugging Face QA experiment tracking exact match, token F1, mean latency, P95 latency, and representative model errors.</p>
            <div class="tags"><span class="tag">Transformers</span><span class="tag">Latency</span><span class="tag">QA</span></div>
            <a class="card-link" href="{{ '/projects/genai-evaluation/' | relative_url }}">View my work →</a>
          </article>
          <article class="card">
            <div class="number">04 / MODELING</div>
            <h3>Readable regression</h3>
            <p>A scikit-learn model with preprocessing, cross-validation, coefficient interpretation, residual analysis, and a baseline comparison.</p>
            <div class="tags"><span class="tag">Python</span><span class="tag">ML</span><span class="tag">Diagnostics</span></div>
            <a class="card-link" href="{{ '/projects/regression/' | relative_url }}">View my work →</a>
          </article>
          <article class="card">
            <div class="number">05 / FOUNDATIONS</div>
            <h3>Data and SQL analysis</h3>
            <p>Business-focused SQL and exploratory analysis projects that demonstrate data cleaning, aggregation, KPI design, and communication.</p>
            <div class="tags"><span class="tag">SQL</span><span class="tag">Pandas</span><span class="tag">KPI</span></div>
            <a class="card-link" href="{{ '/projects/foundations/' | relative_url }}">View my work →</a>
          </article>
          <article class="card">
            <div class="number">06 / NEXT</div>
            <h3>Production path</h3>
            <p>The next layer is API serving, embeddings, hybrid retrieval, prompt/version tracking, Docker, and a CI evaluation gate.</p>
            <div class="tags"><span class="tag">FastAPI</span><span class="tag">Docker</span><span class="tag">MLOps</span></div>
            <a class="card-link" href="{{ '/projects/production/' | relative_url }}">Open roadmap →</a>
          </article>
        </div>
      </div>
    </section>

    <section class="section alt" id="method">
      <div class="shell">
        <div class="section-heading">
          <h2>How I work</h2>
          <p>The portfolio is designed around evidence, not claims.</p>
        </div>
        <div class="story">
          <div class="story-block"><h3>Build the smallest useful baseline.</h3><ul><li>Use a real benchmark or clearly documented data.</li><li>Keep the code readable enough to audit.</li><li>Separate data preparation, model logic, and scoring.</li></ul></div>
          <div class="story-block"><h3>Make failure visible.</h3><ul><li>Choose metrics that reflect the product risk.</li><li>Inspect confusion matrices and error examples.</li><li>Track latency and not only quality.</li></ul></div>
          <div class="story-block"><h3>Design the next experiment.</h3><ul><li>Compare lexical and dense retrieval.</li><li>Test slices, drift, bias, and adversarial inputs.</li><li>Record model and dataset versions.</li></ul></div>
          <div class="story-block"><h3>Keep production in view.</h3><ul><li>Put providers behind adapters.</li><li>Plan for secrets, auth, logging, and monitoring.</li><li>Turn evaluation into a CI quality gate.</li></ul></div>
        </div>
      </div>
    </section>
  </main>

  <footer class="shell footer" id="contact">
    <a class="start-button" href="{{ '/' | relative_url }}">▣ Start</a>
    <span class="task-divider"></span>
    <strong>Talha Mushtaq</strong> · NLP and GenAI portfolio · <a href="https://www.linkedin.com/in/tmushtaq/">LinkedIn</a> · <a href="mailto:tmushtaq599@outlook.com">Email</a> · <a href="https://github.com/tmushtaq12">GitHub</a>
    <span class="clock">NLP.EXE</span>
  </footer>
</body>
</html>
