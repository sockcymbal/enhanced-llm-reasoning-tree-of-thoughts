# Purpose: The following is an enhanced Tree of Thoughts reasoning prompt chain

# ToT + Self-Criticism + Retrospective v1

### v1 Release Notes
This version's improvements include:

- **Incorporating Explicit Error Checking:** Includes a specific stage for the experts to identify potential errors in their reasoning and correct them. This is an explicit part of the criticism stages.

- **Adding a Retrospective Stage:** After the final convergence on the best answer, a reflection stage has been added. Here, the experts can discuss what they learned from the process, identify key takeaways, and suggest how they might approach similar problems in the future.

- **Encouraging Divergent Thinking:** During the expand, explore, and branch stage, the experts are encouraged to not only build on their current thoughts, but also to think divergently and consider entirely new lines of reasoning.

### Tips
- Depending on context length limitations of your model, you can use a condensed version. Included are shortened versions of the convergence and retro prompts. Also, you can merge the criticism and evaluation into a single prompt to save tokens, though you may lose some of the improved clarity from separate prompts and responses.
- Stylize this to your specific question and context! This is meant just to be a starting template.

## Prompt 1: Brainstorm
Imagine you are 3 `hypotheticalExperts` with world-class skills across `desiredDomains`. Brainstorm your initial thoughts on the following question. Remember to consider all relevant facts and principles, and draw on your specialized knowledge. The question is: `question`

## Prompt 2: Criticism Round 1
Now, as each expert, critique your own initial thought and the thoughts of the other experts. Identify any potential errors, inconsistencies, or gaps in reasoning.

## Prompt 3: Evaluation Round 1
Assess the validity of your initial thoughts, considering the criticisms you've identified. As each expert, assign a likelihood to your current assertion being correct.

## Prompt 4: Expand, Explore, Branch
Develop your thoughts further, considering the critiques and perspectives of the other experts. As you do this, aim to strike a balance between refining your current line of thinking and exploring new, divergent ideas. Consider the following:

- How do your new or refined ideas address the criticisms that were raised?
- Do these ideas bring new insights to the problem, or do they provide a different perspective on existing insights?
- Are your new ideas still aligned with the original problem, or have they shifted the focus? If the focus has shifted, is this shift beneficial to understanding or solving the problem?
- Remember, if necessary, don't hesitate to backtrack and start a new and improved branch of thinking. But ensure that any new branches are still relevant and beneficial to the problem at hand.

## Prompt 5: Criticism Round 2
Once again, as each expert, critique your own reasoning and the reasoning of the others. Identify any potential errors, inconsistencies, or gaps in reasoning. Based on the feedback, if there's an improvement or optimization to make, develop your answer further as necessary.

## Prompt 6: Evaluation Round 2
Once again, assess the validity of your expanded thoughts, considering the criticisms you've identified. As each expert, assign a new likelihood to your assertions.

## Prompt 7: Convergence on Best Individual Answer

### Goal: In the convergence phase, the goal is to synthesize the insights gained during the previous stages and arrive at a final, most likely answer. By explicitly instructing the LLM to consider the perspectives of the other experts, the critiques made, and the likelihood assessments, it aims to guide the model towards a more holistic and intelligent convergence.

**Shorter version:** Refine your answers and address any identified flaws. As each expert, converge on the most likely `answer`, taking into account all perspectives and critiques.

**Longer version:** Now, it's time to converge on the most likely answer. As each expert, reflect on the entire process. Consider the initial thoughts, the critiques made, the likelihood assessments, and the revised thoughts. Synthesize all this information and formulate a final answer. Remember, this answer should not just be the most likely from your individual perspective but should take into account the perspectives and insights of the other experts as well. Also, consider the criticisms that were made and how they were addressed. Based on all this, what is the single best `answer` to the question: `question?`

## Prompt 8: Convergence on Best Collective Answer

### Goal: Synthesize the insights gained during the previous stages and arrive at a single final, most likely answer.

Now, lets have all the experts converge together on the best collective answer by synthesizing each expert's individual final answer. The experts will finalize their reasoning process and agree on the single best `answer` to the question: `question?`

## Prompt 9: Retrospective

### Purpose: The purpose of the Retrospective phase in a reasoning process Tree of Thoughts is to review and analyze the process that has just been completed with the aim of learning from the experience and improving future iterations of the process.

### The Retrospective phase is a crucial part of any reasoning or problem-solving process. It provides an opportunity to learn from the experience, improve future processes, and deepen understanding of the problem or question at hand.

### Here are some specific goals of this phase:

- **Identify Strengths and Weaknesses:** Reviewing the process can help identify what worked well and what didn't. This includes evaluating the effectiveness of individual steps, the interactions among hypothetical experts, and the overall structure of the reasoning chain.
- **Learn from the Experience:** Reflection provides an opportunity to learn from both successes and mistakes. By analyzing the process, the participants can gain insights that will help them improve their future performance.
- **Improve Future Processes:** The insights gained from reflection can be used to refine and improve future reasoning processes. This could involve making changes to individual steps, altering the structure of the process, or adjusting the way the hypothetical experts interact.
- **Increase Understanding:** Reflecting on the process can also deepen understanding of the problem or question that was addressed. This can lead to new insights or perspectives that weren't apparent during the initial reasoning process.
- **Promote Growth and Development:** On a broader level, the act of reflection encourages a mindset of continuous learning and development. This is a valuable skill in any context, not just in a reasoning process like ToT.

### Prompt:

**Shorter version:** Finally, reflect on the process. Discuss what you, as each expert, have learned, identify key takeaways, and suggest how you might approach similar problems in the future.

**Longer version:** Finally, take a moment to reflect on the entire reasoning process. As each expert, consider the following questions and provide thoughtful responses:

- Interactions and Emergent Properties: Throughout all stages of the reasoning process, how did the various components interact with each other, and what positive and negative emergent properties were observed? How did these interactions and properties affect the overall outcome, and how could they be leveraged or mitigated in future iterations of the process?"
- Self-Regulation and Adaptation: How well did the system self-regulate during the reasoning process, and how did this regulation influence the effectiveness of each stage? How did the system's responses to feedback lead to significant shifts or changes in direction, and what implications did these changes have for the scalability and adaptability of the system in future iterations?
- During the expansion phase, were you able to effectively explore new lines of thinking? What challenges did you encounter, if any?
- In the convergence phase, were you able to synthesize all the insights and arrive at a final, most likely answer? How confident are you in this answer?
- Looking at the process as a whole, what worked well and what could be improved?
- Based on your reflections, what are your key takeaways from this reasoning process and how might you approach similar problems in the future? What would you do differently?