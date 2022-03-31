---
title: Reversing Neural Networks
date: 31-03-2022
---

What if you could run a deep learning model in reverse? Train up an MNIST classifier, and get the "perfect" image representation of the number 5?

# Questions
- You can't inverse the ReLu function, right?

## Inversing ReLu
If using tanh instead of relu, the inverse is 
$\frac{1}{2}*\log_2(\frac{(1+x)}{(1-x)})$

