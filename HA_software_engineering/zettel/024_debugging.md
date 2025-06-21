# Debugging

## Core Insight
The detective work of finding where intention met reality, the humbling practice of discovering our own mistakes.

Debugging is the investigation of mysteries we ourselves created. It begins with a contradiction: the code should work (we wrote it correctly) yet doesn't work (reality disagrees). This gap between expectation and observation drives the debugging process. Like detectives at a crime scene, debuggers gather evidence, form hypotheses, test theories, and slowly narrow down the space of possibilities until the culprit is found.

The essence of debugging is the scientific method applied to code. Observe the symptom. Form a hypothesis about the cause. Design an experiment to test it. Run the experiment. Revise the hypothesis based on results. This cycle repeats until understanding emerges. Print statements, debuggers, and logging are tools for observation. Binary search through code history isolates when bugs appeared. Systematic variation of inputs reveals patterns. Each technique adds evidence to the investigation.

Debugging reveals the gap between our mental models and reality. The bug exists because our understanding was incomplete or incorrect. We thought the function would be called once but it's called twice. We assumed the data was sorted but it wasn't. We believed the types matched but they didn't. Each bug fixed is a mental model corrected, a lesson learned about the difference between what we assumed and what actually is.

The psychology of debugging is as important as the technique. Frustration clouds judgment. Assumptions blind us to obvious errors. Pride prevents us from questioning our own code. The best debuggers cultivate humility and curiosity. They assume the bug is their fault (it usually is). They question everything, especially the "impossible." They know that the most baffling bugs often have embarrassingly simple causes - a typo, an off-by-one error, a misunderstood API. The computer is always right; the challenge is understanding what we actually told it to do.

## Connections
→ [[testing]]
→ [[state]]
→ [[condition]]
→ [[loop]]
← [[bug]]
← [[code]]

---
Level: L2
Date: 2025-06-21
Tags: #investigation #problem-solving #humility #learning