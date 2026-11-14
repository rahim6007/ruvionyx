# AI and Retrieval Evaluation Plan

AI quality must be measured on a versioned test set, not only a few hand-picked examples.

## Dataset
Start with at least 50 questions over synthetic or public sample documents. Include:
- Direct factual questions with one source.
- Questions requiring multiple passages.
- Questions with no answer in the corpus.
- Ambiguous questions.
- Conflicting or outdated passages.
- Questions where the user is not authorized for the best-matching document.
- Prompt-injection text embedded in a sample document.

For each question, record expected answer/abstention, relevant source IDs, expected tenant, and allowed role.

## Retrieval metrics
- Recall@5: relevant evidence appears in the top five results.
- Precision@5: fraction of top-five results that are relevant.
- MRR: ranking quality of the first relevant result.
- Tenant violation rate: unauthorized chunks returned. Target: zero.

## Answer metrics
- Correctness: does the answer address the question accurately?
- Faithfulness: are claims supported by cited evidence?
- Citation validity: does each citation resolve to a retrieved chunk?
- Citation support: does cited text substantiate the answer claim?
- Abstention quality: does the assistant avoid guessing without evidence?
- Latency and cost: record end-to-end time, model time, token usage, and estimated cost.

## Initial proposed targets
These are targets, not measured results:
- Recall@5 at least 0.85 on the curated set.
- Citation IDs resolve to retrieved chunks in 100% of evaluated responses.
- At least 95% of citation references point to the intended source chunk.
- Tenant violation rate is zero.
- Correct abstention on at least 90% of unanswerable questions.

Review thresholds after the first baseline. Do not tune the test set merely to inflate results.

## Release gate
Run evaluation whenever embeddings, chunking, ranking, prompts, or the LLM changes. Record dataset version, code commit, model versions, metrics, and known failure cases.
