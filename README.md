# ETL4DSc

This project provides a server based interface for business teams to manage ETL processes that enables reporting and data science solutions.

Interface also provides the following functionality:

## ETL Functionality
* Easy etl job creation and scheduling
* **Column Lake(TM)**, each colum calculated seperately with a set of dimension, this key(s) are stored as metadata of the column, all joins can be done over matcing keys of desired columns. Tool can propose similar columns with the same key similarity
* Job based definition and documentation, enable reusability, saving resources (who created, for which tasks, reports, projects, etc)
* Generation of new columns from existing tables (inheriting existing jobs to create additional columns for already existing jobs)
  * JOB123 > KEY_FIELD1, KEY_FIELD2, FIELD3, FIELD4
  * JOB546(JOB123) > +FIELD5
  * new job wont duplicate existing one, but add new column just for the forking user. 
  * New column can be private or public.
  * Sample loading for debugging (mod(IP_ID,1000)=1)
* Post field generation
  * Existing fields: FIELD1, FIELD2
  * Post fields: round(FIELD1/FIELD2,3) as FIELD1_SOW
* User based or public lookup tables
  * for a specific column lookup table may be different for different users
  * if the column is public and have multiple lookup tables for different users, then column name will be displayed with etl job suffix
* Ready to use statistics and documentation
  * kaggle like summary information (for analyzed columns)
  * column based documentation (joins, filters, aggregations, etc to create that column, owner, wiki page link etc)
  * consumer projects and users
  * Data lineage
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
  * create background staging tables to imporve performance
* Incremental load options
  * users can define queries to define incremental load subsets (```select date from calendar t1 join source t2 where t2.key_field is null```) 
  
## Data Science Functionality
* Data preperation functions
  * Data distribution detection
  * Propose functions for field modification according to the data characteristics
    * q-binning, log transformation, min-max scaling, standart scaling
    * imputation without modifying original data (org: FIELD1, imp: FIELD1_IMP0)
    * all transformations are no code ready to use, user can select by just clicking
  * Anomaly detection on fields
    * IQR testing
    * Background co-existance controls
  * Simple on-the-go clustering with one click
  * One time calculatin, public fields can be reuasable, (strict documentation required)
* Ready to use analytic fields
  * Kümülatif Toplam (sum over): 
    * partition cols: FIELD1, FIELD2, 
    * aggregation : count distinct
    * aggregate cols: FIELD3, 
  * Lag/Lead
  * Moving Average, (3/6/9/12 ortalama)
  * Last non null
  
## Data Governance Functionality
* Easy to define quality rules, 
  * ready to use simple rules that user can enable with a single click
  * auto generated complex rules from calculated fields
  * quality result monitoring with minimum indicators, included in field documentation
* Governance integration
  * integrate with existing framework
  * provide a simple framework for DG 
* Naming conventions
  * Provide field name proposals supporting the enterprise conventions
  * Define prefixes for each entity and table name to automatically add suffix added column names in joins
    * Entity Name: VOLUMES, suffix: VOL_
    * Table Name: DEPOSITS, suffix: DPS_
    * Field Name: TERM_DEPOSIT, calculation sum(case when CURRENCY='TL' ), 
    * Proposed Name: VOL_DPS_TERM_DEPOSIT_AMOUNT_TL
    * Field Name: TERM_DEPOSIT, count(distinct IP_ID)
    * Proposed Name: VOL_DPS_TERM_DEPOSIT_NUM_CUSTOMER
* Quick search terms
  * List tree based (entity, table, field, related reports, projects, charts, etc)
    
## Data Publishing Functionality
* Publishing
  * Add simple D3JS charts at the end of etl tasks
  * Provide mash-up like report and presentation pages
  * Flask or dash based drilldown reporting fascility
  * Enable advanced users modify chart code
  * Publish report pages to others
  * Populate data inside predefined excel templates
  * Email summary reports to defined audiences
  * API gateway for integrating with other application 

## Integration Functionality
* Python integration
  * Add python functions to make transformations on data
  * Run model prediction (like model deployment)
    * Model performance monitoring & reporting
  * Model prediction by API
* Office integraiton
  * Excel integration
    * Run recorded excel makro's for the given set of data loop
    * Upload-Merge-Split excel using the data reside in db
    * format (copy format from existing excel)
  * Power Point integration
    * manipulate source data of the prepared ppt (python-pptx)
* External data integration
  * Inflation rates, currency conversions
  * TUIK statistics
  * Data marketplace, enable data developers sell processed data through the marketplace
  * Web scraping
    * Scraping scheduling (bs4 & selenium)
    * NLP support, named entity tagging
* IOT integration
  * Python listener from microcontrollers (REPL)
