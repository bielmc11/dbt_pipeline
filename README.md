# Netflix Ratings Pipeline

Data pipeline that extracts Netflix ratings CSV files from a storage bucket, ingests them into **Snowflake**, and transforms them using **dbt** following a **medallion architecture (bronze → staging → marts)**.

## Source Datasets

The CSVs contain movie ratings information:

| File               | Description                          |
|--------------------|--------------------------------------|
| `ratings.csv`      | User ratings for movies              |
| `movies.csv`       | Movie catalog                        |
| `tags.csv`         | Tags assigned by users               |
| `links.csv`        | External identifiers (IMDb, TMDB)    |
| `genome_score.csv` | Tag-movie relevance scores           |
| `genome_tags.csv`  | Genome tag descriptions              |

## Architecture (Medallion)

```
Bucket (CSVs) → Snowflake → dbt
                              ├── bronze    (raw layer, data as-is)
                              ├── staging   (cleaning, typing, normalization)
                              └── marts     (analytical models ready for consumption)
```

### Layers

- **Bronze**: Raw data ingested from CSVs without transformation.
- **Staging**: Cleaning, type casting, column renaming, and relationships.
- **Marts**: Aggregated models prepared for analysis and reporting.

## Tech Stack

- **Storage**: Object bucket (CSVs)
- **Data Warehouse**: Snowflake
- **Transformation**: dbt (data build tool)
- **Orchestration**: Python / scripts

## Usage

```bash
# Ingest CSVs to Snowflake
python main.py

# Run dbt transformations
dbt run

# Run tests
dbt test
```
