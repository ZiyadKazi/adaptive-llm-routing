# Adaptive LLM Routing

COMP 345 midterm project investigating whether question embeddings can
help select a smaller or larger language model for mathematics problems.

## Current progress

Implemented:
- Collection of real model responses through the Groq API
- Persistent response caching and resumable collection
- Final-answer extraction and mathematical-equivalence grading
- Manual review of unresolved grading cases
- Accuracy, estimated cost, and latency comparisons

Training and evaluating the learned router is planned for the next stage.

## Pilot setup

- Dataset: MATH algebra
- Sample: 50 questions from the official training split
- Random seed: 345
- Smaller model: openai/gpt-oss-20b
- Larger model: openai/gpt-oss-120b
- Temperature: 0
- Maximum completion tokens: 2,048

## Preliminary results

| Metric | Small model | Large model |
|---|---:|---:|
| Accuracy | 98% | 100% |
| Correct answers | 49/50 | 50/50 |
| Mean request latency | 0.855 s | 1.275 s |
| Estimated cost for 50 questions | $0.009272 | $0.015521 |

Always-small reduced estimated cost by 40.3%, with a two-percentage-point
accuracy decrease. These are baseline results, not learned-router results.

The only small-model failure was a response truncated before its final
answer. Actual API spending was zero on the free tier; reported costs
estimate paid deployment using the documented token rates.

## Files

- `MATH_Adaptive_Routing.ipynb`: executed experiment notebook
- `experiment_results/`: saved responses, grading records, and summaries

## Running the notebook

1. Open the notebook in Google Colab.
2. Run the dependency installation cells.
3. Mount Google Drive and confirm the project directory.
4. Enter your own Groq API key through the hidden input prompt.
5. Run the collection and grading cells.

Generation requires access to the specified Groq models and is subject
to account rate limits. Completed requests are cached and skipped on
subsequent runs.

The notebook currently expects results under:
`MyDrive/COMP345_Adaptive_Routing/`

To reuse the provided responses, copy the contents of
`experiment_results/` into that Drive folder before collecting.

Never put API keys in notebook source or commit them to GitHub.

## Limitations and next steps

This is a small development pilot, not a held-out evaluation of a trained
router. Next steps include broader data collection, router training,
validation-based threshold selection, and held-out baseline comparisons.
