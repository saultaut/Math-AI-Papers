## Orca-Math: Unlocking the Potential of SLMs in Grade School Math

[Orca-Math Paper](https://arxiv.org/abs/2402.14830)

Orca-Math achieves 86.81% pass@1 on GSM8K while trained on only 200K synthetic math problems. Orca-Math, a 7-billion-parameter SLM based on the Mistral-7B model, incorporates the following key elements:

1. A high-quality synthetic dataset created using a multi-agent setup (teacher-student paradigm).
2. Learning from preference pairs that incorporate the SLM solutions and feedback.

This approach is a distillation of the GPT-4 model, which achieves 97.0% pass@1 on GSM8K. The OVM model, Mistral 7B+7B, shows an accuracy of 84.7% on verify100@1.

### Orca-Math Dataset

Orca-Math dataset, a synthetic dataset of 200K math problems, is paired with GPT-4-Turbo solutions, showcasing an innovative way to paraphrase existing problems and expand the problem set in both diversity and difficulty.

### Answer extraction

Given a model generated answer, we prompt GPT4 to extract the final short answer and match it with the gold short answer.
Opinion: This is very costly.

### Small Model Performance

Small models from other researchers show strong results: Phi-GSM+V Phi-1.5 1.3B+1.3B code achieves 81.5% verify48@1.

### Innovative Problem Paraphrasing

A good method for paraphrasing problems uses the subsequent prompt:

```
Your goal is to create multiple word problems from a given word problem and
its answer. First, convert the question of the word problem into a statement.
Then, for each number in the converted problem, create a new word problem.
```

This method involves taking any number from the solution and generating a question for this solution.

#### Iterative Learning from Both Positive and Negative Signals

We fine-tune Mistral-7B for up to three iterations. In the first iteration, we use supervised fine-tuning to obtain M1. For the second iteration, use the KTO trained model, call this M2, and use M2 to generate the dataset for iteration #3. This approach differs from OVM, which uses just a single iteration to generate labels.

##### Positive and Negative Data Generation

Both positive and negative solutions are very important. If the model correctly solved the problem, add negative solutions from other questions.

##### Dataset Details

1. To generate additional positive and negative solutions for each problem, we sample four responses from the SFT-tuned model from iteration #1. For all solutions where the student-generated answer does not match the teacher's answer, we label them as negative; otherwise, we label the solution as positive.

Negative solutions can be empty if all 4 responses are aligned with the teacher's solution. For such situations, randomly sample one response from other negative solutions for 4 different questions in the negative solutions dataset.
