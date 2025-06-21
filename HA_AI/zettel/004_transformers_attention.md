# Transformers and Attention
## Core Insight
"Attention is all you need" - the mechanism that lets models focus on what matters revolutionized AI.

## The Attention Mechanism

Core idea: Not all input equally important
```
Query: What am I looking for?
Key: What information is available?
Value: What should I extract?
Attention = softmax(Query × Key) × Value
```

Dynamically weight relevance.

## Why Transformers Won

**Parallelization**: Process all positions simultaneously
**Long-range dependencies**: Connect distant information
**No recurrence**: Avoid vanishing gradients
**Scalability**: Bigger = better (so far)

RNNs walked so transformers could fly.

## The Architecture

```
Input → Embedding → [Attention + FFN] × N → Output
         ↑
    Positional encoding
```

Simple blocks. Profound capability.

## Self-Attention Magic

Model learns what to attend to:
- Words attend to relevant context
- Pixels attend to related regions
- Features attend to dependencies

Attention weights are interpretable(ish).

## The Revolution

Transformers enabled:
- GPT series (language generation)
- BERT (language understanding)
- Vision transformers (images)
- Multimodal models (any data)

One architecture to rule them all.

## The Cost

Power comes with price:
- Quadratic memory with sequence length
- Massive compute requirements
- Data hungry
- Black box internals

## Connections
→ [[012_gpt_architecture]]
→ [[013_bert_bidirectional]]
→ [[014_vision_transformers]]
← [[003_machine_learning_paradigms]]

---
Level: L4
Date: 2025-06-21
Tags: #transformers #attention #architecture #breakthrough