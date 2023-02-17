# ETL4DSc

This project provides an interface for business teams to manage ETL processes that enables reporting and data science solutions.

Interface also provides the following functionality:
* easy to use etl jobs definition and scheduling
* job based definition and documentation (who created, for which tasks, reports, projects, etc)
* generation of new columns for existing tables (inheriting existing jobs to create additional columns for already existing jobs)
  * JOB123 > KEY_FIELD1, KEY_FIELD2, FIELD3, FIELD4
  * JOB546(JOB123) > FIELD5
  * new job wont duplicate existing one, but add new column just for the forking user. 
  * New column can be private or public.
* post field generation
  * Existing fields: FIELD1, FIELD2
  * Post fields: round(FIELD1/FIELD2,3) as FIELD1_SOW
* ready to use analytic fields
  * Kümülatif Toplam: 
    * partition cols: FIELD1, FIELD2, 
    * aggregation : count distinct
    * aggregate cols: FIELD3, 
* user based or public lookup tables
  * for a specific column lookup table may be different for different users
  * if the column is public and have multiple lookup tables for different users, then column name will be displayed with etl job suffix
* ready to use statistics and documentation
  * kaggle like summary information (for analyzed columns)
  * column based documentation (joins, filters, aggregations, etc to create that column, owner, wiki page link etc)
  * consumer projects and users
* easy to define quality rules, 
  * ready to use simple rules that user can enable with a single click
  * auto generated complex rules from calculated fields
  * quality result monitoring with minimum indicators, included in field documentation
