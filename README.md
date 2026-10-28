# TEAL - SkillComposer Take-Home Assignment

Thank you for your interest in the TEAL Lab! I am John Woods, a PhD student under the direction of Dr. Hasti Seifi. To assess your technical skills, we ask you to please complete this take-home problem.

## 1. Background

In SkillComposer, robots can be programmed using primitive functions, such as moving to an object, grasping it, moving to a new location, and releasing it. These functions can be combined to perform more complex actions, so many robot programs end up containing repeated sequences of primitive functions.

To illustrate, consider the following Python program:

```python
grasp_object("Banana 1")
move_to_position(0.2, 0.0, 0.5)
release_object()

grasp_object("Banana 2")
move_to_position(0.3, 0.0, 0.5)
release_object()
```

Although the arguments differ, both sequences follow the same general structure: grasp an object, move it, and release it.

Instead of repeatedly generating this sequence, we can first create a reusable function (called a **macro**):

```python
def move_object(name, x):
    grasp_object(name)
    move_to_position(x, 0.0, 0.5)
    release_object()
```

The original program can then be shortened to:

```python
move_object("Banana 1", 0.2)
move_object("Banana 2", 0.3)
```

This process is called **library learning**: automatically identifying recurring program structures and converting them into reusable functions.

For more details on how SkillComposer currently implements library learning, **please read the full paper before beginning: [Paper](https://arxiv.org/pdf/2608.14944)**

## 2. Goal

Because Stitch operates on functional s-expressions instead of imperative robot programs, the macros it generates do not always correspond to valid imperative functions. This is what necessitated the substitution and filtering steps in the original work.

**Your goal is to research and implement a different algorithm for finding repeated sequences of functions and converting them into macros.**

## 3. Tasks

### A. Research Two Methods

Describe two distinct methods for detecting or selecting repeated function sequences. You may either search existing literature for ideas or come up with your own. For each, explain the main idea in your own words, give a small worked example, cite your sources, and discuss expected benefits and limitations. Explicitly identify how each method changes or extends the current SkillComposer pipeline.

### B. Implement One Method

Your implementation should:

1. Read a JSON file containing a list of robot programs and identify recurring contiguous sequences.
2. Create macros containing at least two primitive calls.
3. Rewrite programs using the learned macros, preserving call order and all argument values.
4. Export the learned macro schemas to a file

The program JSON files are provided in this repository in the `data` directory. It also contains the function schemas for the five SkillComposer primitives for your reference and use. Please fork this repository to use as a starter for your implementation.

### C. Evaluate and Interpret the Results

Compare your implemented method with the SkillComposer results reported in the paper.

Create a spreadsheet that reports the following for each of the 40 provided programs:

| Column                    | Definition                                        |
| ------------------------- | ------------------------------------------------- |
| **Rewritten program**     | The raw program rewritten with learned macros.    |
| **Old program length**    | Number of function calls before rewriting.        |
| **New program length**    | Number of function calls after rewriting.         |
| **Macro usage (%)**       | `100 × macro calls / program length`.             |
| **Number of macros**      | Number of learned macros at that point.           |

Feel free to report any additional metrics that you feel are relevant to your approach.

## 4. Deliverables

- **Code and README:** Include all code files necessary to run your implementation in the repository and create a README describing any setup, commands, settings, and dependencies your code needs.
- **Outputs:** Evaluation spreadsheet described above
- **Report:** In your report, describe the two methods you came up with, your choice with justification, an explanation of your implementation, how your approach differs from SkillComposer, evaluation results, examples of learned macros, successes and failures, limitations of your approach, and a future experiment you would like to run.
- **Disclosure:** List any external code, libraries, or AI assistance used. Also include time spent on this assignment and anything you didn't get to finish.

Our goal is to assess your problem-solving capabilities, understand your thinking process, and see how you approach research, so please make that clear in your deliverables.

To submit, please respond to the email you were sent with the link to your forked repository.

## 5. Suggested Reading

1. Matthew Bowers et al. **Top-Down Synthesis for Library Learning.** This is the paper that introduced Stitch and may be helpful reading to get a better understanding of how it works. [Paper](https://doi.org/10.1145/3571234).
2. Craig G. Nevill-Manning and Ian H. Witten. **Compression and Explanation using Hierarchical Grammars.** If you're looking for a place to start your research, I would recommend checking this out. [Paper](https://academic.oup.com/comjnl/article-abstract/40/2_and_3/103/360801).
