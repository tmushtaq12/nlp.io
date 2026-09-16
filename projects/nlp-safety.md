---
layout: null
title: NLP Safety Pipeline
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
    <div class="case-titlebar">NLP Safety Pipeline.exe</div>
    <article class="case-body">
      <div class="eyebrow">01 / Safety classification</div>
      <h1>Offensive-speech detection</h1>
      <p>A guided walkthrough of a small NLP safety system: define the risk, build a baseline, measure the tradeoffs, and decide what should happen next.</p>

      <div class="case-metrics">
        <div class="case-metric"><strong>0.710</strong><span>Validation macro F1</span></div>
        <div class="case-metric"><strong>0.72</strong><span>Test macro F1</span></div>
        <div class="case-metric"><strong>0.66</strong><span>Offensive recall</span></div>
      </div>

      <div class="guide-step"><span class="step-number">01</span><div><h2>Start with the problem</h2><p>A conversational product needs to identify potentially offensive input before it reaches a downstream model or human workflow. The cost of missing unsafe content is different from the cost of incorrectly flagging a normal message.</p></div></div>
      <div class="guide-step"><span class="step-number">02</span><div><h2>Use real labeled data</h2><p>The project uses the TweetEval offensive-language benchmark with fixed train, validation, and test splits. The labels are binary: not offensive or offensive.</p></div></div>
      <div class="guide-step"><span class="step-number">03</span><div><h2>Build an understandable baseline</h2><ul><li>TF-IDF converts text into weighted word and phrase features.</li><li>Unigrams and bigrams capture both words and short expressions.</li><li>Class-balanced logistic regression gives the minority class appropriate weight.</li><li>Email addresses, phone numbers, and usernames are masked before downstream use.</li></ul></div></div>
      <div class="guide-step"><span class="step-number">04</span><div><h2>Evaluate the risk</h2><p>Macro F1 gives both classes equal importance. Offensive recall shows how much unsafe content the detector catches; offensive precision shows how often those flags are correct.</p><p class="callout"><strong>Lesson:</strong> Accuracy alone can hide safety failures. Inspect the confusion matrix and the false-positive/false-negative tradeoff.</p></div></div>
      <div class="guide-step"><span class="step-number">05</span><div><h2>Design the next experiment</h2><p>Compare this baseline with a calibrated transformer. Then evaluate multilingual, adversarial, and ambiguous examples before choosing a production threshold.</p></div></div>

      <h2>Practice exercise</h2>
      <p>Open the source code and change <code>ngram_range=(1, 2)</code> to <code>ngram_range=(1, 3)</code>. Run the experiment again. Record what changes in macro F1, offensive precision, and offensive recall.</p>
      <a class="case-link" href="https://github.com/tmushtaq12/analytics-portfolio/tree/main/projects/nlp-safety-pipeline">View source code</a>
      <a class="case-link" href="{{ '/' | relative_url }}">Back to portfolio</a>
    </article>
  </main>

  <footer class="shell footer" id="contact">Talha Mushtaq · <a href="mailto:tmushtaq599@outlook.com">Email</a> · <a href="https://www.linkedin.com/in/tmushtaq/">LinkedIn</a></footer>
</body>
</html>
