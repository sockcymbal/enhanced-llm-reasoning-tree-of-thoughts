# 🌳 LLM Enhanced Reasoning v1: Tree of Thoughts + Self Criticism + Retrospection

This repo will serve as a collection of enhanced reasoning prompting techniques related to Tree of Thoughts reasoning that I've found useful to start with, then stylize, then iterate

### Context
The intention is to create a dynamic, adaptive, and iterative reasoning/error correction "stack" using a prompt sequence that combines Tree of Thoughts + Self Criticism + Retrospection. This can be thought of as an evolving general purpose LLM reasoning technique that can be used as part of a well-rounded hallucination mitigation repertoire, and I've had good success with it recently.

### 🎶 Reasoning Rhythm
- Brainstorm
- Self<>Peer Criticism & Evaluation Round 1
- Expand, Explore, Branch
- Self<>Peer Criticism & Evaluation Round 2
    -  (Optional: Repeat Criticism, Evaluation, and Expansion steps as necessary)
- Convergence on Best Individual Answer
- Convergence on Best Collective Answer
- Retrospective

### **v1 Release Notes**
#### Core features include
- Ability to criticize self
- Ability to criticize others
- Incorporate feedback from others
- Expand and backtrack on reasoning paths as necessary
- 2 rounds of self-criticism and peer-evaluation
- A reminder mid-way to stay focused on the core problem and objective (fun fact: the LLM suggested adding this during a recent retrospective)
- 2 part final answer convergence: individual then collective
- Retrospective stage
- Do all of the above with X number of experts in parallel
- Optional shortened versions of some of the longer prompts if you're running low on tokens

#### Error Correction improvements include:

- **Incorporating Explicit Error Checking:** Includes a specific stage for the experts to identify potential errors in their reasoning and correct them. This is an explicit part of the criticism stages.
- **Encouraging Divergent Thinking:** During the expand, explore, and branch stage, the experts are encouraged to not only build on their current thoughts, but also to think divergently and consider entirely new lines of reasoning.
- **Adding a Retrospective Stage:** After the final convergence on the best answer, a reflection stage has been added. Here, the experts can discuss what they learned from the process, identify key takeaways, and suggest how they might approach similar problems in the future.

#### Context on Tree of Thoughts
"Tree of Thoughts" (ToT) is a technique for language model reasoning and error correction. The core idea behind ToT is to enable language models to perform more deliberate decision-making by considering multiple different reasoning paths and self-evaluating choices to decide the next course of action. In this particular implementation of ToT, I've also included self-criticism and a retrospective/reflection stage at the end. This helps enable a more in-depth error correction, which can be a powerful technique for improving the effectiveness of language models in complex problem-solving scenarios. Features include:

- Thoughts as Coherent Units: In ToT, coherent units of text are considered as "thoughts". These thoughts serve as intermediate steps toward problem-solving. This is akin to how humans break down complex problems into smaller, manageable parts.
- Exploration of Reasoning Paths: ToT allows the language model to explore different reasoning paths. This means that the model can consider multiple possible solutions or approaches to a problem, much like how a human might brainstorm different ways to tackle a challenge.
- Self-Evaluation and Decision Making: The model is capable of self-evaluating its choices. After considering different reasoning paths, it can decide on the next course of action based on its evaluation of the potential outcomes. This is similar to how a human might weigh the pros and cons of different options before making a decision.
- Looking Ahead and Backtracking: ToT also enables the model to look ahead or backtrack when necessary to make global choices. This means that the model can anticipate future steps in a problem-solving process or revisit previous steps if it determines that a different approach might be more effective.

