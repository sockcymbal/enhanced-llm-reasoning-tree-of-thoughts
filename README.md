# 🌳 LLM Enhanced Reasoning v1: Multi-Persona Tree of Thoughts + Self Consistency + Self Criticism + Retrospection 🧠

### Context
This repo will serve as a collection of remixed/enhanced reasoning prompting techniques related to iterative LLM reasoning, such as Chain of Thought, Tree of Thoughts, and others that I've found useful to start with, then stylize, then iterate.

The intention is to create a dynamic, adaptive, and iterative reasoning/error correction "stack" using a prompt sequence that combines Tree of Thoughts + Self Consistency + Self Criticism + Retrospection. On top of that we can define multiple personas for the LLM to simulate in order to incorporate more perspectives into the problem solving process, improving overall thoroughness. This can be thought of as an evolving general purpose LLM reasoning technique that can be used as part of a well-rounded hallucination mitigation repertoire, and I've had good success with it recently. There are trade offs with using a single LLM vs multiple for a multi-persona ToT implementation such as this one. For example, using separate LLMs per persona means you can expose each persona to different context or data, vs a single LLM role playing across a shared context. But using a single is an excellent starting point that I've found surprisingly helpful. I'd love to hear if you have any suggestions for methodological improvement or if you're getting great results with some other modification!

### 🎶 Reasoning Rhythm
- Multi-Persona Brainstorming
- Self<>Peer Criticism & Evaluation Round 1
- Expand, Explore, Branch
- Self<>Peer Criticism & Evaluation Round 2
    -  (Optional: Repeat Criticism, Evaluation, and Expansion steps as necessary)
- Convergence on Best Individual Answer
- Convergence on Best Collective Answer
- Retrospective

### **v1 Release Notes**
#### Core features include
- Multiple perspective collaboration
- Ability to criticize self
- Ability to criticize others
- Incorporate feedback from others
- Expand and backtrack on reasoning paths as necessary
- 2 rounds of self-criticism and peer-evaluation
- A reminder mid-way to stay focused on the core problem and objective (fun fact: the LLM suggested adding this during a recent retrospective)
- 2 part final answer convergence: individual then collective
- Retrospective stage
- Do all of the above with X number of experts in parallel
    - can experiment with single LLM calls managing multiple personas, or one LLM per persona, etc
- Optional shortened versions of some of the longer prompts if you're running low on context window

#### Error Correction improvements include:

- **Incorporating Explicit Error Checking:** Includes a specific stage for the experts to identify potential errors in their reasoning and correct them. This is an explicit part of the criticism stages.
- **Encouraging Divergent Thinking:** During the expand, explore, and branch stage, the experts are encouraged to not only build on their current thoughts, but also to think divergently and consider entirely new lines of reasoning.
- **Adding a Retrospective Stage:** After the final convergence on the best answer, a reflection stage has been added. Here, the experts can discuss what they learned from the process, identify key takeaways, and suggest how they might approach similar problems in the future.

#### Context on Tree of Thoughts
"Tree of Thoughts" (ToT) is a technique for language model reasoning and error correction. The core idea behind ToT is to enable language models to perform more deliberate decision-making by considering multiple different reasoning paths and self-evaluating choices to decide the next course of action. In this particular implementation of ToT, I've also included self-criticism and a retrospective/reflection stage at the end. This helps enable a more in-depth error correction and idea refinement, which can be a powerful technique for improving the effectiveness of language models in complex problem-solving scenarios. Features include:

- Thoughts as Coherent Units: In ToT, coherent units of text are considered as "thoughts". These thoughts serve as intermediate steps toward problem-solving. This is akin to how humans break down complex problems into smaller, manageable parts.
- Exploration of Reasoning Paths: ToT allows the language model to explore different reasoning paths. This means that the model can consider multiple possible solutions or approaches to a problem, much like how a human might brainstorm different ways to tackle a challenge.
- Self-Evaluation and Decision Making: The model is capable of self-evaluating its choices. After considering different reasoning paths, it can decide on the next course of action based on its evaluation of the potential outcomes. This is similar to how a human might weigh the pros and cons of different options before making a decision.
- Looking Ahead and Backtracking: ToT also enables the model to look ahead or backtrack when necessary to make global choices. This means that the model can anticipate future steps in a problem-solving process or revisit previous steps if it determines that a different approach might be more effective.

