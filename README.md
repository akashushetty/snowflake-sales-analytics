# Snowflake Sales & Orders Analytics

**Snowflake SQL | CSV | Data Cleaning | Analytics | Streams & Tasks**

I used a sample retail sales dataset to practice loading, cleaning, and analyzing data in Snowflake. The project began as a SQL worksheet where I tried different features and queries while learning.

## What I worked on

- Loaded a sales CSV into a RAW table using an internal stage, file format, and `COPY INTO`.
- Created CLEAN-table transformations using `TRIM`, `UPPER`, `COALESCE`, and `CASE`.
- Wrote queries using joins, aggregations, window functions, and date functions.
- Practiced Streams and a scheduled Task to insert new order IDs into a separate table.
- Explored JSON data using `PARSE_JSON`, `VARIANT`, and `FLATTEN` in a separate exercise.

## Data flow

```text
Retail sales CSV
       |
Snowflake internal stage
       |
     COPY INTO
       |
    RAW_SALES
       |
 SQL transformations
       |
   CLEAN_SALES
       |
Analytics queries
```

I practiced Stream/Task-based incremental loading and JSON analysis separately. They are not connected into one automated workflow in this repository.

## Project files

- `sql/sales_project_history_NON_EXECUTABLE.sql` — original SQL exercises, preserved as comments
- `sql/01_setup_example_NOT_RETESTED.sql` — example sandbox setup
- `sql/02_read_only_analysis_examples.sql` — sample analysis queries
- `data/README.md` — notes on the source dataset
- `docs/` — technical notes and limitations

## Getting started

Read [the dataset notes](data/README.md) and use a separate Snowflake test database. The original retail CSV is not included, so you will need a permitted copy with the expected columns.

The historical worksheet is **for reading, not for running as one script**. The separate example SQL files have not yet been retested together in a fresh Snowflake environment.

This is a learning project based on hands-on SQL practice, not a production pipeline. See [technical notes](docs/SAFETY_AND_EVIDENCE.md) for details.