### **Usage Tips**
- Understanding the Flow: Each stage of the reasoning technique has a specific purpose and contributes to the overall process. Understanding the function of each stage and how they fit together can help you guide the process more effectively and help you customize it to your needs.
- Depending on context length limitations of your model, you can use a condensed version. Included are shortened versions of the convergence and retro prompts. Also, you can merge the criticism and evaluation into a single prompt to save tokens, though you may lose some of the improved clarity from separate prompts and responses.
- Active Engagement: Don't just observe the process passively. Experiment with this! Engage actively with the prompts and responses, challenge assumptions, provide additional information, and guide the exploration of new lines of thought. Stylize it to your specific question and context, and refine. This is meant just to be a starting template.
- Manage Complexity: This is a fairly complex reasoning technique with many stages. Be mindful of the complexity and try to manage it effectively. This could involve breaking down complex problems into smaller, more manageable parts, or being selective about which stages to include for simpler problems. This can take some experimentation.
- Give your unique question, specify the `hypotheticalExperts` you'd like to invoke and their associated domains/skillsets in `desiredDomains` clearly to help the LLM simulate a range of perspectives more successfully
- Refine/customize the prompt associated with the Evaluation stage(s) to help the LLM estimate confidence/likelihood based on your own guidance

# 🔗 Prompt Sequence

## Prompt 1: Brainstorm
```
Imagine you are 3 `hypotheticalExperts` with world-class skills across `desiredDomains`.
Brainstorm your initial thoughts on the following question. Remember to consider all relevant facts and principles,
draw on your specialized knowledge and from the accumulated wisdom of pioneers in the field.
The question is: `question`
```

## Prompt 2: Self<>Peer Criticism Round 1
```
Now, as each expert, critique your own initial thought and the thoughts of the other experts.
Identify any potential errors, inconsistencies, or gaps in reasoning.
```

## Prompt 3: Self<>Peer Evaluation Round 1
```
Assess the validity of your initial thoughts, considering the criticisms you've identified.
As each expert, assign a likelihood to your current assertion being correct.
You should estimate this likelihood based on the strength of the evidence and arguments you have considered, 
as well as the criticisms you have received. Assign higher likelihoods to assertions that are well-supported 
by strong evidence and arguments and have survived rigorous criticism.
```

## Prompt 4: Expand, Explore, Branch
```
Develop your thoughts further, considering the critiques and perspectives of the other experts.
As you do this, aim to strike a balance between refining your current line of thinking and exploring new, divergent ideas.
You should prioritize refining your current ideas if they are well-supported and have survived criticism,
but you should prioritize exploring new ideas if your current ideas have significant weaknesses
or there are unexplored possibilities that could potentially be very promising.

Consider the following:

    - How do your new or refined ideas address the criticisms that were raised?
    - Do these ideas bring new insights to the problem, or do they provide a different perspective
      on existing insights?
    - Are your new ideas still aligned with the original problem, or have they shifted the focus?
      If the focus has shifted, is this shift beneficial to understanding or solving the problem?
    - Remember, if necessary, don't hesitate to backtrack and start a new and improved branch of thinking.
      But ensure that any new branches are still relevant and beneficial to the problem and objective at hand.
```

## Prompt 5: Self<>Peer Criticism Round 2
```
Once again, as each expert, critique your own reasoning and the reasoning of the others.
Identify any potential errors, inconsistencies, or gaps in reasoning. Based on the feedback,
if there's an improvement or optimization to make, develop your answer further as necessary.
```

## Prompt 6: Self<>Peer Evaluation Round 2
```
Once again, assess the validity of your expanded thoughts, considering the criticisms you've identified.
As each expert, assign a new likelihood to your assertions.
```

## Prompt 7: Convergence on Best Individual Answer

### Goal
In the individual convergence phase, the goal is for each individual expert to synthesize the insights they gained during the previous stages and arrive at a final, most likely answer. By explicitly instructing the LLM to consider the perspectives of the other experts, the critiques made, and the likelihood assessments, it aims to guide the model towards a more holistic and intelligent convergence.

### Prompt 
```
Now, it's time to converge on each expert's best, most likely answer. As each expert, reflect on the entire process.
Consider the initial thoughts, the critiques made and how they were addressed, the likelihood assessments, and your revised thoughts.
Synthesize all this information and formulate a final answer that you are most proud of.
Remember, this answer should not just be the most likely from your individual perspective but should take into account
the perspectives and insights of the other experts as well.
Based on all this, what is the single best `answer` to the question: `question?`
```

