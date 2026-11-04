# Sales Analytics — Technical Notes

This project uses a retail sales CSV and Snowflake SQL for ingestion, data cleaning, analytics, and separate incremental-processing exercises.

## What was practiced

- Loaded a 25-column CSV through an internal stage and `COPY INTO`, using an ISO-8859-1 CSV file format.
- Worked with `RAW_SALES`, `CLEAN_SALES`, text cleanup, `COALESCE`, `CASE`, date functions, joins, aggregations, and window functions.
- Tested a warehouse-backed scheduled Stream/Task INSERT that added two order IDs to an incremental target.
- Explored JSON with `PARSE_JSON`, `VARIANT`, and `LATERAL FLATTEN` in a separate exercise.

## Current limitations

- The original retail CSV is not included. See [dataset notes](../data/README.md) to obtain and check a permitted copy.
- The original development worksheet is preserved entirely as comments so it cannot be executed accidentally. The separate setup and analytics examples have not yet been retested together.
- Several historical statements were exploratory, may depend on earlier steps, and should not be treated as a complete setup-to-output script.
- Some queries join on `ORDERNUMBER`, which can appear on more than one order line. These joins may multiply records unless the correct line-item key is used.
- One historical transformation filtered out rows with a NULL `STATE`. That was a particular exercise choice, not a general data-cleaning rule.
- The historical worksheet includes account grants, warehouse changes, and `CREATE OR REPLACE` commands. It is **reference material, not a script to run wholesale**.

Streams/Tasks and JSON analysis were practiced separately from the main sales transformation exercise. The repository does not demonstrate a complete production automation workflow.
