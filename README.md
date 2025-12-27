# Text-to-SQL Cost Evaluation Dataset

This repository contains the experimental data from the paper:

**"Cost-Aware Text-to-SQL: Evaluating Cloud Compute Costs of LLM-Generated Queries"**

## Dataset Contents

### 1. `benchmark_questions.csv`
The 30 natural language questions used in our evaluation, categorized by complexity:
- **Simple (S1-S10)**: Single-table queries with basic filtering and aggregation
- **Medium (M1-M10)**: Multi-table queries with 2-3 joins and grouping
- **Complex (C1-C10)**: Queries requiring subqueries, window functions, CTEs, or 4+ table joins

### 2. `results_summary.csv`
Complete experimental results with the following columns:
- `Model`: LLM model name
- `Model_Type`: "Reasoning" or "Standard"
- `Question_ID`: Question identifier (S1-S10, M1-M10, C1-C10)
- `Complexity`: Simple, Medium, or Complex
- `Bytes_Processed_MB`: Total bytes scanned from storage
- `Slot_Seconds`: Compute resources consumed
- `Execution_Time_S`: Query execution time in seconds
- `Bytes_Shuffled_B`: Data moved between workers
- `Bytes_Spilled_B`: Data spilled to disk (0 for all queries)
- `Correct`: Y/N indicating query correctness
- `Cost_USD`: Estimated cost at $6.25/TB

### 3. `prompt_template.txt`
The complete prompt template used for all experiments, including:
- System instruction
- Full schema definitions for all 7 StackOverflow tables
- Foreign key relationships
- Notes on experimental methodology

### 4. Raw Model Results (in parent directory)
Individual CSV files for each model containing generated SQL queries:
- `AI Infra Benchmark - Opus 4.5 Thinking.csv`
- `AI Infra Benchmark - Sonnet 4.5.csv`
- `AI Infra Benchmark - GPT 5.1.csv`
- `AI Infra Benchmark - GPT 5.2 Reasoning.csv`
- `AI Infra Benchmark - Gemini 3 Flash.csv`
- `AI Infra Benchmark - Gemini 3 Pro (2).csv`

## Models Evaluated

| Model | Vendor | Type |
|-------|--------|------|
| Opus 4.5 Thinking | Anthropic | Reasoning |
| Sonnet 4.5 | Anthropic | Standard |
| GPT-5.2 High Reasoning | OpenAI | Reasoning |
| GPT-5.1 | OpenAI | Standard |
| Gemini 3 Pro Thinking | Google | Reasoning |
| Gemini 3 Flash | Google | Standard |

## Dataset

All experiments were conducted on Google BigQuery using the public StackOverflow dataset:
- **Dataset**: `bigquery-public-data.stackoverflow`
- **Size**: ~230 GB
- **Tables**: users, posts_questions, posts_answers, comments, badges, votes, tags

## Key Findings

1. **Reasoning models are 44.5% more cost-efficient** than standard models (p=0.003, Cohen's d=0.52)
2. **Execution time correlates weakly with cost** (r=0.16), invalidating speed as a cost proxy
3. **GPT-5.1 exhibited highest variance** with outliers exceeding 36GB per query

## Citation

If you use this dataset, please cite our paper:

```
@dataset{deochake2025texttosql_dataset,
  author       = {Deochake, Saurabh},
  title        = {{Cost-Aware Text-to-SQL: An Empirical Study of Cloud Compute Costs for LLM-Generated Queries}},
  month        = dec,
  year         = 2025,
  publisher    = {Zenodo},
  version      = {1.0},
  doi          = {10.5281/zenodo.18070764},
  url          = {https://doi.org/10.5281/zenodo.18070764}
}
```

## License

This dataset is released under the MIT License.
