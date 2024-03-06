## Functional Benchmarks for Robust Evaluation of Reasoning Performance, and the Reasoning Gap

[Paper link](https://arxiv.org/abs/2402.19450)

Use MATH dataset to rewrite the each static QA’s reasoning into code, whose inputs can be varied to create infinite versions that follow the same reasoning pattern, but the steps needed in each would be different. 

Functionalized 41.2% (2060/5000) of the MATH benchmark, with the subset chosen so as to fully cover the static QA **tests** solved by 4 closed-weight and 9 open-weight state-of-the-art (SOTA) models. 

**Reasoning gap:** The reasoning gap is the percent decrease in the accuracy between the static and functional variants.

**Gap = 58-80% for SOTA models **

Example of functionalizing a test is provided in paper. Main idea is to express the QA in controllable python code, which uses python Math librarys to calculate the answers.


 ```
Text problem:
 The letters of the word ‘SIXTEEN’ are randomly arranged.
 What is the probability that the two E’s are not next to each other?
```

The problem expressed in the python code:

```Python
def problem(word: str)-> str:
    prb = f"The letters of the word ‘{word}’ are randomly arranged."
          f"What is the probability that the two E’s are not next to each other?"
    return prb

def solution(word: str)-> str:
    length = len(word)
    # The numerator is always 2 less than the length of the
    # random string- 2 being the length of the string ’EE’
    numerator = length- 2
    # Resulting denominator will always be the length of the string
    denominator = length
    # Simplifying the fraction
    common_factor = math.gcd(numerator, denominator):
    if common_factor > 1:
        numerator //= common_factor
        denominator //= common_factor
    return f"\\dfrac{{{numerator}}}{{{denominator}}}"

def inputs(rngs, seed):
    rngs.set_seed(seed)
    # The string is made up of three parts, pre + ’EE’ + post
    # We keep the string ’EE’ constant to align with original problem
    # ....
```
