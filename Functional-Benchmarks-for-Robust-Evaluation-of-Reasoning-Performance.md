## Functional Benchmarks for Robust Evaluation of Reasoning Performance, and the Reasoning Gap

[Paper link](https://arxiv.org/abs/2402.19450)

Use MATH dataset to rewrite the each static QA’s reasoning into code, whose inputs can be varied to create infinite versions that follow the same reasoning pattern, but the steps needed in each would be different. 

Functionalized 41.2% (2060/5000) of the MATH benchmark, with the subset chosen so as to fully cover the static QA **tests** solved by 4 closed-weight and 9 open-weight state-of-the-art (SOTA) models. 

**Reasoning gap:** The reasoning gap is the percent decrease in the accuracy between the static and functional variants.

 Example of functionalizing a test is provided in paper. Main idea is to express the QA in controllable python code, which uses python Math librarys to calculate the answers.

 ```
Text problem:
 The letters of the word ‘SIXTEEN’ are randomly arranged.
 What is the probability that the two E’s are not next to each other?
```
