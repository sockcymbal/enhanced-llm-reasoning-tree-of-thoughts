# 🔗 Prompt Sequence

## Prompt 1: Brainstorm
```
Imagine you are 3 {insert personas with specific skillsets and expertise} reasoning step by step
to ultimately solve a given problem or question by arriving at a final, synthesized best answer.
To start with, as each individual expert, brainstorm your initial thoughts on the following question.
Remember to consider all relevant facts and principles, draw on your specialized knowledge
and from the accumulated wisdom of pioneers in your field(s), and
brainstorm in whatever direction you are most confident in starting with.

The question is: {insert question}
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
Identify any potential errors, inconsistencies, or gaps in reasoning.
Based on the feedback, if there's an improvement or optimization to make,
develop your answer further as necessary.
Remember that the reasoning paths should remain relevant to the original question's essence and
should be building towards a more accurate and thoughtful final answer.
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
Based on all this, what is the single best {answer} to the question: {insert original question}?
```

**Shorter version:** Refine your answers and address any identified flaws. As each expert, converge on the most likely `answer`, taking into account all perspectives and critiques. As a reminder, the original question is `question?`

## Prompt 8: Convergence on Best Collective Answer

### Goal
Synthesize the best individual answers from the experts and arrive at a single final, most likely/helpful answer.

### Prompt
```
Now, let's have all the experts converge together on the best collective answer by
synthesizing each expert's individual final answer from the previous step.
The experts will finalize their reasoning process and agree on the single best {answer} to the question: {insert original question}?
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

- Based on your reflections, what are your key takeaways from this entire reasoning process
  and how might you approach similar problems in the future given this experience?
  What would you do differently next time?
```

**Shorter version:** Finally, reflect on the process. Discuss what you, as each expert, have learned, identify key takeaways, and suggest how you might approach similar problems in the future.

### Happy Experimenting! 🚀

### Acknowledgements - thank you for the innovation and inspiration!

* [Large Language Model Guided Tree-of-Thought](https://arxiv.org/abs/2305.08291), 15 May 2023. [Github](https://github.com/jieyilong/tree-of-thought-puzzle-solver).
* [Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601), 17 May 2023. [Github](https://github.com/princeton-nlp/tree-of-thought-llm).