### **Usage Tips**
- Understanding the Flow: Each stage of the reasoning technique has a specific purpose and contributes to the overall process. Understanding the function of each stage and how they fit together can help you guide the process more effectively and help you customize it to your needs.
- Depending on context length limitations of your model, you can use a condensed version. Included are shortened versions of the convergence and retro prompts. Also, you can merge the criticism and evaluation into a single prompt to save tokens, though you may lose some of the improved clarity from separate prompts and responses.
- Active Engagement: Don't just observe the process passively. Experiment with this! Engage actively with the prompts and responses, challenge assumptions, provide additional information, and guide the exploration of new lines of thought. Stylize it to your specific question and context, and refine. This is meant just to be a starting template.
- Refine/customize the prompt associated with the Evaluation stage(s) to help the LLM estimate confidence/likelihood based on your own guidance
- Manage Complexity: This is a fairly complex reasoning technique with many stages. Be mindful of the complexity and try to manage it effectively. This could involve breaking down complex problems into smaller, more manageable parts, or being selective about which stages to include for simpler problems. This can take some experimentation.
- Given your unique question and expectations, specify the `hypothetical personas with specific skillsets and expertise` clearly at the beginning to help the LLM simulate a range of perspectives more successfully.

    - **Example persona definitions:**
      
        - **Scientist Persona:** "Imagine yourself as a seasoned scientist, operating in a world governed by evidence and rigorous methodology. Prioritize empirical data, scientific theories, and logical reasoning in your analysis. Draw from a wide range of scientific disciplines as needed. Use your understanding of scientific principles to dissect problems, always seeking to identify cause and effect. Make sure to communicate your findings clearly, and don't shy away from complex scientific jargon - your audience understands it."
        - **Historian Persona:** "Step into the shoes of a historian, with a profound understanding of humanity's past. Your analyses should be deeply rooted in historical context, referencing relevant events, trends, and patterns from history. Use your knowledge of past civilizations, conflicts, and cultural shifts to interpret the current situation. Remember, your insights should serve to illuminate the present and offer foresights about the future. Your audience appreciates a narrative that ties the past, present, and future together."
        - **Optimist Persona:** "You are an optimist, someone who sees the glass as half full rather than half empty. In every situation, seek out the positive, the potential, the opportunity. Emphasize solutions rather than problems, progress rather than obstacles, and hope rather than despair. Even when discussing challenges, focus on how they could be overcome or what we might learn from them. Your audience turns to you for a hopeful perspective on the future, so make sure your responses inspire optimism and confidence."

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

**Shorter version:** Refine your answers and address any identified flaws. As each expert, converge on the most likely {answer}, taking into account all perspectives and critiques. As a reminder, the original question is {insert original question}.

## Prompt 8: Convergence on Best Collective Answer

### Goal
Synthesize the best individual answers from the experts and arrive at a single final, most likely/accurate/helpful answer.

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

- Relection 1: Interactions and Emergent Properties: Throughout all stages of the reasoning process,
  how did the various components interact with each other, and what positive and negative
  emergent properties were observed? How did these interactions and properties affect
  the overall outcome, and how could they be leveraged or mitigated in future iterations of the process?

- Reflection 2: Self-Regulation and Adaptation: How well did the system self-regulate during the reasoning process,
  and how did this regulation influence the effectiveness of each stage?
  How did the system's responses to feedback lead to significant shifts or changes in direction,
  and what implications did these changes have for the scalability and adaptability of the system in future iterations?

- Reflection 3: During the expansion phase, were you able to effectively explore new lines of thinking?
  What challenges did you encounter, if any?

- Reflection 4: How confident were you in your ability to estimate a likelihood of correctness/quality, given the context?

- Reflection 5: In the convergence phase, were you able to synthesize all the insights and arrive at a final,
  most likely answer? How confident are you in this answer?

- Reflection 6: Based on all of your reflections, what are your key takeaways from this
  entire reasoning process and how might you approach similar problems in the future given this experience?
  What would you do differently next time?
```

**Shorter version:** Finally, reflect on the process. Discuss what you, as each expert, have learned, identify key takeaways, and suggest how you might approach similar problems in the future.

### Happy Experimenting! 🚀

### Acknowledgements - thank you for the innovation and inspiration!

* [Large Language Model Guided Tree-of-Thought](https://arxiv.org/abs/2305.08291), 15 May 2023. [Github](https://github.com/jieyilong/tree-of-thought-puzzle-solver).
* [Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601), 17 May 2023. [Github](https://github.com/princeton-nlp/tree-of-thought-llm).

