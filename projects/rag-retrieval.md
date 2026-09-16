---
layout: null
title: RAG Retrieval Evaluation
---
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{{ page.title }} | NLP Systems</title>
  <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
</head>
<body>
  <header class="shell topbar">
    <a class="brand" href="{{ '/' | relative_url }}">TM / NLP SYSTEMS</a>
    <nav class="nav"><a href="{{ '/' | relative_url }}">Home</a><a href="#contact">Contact</a></nav>
  </header>

  <main class="shell case-study">
    <div class="case-titlebar">RAG Retrieval Evaluation.exe</div>
    <article class="case-body">
      <div class="eyebrow">02 / Retrieval</div>
      <h1>Finding the evidence first</h1>
      <p>A guided walkthrough of the retrieval half of a RAG system: index knowledge, rank evidence, measure what was found, and only then think about generation.</p>

      <div class="case-metrics">
        <div class="case-metric"><strong>5,928</strong><span>Answerable questions</span></div>
        <div class="case-metric"><strong>60.3%</strong><span>Recall@1</span></div>
        <div class="case-metric"><strong>84.5%</strong><span>Recall@5</span></div>
      </div>

      <div class="guide-step"><span class="step-number">01</span><div><h2>Separate retrieval from generation</h2><p>A RAG system has two distinct jobs: retrieve useful evidence and generate an answer from that evidence. This project evaluates retrieval alone so a weak retriever cannot hide behind fluent model output.</p></div></div>
      <div class="guide-step"><span class="step-number">02</span><div><h2>Use a real benchmark</h2><p>The project uses the SQuAD v2 development set. It keeps answerable questions for the retrieval score, deduplicates their source contexts, and preserves the gold answer for evaluation.</p></div></div>
      <div class="guide-step"><span class="step-number">03</span><div><h2>Build a transparent baseline</h2><ul><li>TF-IDF converts every context into a sparse lexical vector.</li><li>Unigrams and bigrams capture individual terms and short phrases.</li><li>Cosine similarity ranks contexts against the question.</li><li>The top results become the evidence a future generator would receive.</li></ul></div></div>
      <div class="guide-step"><span class="step-number">04</span><div><h2>Understand Recall@k</h2><p>Recall@1 asks whether the first result contains the answer. Recall@5 asks whether at least one of the first five results contains it.</p><p class="callout"><strong>Lesson:</strong> If the answer-bearing context is not retrieved, a generator cannot reliably ground its answer. Retrieval quality is a prerequisite for faithfulness.</p></div></div>
      <div class="guide-step"><span class="step-number">05</span><div><h2>Inspect the tradeoff</h2><p>Recall rises from 60.3% at rank 1 to 84.5% at rank 5, but sending more context can increase latency, token cost, and the chance of confusing the generator with irrelevant evidence.</p></div></div>
      <div class="guide-step"><span class="step-number">06</span><div><h2>Design the next experiment</h2><p>Replace lexical retrieval with dense embeddings, compare FAISS and hybrid search, add a reranker, and test conversation-aware query rewriting. Keep Recall@k, latency, and context size in the same experiment record.</p></div></div>

      <h2>Practice exercise</h2>
      <p>Change <code>top_k=5</code> to <code>top_k=1</code> inside the evaluation flow. Run it again and compare the result with Recall@5. Then explain why higher recall is not automatically better for a production RAG system.</p>
      <a class="case-link" href="https://github.com/tmushtaq12/analytics-portfolio/tree/main/projects/rag-retrieval-evaluation">View source code</a>
      <a class="case-link" href="{{ '/' | relative_url }}">Back to portfolio</a>
    </article>
  </main>

  <footer class="shell footer" id="contact">Talha Mushtaq · <a href="mailto:tmushtaq599@outlook.com">Email</a> · <a href="https://www.linkedin.com/in/tmushtaq/">LinkedIn</a></footer>
</body>
</html>
