## Bootstrap

* Used to quantify uncertainty or distribution of an estimator or model parameters
* Toy example: consider a sample $x = {1,2,3,4}$ with $\bar{x} = 2.5$ and $s_x \approx 1.29$
	* We can even compute the [standard error](https://en.wikipedia.org/wiki/Standard_error) of sample mean is $s_{\bar{x}} = \frac{s_x}{\sqrt{n}} \approx 0.65$
		* What is the distribution of $\bar{x}$?
	* We can’t estimate the distribution b/c we only have a single observation of
	* Theory states that $\bar{x}$ is approaches Gaussian with mean $\bar{x}$ and std. dev. $s_{\bar{x}}$
		* In many complex situations, theory can’t estimate the distribution of parameters and estimators
* Resampling: we can generate $B$ bootstrap samples $z^{*1}, ..., z^{*B}$
	* Compute mean, $\hat{\mu}^{*i}$, on each $z^{*i}$
	* Examine distribution of these bootstrap means

---

## Bootstrap

* Bootstrapping is resampling with replacement.
	* It helps estimating distribution of the estimators, which otherwise would only be observed once
* We draw $B$ bootstrap samples, $\{\bm{Z}^{\ast b}\}_{1:B}$ from $\bm{Z} = \{z_i\}_{1:N}$, $z_i := (x_i, y_i)$
* $S(\bm{Z})$ is any statistic of interest ($\mathbb{E}z$, $\mathbb{V}z$, $\hat{y}$, $\beta$, ...)
<div class="grid grid-cols-[2fr,2fr]">
<div>

* With bootstrap samples we can estimate the distribution of $S(\bm{Z})$<br>
$\hat{\mathbb{V}}S(\bm{Z}) := \frac{1}{B - 1} \sum\limits_{b=1}^B \big[S(\bm{Z}^{\ast b}) - \bar{S}^2 \big]^2$

</div>
<div>
    <figure>
    <img src="/ESL_figure_7.12.png" style="width: 420px !important">
    <figcaption style="color:#b3b3b3ff; font-size: 11px;">Image source:
      <a href="https://hastie.su.domains/ElemStatLearn/printings/ESLII_print12.pdf#page=269">ESL Fig. 7.12</a>
    </figcaption>
  </figure>
</div>
</div>