---
layout: null
title: Machine Learning Foundations
---
<!doctype html><html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>{{ page.title }} | NLP Systems</title><link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}"></head><body><header class="shell topbar"><a class="brand" href="{{ '/' | relative_url }}">TM / NLP SYSTEMS</a><nav class="nav"><a href="{{ '/' | relative_url }}">Home</a><a href="#contact">Contact</a></nav></header><main class="shell case-study"><div class="case-titlebar">ML Foundations.exe</div><article class="case-body">
<div class="eyebrow">LEARNING / MACHINE LEARNING</div>
<h1>From best-fit lines to neural networks</h1>
<p>A practical guide to supervised learning: fitting a line, measuring its misses, transforming skewed data, and training a small neural network. Each concept connects to a reproducible Titanic fare experiment. This is educational modeling, not a production pricing system.</p>

<h2>1. The line of best fit</h2>
<p>With one input feature, simple linear regression predicts a target with <code>prediction = slope * input + intercept</code>. Ordinary least squares chooses the slope and intercept that minimize the sum of squared residuals. In data terms, the slope is the average predicted target change for a one-unit input change; the intercept is the predicted target when the input is zero.</p>
<p>For a single feature, the best-fit slope can be written as <code>sum((x - mean(x)) * (y - mean(y))) / sum((x - mean(x)) ** 2)</code>; the intercept is <code>mean(y) - slope * mean(x)</code>. Squaring gives large misses more influence, so outliers can pull the line.</p>
<p>A residual is <code>actual - prediction</code>. A point above the fitted line has a positive residual; a point below it has a negative residual. A good residual plot should not show a clear curve or funnel. Curvature suggests the straight-line form misses structure; a widening funnel can indicate that error spread changes with the prediction.</p>
<figure class="learning-figure">
  <svg viewBox="0 0 640 300" role="img" aria-labelledby="fit-title fit-desc">
    <title id="fit-title">Illustrative line of best fit and residuals</title>
    <desc id="fit-desc">Synthetic observations around a fitted line. Dashed vertical segments show residual distances between observations and predictions.</desc>
    <rect x="66" y="24" width="530" height="220" fill="#ffffff" stroke="#808080" />
    <path d="M66 79H596 M66 134H596 M66 189H596 M172 24V244 M278 24V244 M384 24V244 M490 24V244" stroke="#d0d0d0" stroke-width="1" />
    <line x1="85" y1="220" x2="580" y2="48" stroke="#000080" stroke-width="3" />
    <g stroke="#c44" stroke-dasharray="4 4" stroke-width="2">
      <line x1="115" y1="210" x2="115" y2="210" />
      <line x1="165" y1="175" x2="165" y2="192" />
      <line x1="215" y1="190" x2="215" y2="175" />
      <line x1="265" y1="150" x2="265" y2="158" />
      <line x1="315" y1="172" x2="315" y2="141" />
      <line x1="365" y1="115" x2="365" y2="123" />
      <line x1="415" y1="137" x2="415" y2="106" />
      <line x1="465" y1="89" x2="465" y2="89" />
      <line x1="515" y1="82" x2="515" y2="70" />
    </g>
    <g fill="#008080" stroke="#000000" stroke-width="1">
      <circle cx="115" cy="210" r="5" /><circle cx="165" cy="175" r="5" /><circle cx="215" cy="190" r="5" />
      <circle cx="265" cy="150" r="5" /><circle cx="315" cy="172" r="5" /><circle cx="365" cy="115" r="5" />
      <circle cx="415" cy="137" r="5" /><circle cx="465" cy="89" r="5" /><circle cx="515" cy="82" r="5" />
    </g>
    <text x="320" y="278" text-anchor="middle" font-size="14">Input feature</text>
    <text x="18" y="136" text-anchor="middle" font-size="14" transform="rotate(-90 18 136)">Target</text>
    <line x1="420" y1="264" x2="450" y2="264" stroke="#000080" stroke-width="3" /><text x="457" y="268" font-size="12">Best-fit line</text>
    <line x1="520" y1="264" x2="550" y2="264" stroke="#c44" stroke-dasharray="4 4" stroke-width="2" /><text x="557" y="268" font-size="12">Residual</text>
  </svg>
  <figcaption>Illustrative synthetic data: each vertical gap is a residual, the distance from an observed value to the model's prediction.</figcaption>
