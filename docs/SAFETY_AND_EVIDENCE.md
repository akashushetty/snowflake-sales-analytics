# Sales source audit, scope, and evidence

## Source reviewed
- `Sales_data_project.zip` contained **one** SQL file (`Sales_data_project.sql`). No Python program, original retail CSV, environment file, or actual Snowflake connection parameters were supplied within this ZIP.
- This repository is prepared from that source. The original ZIP was not modified.

## Publication edits
- Fully comment out the historical SQL so its `CREATE OR REPLACE DATABASE`, account-level grants, Task RESUME, and warehouse ALTER commands cannot run if the file is selected as a whole.
- Replace a personal name occurring inside an illustrative JSON object with `Sample Customer`.
- Remove unrelated trailing Wing file-format/stage commands from the public historical archive.
- Add a read-only analytics example and a separate non-destructive initial setup example. These new examples are **not live-retested**.
- No source retail CSV is included; licensing and customer-data rights must be checked by the owner before uploading any dataset.

## Evidence boundaries
- Stage/COPY, RAW/CLEAN transformations, CASE region logic, joins, windows, and date exercises are present in the original SQL worksheet.
- JSON parsing and flattening are separate in the worksheet and not part of an independently verified automated load.
- Private exported Task History examined for resume review showed `SALES_PROJECT.LOAD_INCREMENTAL_SALES` succeeded on **2026-09-01** with an **INSERT of 2 rows**. It was a warehouse-backed Task.
- No source files establish a fully automated production pipeline, Snowpipe, serverless Tasks, dbt, Airflow, AWS S3 integration, enterprise-scale performance, or verified idempotent MERGE.
- No fresh Snowflake run was performed in preparing this GitHub kit.

## Review notes from static SQL inspection
- Order numbers may repeat across order line items; the saved worksheet includes joins and updates by `ORDERNUMBER`. Those joins can multiply rows if the keys are not unique.
- The source references `GRANT EXECUTE TASK` and `GRANT OWNERSHIP` as learning experiments, which require elevated permissions and must not be copied blindly.
- The historical worksheet includes a mismatched column query, duplicated `WHERE` clauses, and a stray comma in a SELECT. Treat it as an experimental lab notebook rather than polished runnable code.
- Historical `CREATE OR REPLACE` operations could delete objects if executed outside the fully commented archival version.