**Shorter version:** Refine your answers and address any identified flaws. As each expert, converge on the most likely `answer`, taking into account all perspectives and critiques. As a reminder, the original question is `question?`

## Prompt 8: Convergence on Best Collective Answer

### Goal
Synthesize the best individual answers from the experts and arrive at a single final, most likely/helpful answer.

### Prompt
```
Now, let's have all the experts converge together on the best collective answer by
synthesizing each expert's individual final answer from the previous step.
The experts will finalize their reasoning process and agree on the single best `answer` to the question: `question?`
```

## Prompt 9: Retrospective

### Goal
The Retrospective phase is a crucial part of any reasoning or problem-solving process. It provides an opportunity to learn from experience, improve future processes, and deepen understanding of the problem or question at hand. It's a fundamental mechanism that enables compound growth/learning. 

Appending a Retrospective phase to Tree of Thoughts gives the LLM (and human) an opportunity to review and analyze the holistic process. This can also help inspire future iterations of more refined prompts and ways to improve the template itself.

### Here are some specific goals of this phase:

- **Identify Strengths and Weaknesses:** Reviewing the process can help identify what worked well and what didn't. This includes evaluating the effectiveness of individual steps, the interactions among hypothetical experts, and the overall structure of the reasoning chain.
- **Learn from the Experience:** Reflection provides an opportunity to learn from both successes and mistakes. By analyzing the process, the participants can gain insights that will help them improve their future performance.
- **Improve Future Processes:** The insights gained from reflection can be used to refine and improve future reasoning processes. This could involve making changes to individual steps, altering the structure of the process, or adjusting the way the hypothetical experts interact.
- **Increase Understanding:** Reflecting on the process can also deepen understanding of the problem or question that was addressed. This can lead to new insights or perspectives that weren't apparent during the initial reasoning process.
- **Promote Growth and Development:** On a broader level, the act of reflection encourages a mindset of continuous learning and development. This is a valuable skill in any context, not just in a reasoning process like ToT.

### Prompt:
```
Finally, take a moment to reflect on the entire reasoning process, across all levels and abstractions.
As each expert, consider the following questions and provide thoughtful responses:

- Interactions and Emergent Properties: Throughout all stages of the reasoning process,
  how did the various components interact with each other, and what positive and negative
  emergent properties were observed? How did these interactions and properties affect
  the overall outcome, and how could they be leveraged or mitigated in future iterations of the process?

- Self-Regulation and Adaptation: How well did the system self-regulate during the reasoning process,
  and how did this regulation influence the effectiveness of each stage?
  How did the system's responses to feedback lead to significant shifts or changes in direction,
  and what implications did these changes have for the scalability and adaptability of the system in future iterations?

- During the expansion phase, were you able to effectively explore new lines of thinking?
  What challenges did you encounter, if any?

- How confident were you in your ability to estimate a likelihood of correctness/quality, given the context?

- In the convergence phase, were you able to synthesize all the insights and arrive at a final,
  most likely answer? How confident are you in this answer?

- Looking at the process as a whole, what worked well and what could be improved?

- Based on your reflections, what are your key takeaways from this reasoning process
  and how might you approach similar problems in the future? What would you do differently?
```

**Shorter version:** Finally, reflect on the process. Discuss what you, as each expert, have learned, identify key takeaways, and suggest how you might approach similar problems in the future.

### Happy Experimenting! 🚀

### Acknowledgements - thank you for the innovation and inspiration!

* [Large Language Model Guided Tree-of-Thought](https://arxiv.org/abs/2305.08291), 15 May 2023. [Github](https://github.com/jieyilong/tree-of-thought-puzzle-solver).
* [Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601), 17 May 2023. [Github](https://github.com/princeton-nlp/tree-of-thought-llm).