</figure>
<div class="callout"><strong>Connect this to my project:</strong> The Titanic fare model uses several inputs, including passenger class, age, family size, sex, and embarkation port. It is still linear regression, but its fit is not one line on a two-dimensional chart.</div>

<h2>2. Regression errors</h2>
<p>Error metrics summarize how far predictions are from actual values. They answer different questions, so I compare more than one and always identify the evaluation set:</p>
<ul>
  <li><code>MAE = mean(abs(actual - prediction))</code>: the average miss size, in the target's units. For Titanic fares, that is GBP.</li>
  <li><code>MSE = mean((actual - prediction) ** 2)</code>: squares each miss, so a few large misses count much more. Its units are squared.</li>
  <li><code>RMSE = sqrt(MSE)</code>: like MSE, it penalizes large misses, but returns to the target's units.</li>
  <li><code>R2</code>: compares squared prediction errors with a constant prediction at the evaluated target set's mean. It is not an error size, and can be negative when the model is worse than that reference.</li>
</ul>
<pre><code>residuals = actual - predicted
mae = mean(abs(residuals))
mse = mean(residuals ** 2)
rmse = sqrt(mse)
r2 = 1 - sum(residuals ** 2) / sum((actual - mean(actual)) ** 2)</code></pre>
<p>The mean baseline predicts the training-set average for every test row. MAE and RMSE are reported after inverse transformations, in the original fare units. A model should improve on a baseline and behave reasonably across more than one split before I consider it useful.</p>

<h2>3. Log transforms</h2>
<p>Positive values with a long right tail can be difficult to model: many fares are small and a few are very large. A logarithm compresses the large values. For data that may include zero, Python's <code>log1p(x)</code> computes <code>log(1 + x)</code>. The inverse is <code>expm1(z)</code>.</p>
<pre><code>from sklearn.compose import TransformedTargetRegressor

log_model = TransformedTargetRegressor(
  regressor=preprocessing_and_regressor,
  func=np.log1p,
  inverse_func=np.expm1,
)
log_model.fit(x_train, y_train)
predictions_in_gbp = log_model.predict(x_test)</code></pre>
<p>This project reports MAE and RMSE after predictions are converted back to GBP. A log target changes the training objective: it emphasizes relative differences more than raw-currency differences. It is a hypothesis to test, not an automatic fix for skew or outliers.</p>

<h2>4. Neural networks</h2>
<p>A feed-forward network maps inputs through layers. A neuron calculates a weighted sum plus a bias, then applies an activation. Hidden layers with nonlinear activations can represent curved relationships that a straight line cannot. During training, the optimizer adjusts weights to reduce a loss; the same loss can fall while test performance gets worse, which is overfitting.</p>
<p>The runnable project uses <code>MLPRegressor(hidden_layer_sizes=(16,), solver="lbfgs", alpha=0.01, max_iter=2000)</code> inside the same numeric/categorical preprocessing pipeline as linear regression. A <code>TransformedTargetRegressor</code> trains on <code>log1p(Fare)</code> and returns predictions to GBP. The hidden layer has 16 neurons; <code>alpha</code> penalizes large weights; <code>random_state</code> makes the fit repeatable.</p>
<pre><code>network = build_neural_network_model()
network.fit(x_train, y_train)
network_predictions = network.predict(x_test)
test_mae = mean_absolute_error(y_test, network_predictions)</code></pre>
<p>This MLP is a real educational experiment, but not evidence that a neural network is inherently better. It is more flexible than the linear models and harder to interpret; use the baseline, cross-validation, held-out errors, and residuals together.</p>
<figure class="learning-figure">
  <svg viewBox="0 0 620 245" role="img" aria-labelledby="network-title network-desc">
    <title id="network-title">Simple feed-forward neural network</title>
    <desc id="network-desc">Three input nodes connect to four hidden-layer nodes, which connect to one output node.</desc>
    <g stroke="#808080" stroke-width="1.5">
      <path d="M116 57L278 45 M116 57L278 96 M116 57L278 147 M116 57L278 198 M116 122L278 45 M116 122L278 96 M116 122L278 147 M116 122L278 198 M116 187L278 45 M116 187L278 96 M116 187L278 147 M116 187L278 198" />
      <path d="M318 45L495 122 M318 96L495 122 M318 147L495 122 M318 198L495 122" />
    </g>
    <g fill="#ffffff" stroke="#000080" stroke-width="3">
      <circle cx="100" cy="57" r="16" /><circle cx="100" cy="122" r="16" /><circle cx="100" cy="187" r="16" />
      <circle cx="298" cy="45" r="18" /><circle cx="298" cy="96" r="18" /><circle cx="298" cy="147" r="18" /><circle cx="298" cy="198" r="18" />
      <circle cx="510" cy="122" r="20" />
    </g>
    <g fill="#000000" font-size="13" text-anchor="middle">
      <text x="100" y="231">Inputs</text><text x="298" y="231">Hidden layer</text><text x="510" y="231">Prediction</text>
    </g>
  </svg>
  <figcaption>Illustration only: training learns the connection weights; hidden layers let the model represent nonlinear relationships.</figcaption>
