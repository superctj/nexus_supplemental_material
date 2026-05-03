# Supplemental Material for Nexus: Inferring Join Graphs from Metadata Alone via Iterative Low-Rank Matrix Completion

## Summary
`prompt.md` contains the prompts used for join graph inference, and the code for extracting token usage details from LLM responses.

  - API: Azure OpenAI chat completion API
  - Model: GPT-4o (2025-01-01-preview)
  - Batch size (for join prediction, entity type annotation, and soft matching) per LLM call: 16
  - Max tokens for LLM responses: batch size * 30

`supplemental_material.pdf` includes additional material complementary to the main paper.
