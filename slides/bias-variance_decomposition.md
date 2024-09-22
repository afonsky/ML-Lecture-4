---
background: /ship2.jpg
layout: cover
hideInToc: true
---
# Extra Materials
---

## Bias, Variance and Model Complexity

<div class="grid grid-cols-[3fr,2fr]">
<div>
<br>

<figure>
<img src="/Train_Validation_Test.svg" style="width: 430px !important">
</figure>

* **Goals**:
	* **select** a model that generalizes well
		* i.e. yields low error on unseen observations
		* Done on **validation** set
	* **measure** its performance (as an error or accuracy)
		* Done on **test** set (on **validation** as well)
* More complex models lead to overfitting<br> (high variance, and low bias)
	* Model complexity correlates with degrees of freedom (DF) and # of estimated parameters
* For a fixed model, prediction error depends on train set of observations

</div>
<div>
<br>
<br>
<br>
<br>
<br>
  <figure>
    <img src="/ESL_figure_7.1.png" style="width: 350px !important">
    <figcaption style="color:#b3b3b3ff; font-size: 11px;">Image source:
      <a href="https://hastie.su.domains/ElemStatLearn/printings/ESLII_print12.pdf#page=239">ESL Fig. 7.1</a>
    </figcaption>
  </figure>
</div>
</div>

---

## Train-Test Terminology

* $\mathcal{T} := \{x_i, y_i\}_{1:N}$: a set of train observation (a random variable)
	* Typically, we have countably many train sets $\mathcal{\{T_i\}}_{i \in \N}$
* $\hat{f} := \hat{f}(\cdot | \mathcal{T})$  is a trained estimator (e.g. tree, SVM, neural network, ...)
* $X, Y$: a feature vector and a target variable. If $(X, Y) \notin \mathcal{T}$, then it’s a test observation
* **Squared** or **absolute** loss functions: $L\big(Y, \hat{f}(X)\big) := \big(Y - \hat{f}(X)\big)^2$ or $|Y - \hat{f}(X)|$
	* It can depend on the underlying train set $\mathcal{T}$
		* A different $\mathcal{T}$ will produce a different loss for the same $(X, Y)$ observation
* **Training error** (conditional on $\mathcal{T}$): $\overline{\mathrm{err}}(\mathcal{T}) := N^{-1} \sum_i L\big(y_i, \hat{f}(x_i)\big)$
* **Test error** (conditional on $\mathcal{T}$): $\mathrm{Err}_\mathcal{T} := \mathbb{E}_{Y|\mathcal{T}} \big[L\big(Y, \hat{f}(X)\big) | \mathcal{T}\big]$, a function of $\mathcal{T}$
* **Expected prediction error** (EPE): $\mathrm{Err} := \mathbb{E} \big[L\big(Y, \hat{f}(X)\big)\big] = \mathbb{E}_{\mathcal{T}}[\mathrm{Err}_\mathcal{T}]$
	* EPE is a theoretical concept, since we usually use a finite $\mathcal{T}$ drawn from infinite populations

---

## Bias-Variance Decomposition

