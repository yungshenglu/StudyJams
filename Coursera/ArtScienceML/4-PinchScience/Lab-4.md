# Lab 4: L1 Regularization

## Overview

In this L1 regularization lab, I had add in lots of spurious features and it created a fairly complex model. We're first going to train the model without L1 regularization, and then we will see if L1 regularization helps pulling the model down into a much more sparse, concise, and hopefully more generalizable form.

---
## TensorFlow Playground

1. Access the lab link below to the TensorFlow Playground.
    * https://goo.gl/281mPF
2. Try training with and without L1 regularization. What’s the difference?
3. Tune back into the video for a walkthrough.

---
## Lab Review

* With L1 regularization
    * The useless features all go to zero
* Without L1 regularization
    * The useless features retain some value
    * The only features that survived were $x^2$ and $x^2$