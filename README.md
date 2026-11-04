# Snowflake Sales & Orders Analytics — Learning Portfolio

**Snowflake SQL · CSV ingestion · RAW/CLEAN transformations · analytical SQL · Streams and Tasks**

An independent learning portfolio documenting Snowflake SQL exercises on a retail sales dataset. The original saved project is a **development worksheet**, not one complete runnable pipeline. To avoid accidental account changes, its public archive is **fully commented out**; a separate safe setup template and read-only SQL examples are provided.

## Scope and what was practiced

- A 25-column sales CSV loaded using Snowflake internal stages, an ISO-8859-1 CSV file format, and `COPY INTO`.
- `RAW_SALES` to `CLEAN_SALES` transformations using `TRIM`, `UPPER`, `COALESCE`, date handling, and `CASE` business rules.
- SQL joins, grouping, window functions, ranking and country/region analytics.
- A separately practiced JSON/VARIANT/PARSE_JSON/LATERAL FLATTEN exercise. **This JSON example was not part of the main CSV ingestion workflow.**
- A separately defined `SALES_STREAM` and **warehouse-backed** scheduled Task to append new order IDs to an incremental target. The previously reviewed private Task History recorded **one successful scheduled INSERT of 2 rows on 1 September 2026**. That private account export is intentionally excluded.

## Repository layout

```text
README.md                                    Project summary and usage limitations
.gitignore                                  Excludes credentials, private exports, source CSVs
sql/sales_project_history_NON_EXECUTABLE.sql  Commented archive of earlier SQL experiments
sql/01_setup_example_NOT_RETESTED.sql          Fresh sandbox schema/stage example; not independently tested
sql/02_read_only_analysis_examples.sql        Read-only analysis examples; not independently tested here
data/README.md                              Dataset provenance and privacy notes
docs/SAFETY_AND_EVIDENCE.md                 Important limitations and audit findings
docs/PUBLISH_CHECKLIST.md                   Final publication steps
```

## How to use this repository

1. Review `docs/SAFETY_AND_EVIDENCE.md` and `data/README.md`.
2. Create a **dedicated trial/sandbox Snowflake database**, not a production database.
3. Review the setup example and create an internal stage, CSV file format, and RAW table. The example is not a tested one-command installer.
4. Obtain the original CSV yourself and check its permitted usage. **No source CSV is committed.**
5. Stage and load it manually, first using `VALIDATION_MODE = RETURN_ERRORS`. Validate row counts and the CSV header/type mapping before further work.
6. Run the read-only examples only after the data is loaded. Refer to the fully commented historical worksheet for other learning experiments; **do not uncomment/run it wholesale**.

## Architecture (conceptual)

```text
External retail sample CSV -> Snowflake internal stage -> RAW_SALES
                                                     -> SQL transformations -> CLEAN_SALES
                                                                          -> analytics
Separate exercise: CLEAN_SALES -> SALES_STREAM -> scheduled Task -> INCREMENTAL_CLEAN_SALES
Separate exercise: sample JSON -> PARSE_JSON / VARIANT -> LATERAL FLATTEN
```

## Important limitations

- This is **not** a production deployment, end-to-end orchestrated repository, or fully retested pipeline.
- The archived worksheet includes exploratory DDL, administrative grant commands, `CREATE OR REPLACE`, updates/deletes, active Task resume, and warehouse suspend/resume; all lines are commented so casual execution cannot perform those actions.
- The original source table has line-item/order-number semantics: do not treat `ORDERNUMBER` as a guaranteed unique key without investigating the underlying dataset.
- `CLEAN_SALES` excludes rows with NULL `STATE` in one historical transformation. This is a historical business rule, not a universally justified cleaning rule.
- Several worksheet SQL fragments are partial, contain errors, or depend on tables created in earlier experimentation. The two clean example scripts are **illustrations**, not evidence of a fresh complete execution.
- No customer data, private query history, real Snowflake account identifiers, or credentials are intentionally included.

**Portfolio honesty:** The documented successful scheduled Task was a 2-row warehouse-backed INSERT test, not a proof of large-scale production CDC or fully automated incremental reconciliation.