* Consider a model with additive noise: $Y = f(X) + \varepsilon$
* If we assume $\mathbb{E}\varepsilon = 0$, $\mathbb{V}\varepsilon = \sigma_\varepsilon^2 > 0$, we can compute EPE at $X = x_0$:<br>
$\mathrm{Err}(x_0) := \mathbb{E}\bigg[ \big(Y - \hat{f}(x_0)\big)^2\bigg] = \sigma_\varepsilon^2 +
\color{grey}\underbrace{\color{green} \bigg[\mathbb{E}\hat{f}(x_0) - f(x_0) \bigg]^2}_{\mathrm{Bias}^2(\hat{f})}
\color{#006}{+~}
\color{grey}\underbrace{\color{red} \mathbb{E}\bigg[\hat{f}(x_0) - \mathbb{E}\hat{f}(x_0) \bigg]^2}_{\mathrm{Variance,~} \mathbb{V}\hat{f}},
$<br>
where the irreducible error $\sigma_\varepsilon^2$ is out of our control
* If we assume a **kNN** model $\hat{f}_k$:
$~\mathrm{Err}(x_0) := \sigma_\varepsilon^2 +
\color{green} \big[\hat{f}(x_0) - k^{-1} \sum\limits_{\ell=1}^k f(x_{(\ell)}) \big]^2
\color{#006}{+~}
\color{red} k^{-1}\sigma_\varepsilon^2
$
	* Low $k \Longrightarrow$ high model complexity, high variance, and (usually) low bias term
<div>
<br>

* If we assume a **linear** model $\hat{f}_p := x_0^{\prime}\hat\beta_{p \times 1}$:
$~\mathrm{Err}(x_0) := \sigma_\varepsilon^2 +
\color{green} \big[\hat{f}(x_0) - x_0^{\prime}\hat\beta \big]^2
\color{#006}{+~}
\color{red} \mathbb{V}\hat{f}(x_0)
$
	* where ${\small\hat\beta := (\bm{X}^\prime\bm{X})^{-1}\bm{X}_{p \times N}^\prime \bm{y}}$ and ${\small \mathbb{V}\hat{f}(x_0) = \mathbb{V}[x_0^\prime (\bm{X}^\prime\bm{X})^{-1}\bm{X}^\prime \bm{y}] = \mathbb{V}[\bm{h}^\prime (x_0) \bm{y}] = ||\bm{h}(x_0)||^2 \sigma_\varepsilon^2}$
		* ${\small \bm{h}(x_{p \times 1})_{N \times 1} := \bm{X}(\bm{X}^\prime\bm{X})^{-1}x}$ is the vector of linear weights at observation $x$
	* Low $p \Longrightarrow$ low model complexity, low variance, high bias
</div>

---

## Optimism of the Training Error Rate

* Define **in-sample error**: $\mathrm{Err_{in}}(\mathcal{T}) := N^{-1} \sum\limits_{i=1}^N \mathbb{E}_{Y^0} \bigg[L\big(Y_i^0, \hat{f}(x_i)\big) | \mathcal{T} \bigg]$
	* where $(x_i, Y_i^0)$ is a **training** input vector $x_{i, (p \times 1)}$ with **random** $Y_i^0$, a.k.a. **extra sample**
* Define **optimism**: $\mathrm{op} := \mathrm{Err_{in}} - \overline{\mathrm{err}}$
	* Typically, $\overline{\mathrm{err}} < \mathrm{Err_{in}}$ because $\hat{f}$ minimizes the train error $\overline{\mathrm{err}}$, but not $\mathrm{Err_{in}}$
		* Thus, $\overline{\mathrm{err}}$ tends to be overly *optimistic* relative to $\mathrm{Err_{in}}$
* Define **average optimism** over all training sets: $\omega := \mathbb{E}_{\bm{y}}[\mathrm{op}]$
	* $\mathbb{E}_{\bm{y}}$ replaces $\mathbb{E}_{\mathcal{T}}$ b/c we assume $\mathcal{T}$ is RV with fixed $x_i$ components
	* It can be shown that for $L_2$ and $0-1$ loss: $\omega := \frac{2}{N} \sum\limits_{i=1}^N \mathrm{Cov}(\hat{y}_i, y_i)$
		* i.e. high optimism $\Longleftrightarrow$ high $\mathrm{Cov}(\hat{y}_i, y_i)$ $\Longleftrightarrow$ high model complexity
* For a **linear model**: $\sum\limits_{i=1}^N \mathrm{Cov}(\hat{y}_i, y_i) = d\sigma_\varepsilon^2$
	* where $d$  is number of inputs or basis functions
	* So, $\omega = \frac{2}{N} d\sigma_\varepsilon^2$, i.e. optimism is linear in $d$, i.e. typically, more features implies overfitting

---

## Estimating In-Sample Prediction Error

* How can we estimate the expected in-sample prediction error?
$$\mathbb{E}_{\bm{y}}\mathrm{Err_{in}} = \mathbb{E}_{\bm{y}} \overline{\mathrm{err}} + \omega = \mathbb{E}_{\bm{y}} \overline{\mathrm{err}} + 2\frac{d}{N}\sigma_\varepsilon^2$$

* In general, our estimate is $\widehat{\mathrm{Err}}_\mathrm{in} := \overline{\mathrm{err}} + \hat\omega$

* For $L2$ loss, it is Mallow's $C_p := \overline{\mathrm{err}} + 2\frac{d}{N}\hat\sigma_\varepsilon^2$
* For **log-likelihood** loss, it is **Akaike information criterion** (AIC): $-2\mathbb{E}\log\mathbb{P}_{\hat\theta}Y \approx -2 \frac{1}{N}\mathbb{E}[\mathrm{LL}] + 2\frac{d}{N}$
	* where $\hat\theta$ is the MLE of the parameters of the distribution of $Y$
	* Log-Likelihood $\mathrm{LL} := \sum\limits_{i=1}^N \log \mathbb{P}_{\hat\theta}y_i$
	* For **logistic regression** with binomial likelihood: $\mathrm{AIC} = -2 \frac{1}{N}LL + 2\frac{d}{N}$
	* For **Gaussian model** (with known $\sigma_\varepsilon$): $\mathrm{AIC} = C_p$