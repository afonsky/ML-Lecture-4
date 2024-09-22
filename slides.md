---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /ship2.jpg
attribution: Photo by <a href="https://unsplash.com/@bldjordan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jordan Billard</a> on <a href="https://unsplash.com/s/photos/mont-blanc?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
routerMode: hash
# some information about the slides, markdown enabled
info: |
  ## Slidev Personal Incubator
  NB: [Source code available](https://github.com/twitwi/slidev-incubation)

  Experimenting with new features for [Sli.dev](https://sli.dev)
# persist drawings in exports and build
ghPrefix: https://github.com/twitwi/slidev-incubation/blob/main/incubator/
drawings:
  persist: false
title: "Machine Learning"
subtitle: "Resampling Methods"
date: "23/09/2024"
venue: HSE
author: Alexey Boldyrev, Maksim Karpov
---

# <span v-html="$slidev.configs.title?.replaceAll(' ', '<br/>')"></span>
# <span v-html="$slidev.configs.subtitle?.replaceAll(' ', '<br/>')"></span>
# <span style="font-size:18.0pt" v-html="$slidev.configs.author?.replaceAll(' ', '<br/>')"></span>

<span style="font-size:18.0pt" v-html="$slidev.configs.date?.replaceAll(' ', '<br/>')"></span>

<div>
<br>
<span style="color:#b3b3b3ff; font-size: 11px; float: right;">Image credit: ‘The Mayﬂower at Sea’<br> by Granville Perkins, 1876<br>
Wallach Division Picture Collection<br> The New York Public Library.
</span>
</div>

<style>
  :deep(footer) { padding-bottom: 3em !important; }
</style>

---
src: ./slides/2_what_is_resampling.md
---

---
src: ./slides/3_validation_set_approach.md
---

---
src: ./slides/shuffling_and_iid_assumption.md
---

---
src: ./slides/train_validate_test.md
---

---
src: ./slides/validation_error.md
---

---
src: ./slides/validation_error_averaging.md
---

---
src: ./slides/loocv.md
---

---
src: ./slides/k_fold.md
---

---
src: ./slides/cv_on_a_simulated_dataset.md
---

---
src: ./slides/bias_variance_tradeoff.md
---

---
src: ./slides/k_fold_cv_in_classification.md
---

---
src: ./slides/bootstrap.md
---

---
src: ./slides/bootstrap_toy_example.md
---

---
src: ./slides/bootstrap_toy_example_more_samples.md
---

---
src: ./slides/se_of_bootstrap.md
---

---
src: ./slides/cv_for_time_series.md
---

---
src: ./slides/cv_for_group_data.md
---

---
src: ./slides/stratified_k_fold.md
---

---
src: ./slides/scikit_learn_shuffle_tools.md
---

---
src: ./slides/bias-variance_decomposition.md
---

... nope

# The END
