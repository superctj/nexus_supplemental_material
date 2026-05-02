# Supplemental Material for Nexus: Inferring Join Graphs from Metadata Alone via Iterative Low-Rank Matrix Completion

## LLM Prompts and Setup
`prompt.md` contains the prompts used for join graph inference, and the code for extracting token usage details from LLM responses.

  - API: Azure OpenAI chat completion API
  - Model: GPT-4o (2025-01-01-preview)
  - Batch size (for join prediction, entity type annotation, and soft matching) per LLM call: 16
  - Max tokens for LLM responses: batch size * 30

## XGBoost Features
For XGBoost, we trained on a large corpus of schemas from SchemaPile-Perm (Section 2.2 of our paper), utilizing a superset of metadata features from [1]. The features include containment/Jaccard similarity/edit distance ratio/jaro-winkler similarity of concatenated table and column name tokens, boolean indicators for column data types (integer and string), in addition to those used in [1].
