# Sales Analytics — Technical Notes

This project explores CSV loading, SQL transformations, analytics, and incremental processing in Snowflake.

## Features practiced

- Loaded a retail CSV using an internal stage and COPY INTO.
- Used RAW_SALES and CLEAN_SALES to practice TRIM, UPPER, COALESCE, CASE, dates, joins, aggregations, and window functions.
- Practiced a scheduled Stream and Task separately from the main transformations.
- Explored JSON, VARIANT and FLATTEN in separate exercises.

## Notes for reviewers

The original CSV is not included; see [dataset notes](../data/README.md). The saved SQL worksheet is a commented archive of development experiments, not a runnable setup script. The separate examples have not been retested together.

Some SQL joins use ORDERNUMBER, which can repeat for order line items. One historical example filters out rows with a missing STATE. Those choices need review before using the queries with other data.

The archived worksheet contains statements that change database objects. Review any SQL before running it, preferably in a separate test database.
