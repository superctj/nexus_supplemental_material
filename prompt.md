```python
# System prompt:
"You are a data management expert that only replies with JSON."


# Prompt for entity type inference:
"--- Column 1 ---
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
"--- Pair 1 ---
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
```
