# ETL4DSc

This project provides an interface for business teams to manage ETL processes that enables reporting and data science solutions.

Interface also provides the following functionality:

* Easy etl job creation and scheduling
* Job based definition and documentation (who created, for which tasks, reports, projects, etc)
* Generation of new columns for existing tables (inheriting existing jobs to create additional columns for already existing jobs)
  * JOB123 > KEY_FIELD1, KEY_FIELD2, FIELD3, FIELD4
  * JOB546(JOB123) > FIELD5
  * new job wont duplicate existing one, but add new column just for the forking user. 
  * New column can be private or public.
* Post field generation
  * Existing fields: FIELD1, FIELD2
  * Post fields: round(FIELD1/FIELD2,3) as FIELD1_SOW
* Ready to use analytic fields
  * Kümülatif Toplam: 
    * partition cols: FIELD1, FIELD2, 
    * aggregation : count distinct
    * aggregate cols: FIELD3, 
* User based or public lookup tables
  * for a specific column lookup table may be different for different users
  * if the column is public and have multiple lookup tables for different users, then column name will be displayed with etl job suffix
* Ready to use statistics and documentation
  * kaggle like summary information (for analyzed columns)
  * column based documentation (joins, filters, aggregations, etc to create that column, owner, wiki page link etc)
  * consumer projects and users
* Easy to define quality rules, 
  * ready to use simple rules that user can enable with a single click
  * auto generated complex rules from calculated fields
  * quality result monitoring with minimum indicators, included in field documentation
* Temporary materialized views and archiving snapshots
  * for specific tasks or one time projects create static views 
  * ready to re-run and reproduce up-to-date versions 
* Tree based sub reports generated from source etl job
  * naming of sub reports: JOB123.Analyze1, JOB123.Analyze2
  * each report automatically updates when to source table is reloaded, unless Analyze is protected, if so a new copy is produced as a new version
* Easy to define performance options
  * **parallelization**: split data with partitions or indexes in the source table, auto retrieve this information from db 
  * **load balancing**: propose better schedule times to reduce overall running time
  * **merge similar jobs**: merge or extend similar jobs from different users and generate the same field only for once.
* Naming conventions
  * Provide field name proposals supporting the enterprise conventions
  * Define prefixes for each entity and table name to automatically add suffix added column names in joins
    * Entity Name: VOLUMES, suffix: VOL_
    * Table Name: DEPOSITS, suffix: DPS_
    * Field Name: TERM_DEPOSIT, calculation sum(case when CURRENCY='TL' ), 
    * Proposed Name: VOL_DPS_TERM_DEPOSIT_AMOUNT_TL
    * Field Name: TERM_DEPOSIT, count(distinct IP_ID)
    * Proposed Name: VOL_DPS_TERM_DEPOSIT_NUM_CUSTOMER
