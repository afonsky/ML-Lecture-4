## Scikit-Learn

<div class="grid grid-cols-2">
<div>
Has convenient set of tools for splitting samples

* Some can also shuffle
</div>
<div>
	<img src="/Scikit_learn_splitting_tools.png" style="width: 550px;">
</div>
</div>

---

# Ex. Wrong & Right way to use CV

* <span style="color:red">**Wrong way**</span>:
	* Say, we have $X_{N \times 1M}$ and do the following:
		1. Find the most explanatory predictors, $\tilde{X}_{N \times 100}$
		2. Build a classifier using $\tilde{X}$
		3. Use CV for grid search and test error estimation

* The problem is that we used **ALL** observations (training and testing) to choose features
<br>
<br>


* <span style="color:green">**Correct way**</span>:
	* Identify K folds and do CV:
		1. Find the most explanatory predictors, $\tilde{X}_{N \times 100}$
		2. Build a classifier using  $\tilde{X}$
		3. Estimate the test error

