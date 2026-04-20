```python
# Prompt for join prediction:
Left column:
- Column name: {left_col_name}
- Table name: {left_table_name}

Right column:
- Column name: {right_col_name}
- Table name: {right_table_name}

Evaluate the potential for joining the left column and the right column based on all provided details. Consider semantic meaning from column and table names.

Respond with a single, valid JSON object containing only one key: 'confidence'. The value for the 'confidence' key must be one of the strings: 'high', 'medium', or 'low'.

# Prompt for entity type inference:
--- Column 1 ---
Table: {table_name}
Column: {col_name}
--- Column 2 ---
Table: {table_name}
Column: {col_name}
...
------
What is the most likely entity type for each of these columns?
Give me a short label for each in the order they were provided.
Respond in a JSON format like {'entity_types': ['label1', 'label2', 'label3']}"


# Prompt for soft entity type matching:
--- Pair 1 ---
Left table: {table name}
Left column: {column name}
Left column entity type: {entity type}
Right table: {table name}
Right column: {column name}
Right column entity type: {entity type}
--- Pair 2 ---
Left table: {table name}
Left column: {column name}
Left column entity type: {entity type}
Right table: {table name}
Right column: {column name}
Right column entity type: {entity type}
...
------
For each pair listed above, do the two entity types match?
Provide your answers ('yes' or 'no') in a JSON format like {'match_results': ['yes', 'no', 'yes']}
**It is crucial that the order of the answers in the list matches exactly the order of the pairs as they were given in this prompt.**"


# Azure OpenAI API call to get LLM response and token usage details:
def get_llm_response(
    client, prompt: str, max_tokens: int
) -> tuple[str, int, int]:
    response = client.chat.completions.create(
        model=os.getenv("AZURE_OPENAI_MODEL"),
        response_format={"type": "json_object"},
        max_completion_tokens=max_tokens,
        messages=[
            {
                "role": "system",
                "content": "You are a data management expert that only replies with JSON.",  # noqa: E501
            },
            {"role": "user", "content": prompt},
        ],
    )

    # Extract token usage details if available
    response_dict = response.dict()
    num_input_tokens = response_dict.get("usage", {}).get("prompt_tokens", 0)
    num_output_tokens = response_dict.get("usage", {}).get(
        "completion_tokens", 0
    )
    if num_input_tokens == 0 or num_output_tokens == 0:
        logging.warning(
            "Token usage details are missing in the LLM response. Defaulting to 0 for both input and output tokens."  # noqa: E501
        )

    return response, num_input_tokens, num_output_tokens
```
