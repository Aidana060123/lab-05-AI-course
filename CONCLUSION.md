# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

Layer 1 changed the results the most. The bare agent had 16 correct answers out of 24, while layer 1 had 18. It helped the agent recover from tool errors and answer questions about different region names. Layer 2 did not change the results. Layer 3 also kept 18 correct answers, but reduced wrong answers from 6 to 4. It changed two wrong answers into no answers. However, the confidence intervals for the bare agent [0.47, 0.82] and layer 1 [0.55, 0.88] overlap, so the improvement is not statistically proven with this small sample. After adding my memory notes, the result improved to 22 correct answers out of 24. The notes helped the agent understand region names and calculation rules. Layer 1: Correct answers increased from 16 to 18, wrong answers increased from 4 to 6, and no answers decreased from 4 to 0. The agent stopped failing when a tool returned an error. It could try again. 
Layer 1 changed what the agent can do. Now it can see tool errors and try again instead of stopping. The agent answered q23 and q24 correctly, but q21 and q22 changed from no answer to wrong answers.
Layer 3 changed what the agent admits. It still had 18 correct answers, but it changed two wrong answers into no answers because they were not supported by the tool results.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

The full harness did not fix q17. The question asked how many percentage points the unemployment rate in Aktobe decreased between 2020 and 2023. The correct calculation was 4.5 - 4.1 = 0.4 percentage points. However, the agent calculated a percentage change and answered 8.89. The grounding check did not catch this mistake because the number came from the calculate tool. This shows that an answer can use a tool and still be wrong. I would add a check to make sure the correct formula is used for percentage points. This check could need extra model calls, more tokens and more time. It could also make mistakes and reject correct answers.  The agent made a mistake when selecting the formula for the `calculate` tool. He used a percentage change formula instead of simple subtraction.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

I would choose a workflow for monthly rankings because it gave better results on fixed questions. It answered 13 out of 15 questions correctly, while the bare agent answered 9 out of 15. The workflow also used fewer model calls (15 vs. 26), fewer tokens (3852 vs. 19835) and less time (15.7 vs. 49.8 seconds). This is because the workflow follows fixed steps and sends shorter requests to the model. The agent sends more context and needs more calls to choose tools and give answers. However, a workflow cannot answer open-ended questions. For these questions, I would choose an agent because it can make decisions and use different tools depending on the task.



---

I wrote this file myself, without any AI tool.
