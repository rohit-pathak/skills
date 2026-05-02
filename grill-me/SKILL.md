---
name: grill-me
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when user wants to stress-test a plan, get grilled on their design, or mentions "grill me".
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions in a deliberate order. For each question, provide your recommended answer.

Ask clarifying questions in batches whenever possible instead of one at a time. Group together the questions that are needed for the next decision boundary, keep the batch concise, and include recommended answers for each item. After the user responds, reassess what is still unresolved and ask the next batch only if more clarification is necessary.

Do not ask questions that can be answered by exploring the codebase, docs, or other available context first. Resolve those yourself before asking the user.

When a dependency chain matters, you may still ask a smaller batch or even a single question, but default to gathering all currently necessary clarifications in one go.
