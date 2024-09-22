## Validation Error (using *Auto* dataset)

* Consider a model $\mathrm{mpg}(\mathrm{hp}|\beta_0,\beta_1,d) = \beta_0 + \beta_1 \cdot \mathrm{hp}^d$
  * Predicts *miles per gallon* (mpg) from *horsepower* polynomial term
  * Goal: find $d \in \N$ with smallest (*true*) test MSE (estimated by validation MSE, **vMSE**) <br> $d:= \underset{d=1:10}{\mathrm{argmin}} \mathrm{\{MSE\}}_d \approx \underset{d=1:10}{\mathrm{argmin}} \mathrm{\{vMSE\}}_{d,\nu}$

    where $\nu$ is an index for the validation set of observations (**vSet**)

<div class="grid grid-cols-2">
<v-clicks>
<div>

* Problems:
  * $\mathrm{vMSE}_{d,\nu}$ depends on split (obs. in training set and validation set)
  * $\mathrm{vMSE}_{d,\nu}$ overestimates $\mathrm{vMSE}_{d}$
</div>
<div>
  <img src="/Validation_error.png" style="width: 550px;">
</div>
</v-clicks>
</div>