</figure>
<div class="callout"><strong>Good habit:</strong> A neural network is not automatically better than a line. Start with a simple baseline, use a held-out test set, compare appropriate metrics, and check whether the extra complexity earns its keep.</div>

<h2>5. Results from the runnable comparison</h2>
<p>The project uses one 80/20 split with seed 42 and five shuffled cross-validation folds. These are not independent test sets: cross-validation summarizes training-split sensitivity, while the held-out test set is used for the final comparison.</p>
<div class="table-scroll"><table class="results-table">
  <thead><tr><th>Model</th><th>Test MAE</th><th>Test RMSE</th><th>Test R2</th><th>CV MAE mean +/- SD</th></tr></thead>
  <tbody>
    <tr><th>Training-mean baseline</th><td>GBP 25.69</td><td>GBP 39.38</td><td>-0.002</td><td>Not applicable</td></tr>
    <tr><th>Multiple linear</th><td>GBP 20.65</td><td>GBP 30.31</td><td>0.406</td><td>GBP 20.59 +/- 2.36</td></tr>
    <tr><th>Log-target linear</th><td>GBP 10.79</td><td>GBP 25.08</td><td>0.594</td><td>GBP 13.38 +/- 3.47</td></tr>
    <tr><th>Log-target MLP</th><td>GBP 12.61</td><td>GBP 28.48</td><td>0.476</td><td>GBP 12.52 +/- 2.52</td></tr>
  </tbody>
</table></div>
<p>The log-target linear model has the smallest MAE on this one test split; the MLP has a slightly smaller average MAE across the five training folds. That difference warns against selecting a model from one split. The test set was not used to tune hyperparameters, and these scores should be treated as an educational comparison, not a service-level estimate.</p>
<figure class="learning-figure">
  <img class="case-image" src="https://raw.githubusercontent.com/tmushtaq12/analytics-portfolio/main/images/linear_regression_diagnostics.png" alt="Six-panel regression diagnostic: fitted age-to-fare line, actual versus predicted fare, residuals, coefficients, fare distributions by class, and test MAE comparison.">
  <figcaption>Generated from the same model run. Coefficients belong only to the interpretable linear model; they do not explain the neural network.</figcaption>
</figure>

<h2>6. A useful next experiment</h2>
<ol>
  <li>Change one modeling choice at a time and preserve the same fixed test set for the final comparison.</li>
  <li>Inspect the largest absolute residuals and compare them with passenger class and ticket groups.</li>
  <li>Try a group-aware split by ticket so passengers sharing a ticket cannot appear on both sides.</li>
  <li>Compare the log-target model with a robust or regularized alternative using only the training folds for selection.</li>
</ol>
<p>Record the hypothesis, split seed, feature set, model settings, metrics, and examples of large misses for every run. The point is not to accumulate models; it is to understand where the simpler model fails and whether added complexity improves generalization.</p>
<a class="case-link" href="{{ '/projects/regression/' | relative_url }}">View my regression project</a> <a class="case-link" href="https://github.com/tmushtaq12/analytics-portfolio/blob/main/projects/linear-regression/analysis.py">Read the regression code</a> <a class="case-link" href="{{ '/' | relative_url }}">Back to portfolio</a>
</article></main><footer class="shell footer" id="contact">Talha Mushtaq · <a href="mailto:tmushtaq599@outlook.com">Email</a> · <a href="https://www.linkedin.com/in/tmushtaq/">LinkedIn</a></footer></body></html>
