# DATA WAREHOUSING

- Use for analytic queries
- Periodical and coordinate copy of data from multiples sources into an optimized environment
  for analytical purposes 
- Subject oriented
  - What subject are we analyzing (sells, products, clients...)
- Rarely removing/updating data, always adding new entries
  - Out of date data are archived
- Using dedicated servers to reduce the load on the production servers 

### DATA SOURCES
- ERP
- CRM
- Legacy systems
- Point of sale

### Extract, Transform, Load (ETL)
- Extract data from heterogeneous sources
  - Periodical extraction, with timestamp
  - If no timestamp, keeping table locally and comparing with online database to 
    detect changes
  - Transaction journals
  - Trigger on source database
- Transform
  - Eliminating redondancy, missing data
  - Fusionning, conversion and aggregating data
  - Changing format
  - Decoding values
    - 0, 1 -> Men, Female
- Load
  - Batch loading and real time
- Longuest effort in developpement (70%)

### DATA MODELIZATION
- Star schema
  - Facts table surrounded by dimension tables
    - **Facts table** contains business mesurement
      - Create/keep columns (DD) that allow us to get the data
      - Keeps the FK of all dimensions table
      - Amount of sell, profit
    - **Dimension table** provides a context to the facts
      - Who, what, when, how, why
      - Corrolated attributs (1 -> 1, 1 -> *)
      - Data are descriptive
        - No abbreviation
      - Quality data
        - No redundancy
        - No missing data
      - Dimension hierarchy
        - Dimension are organize with categories and sub-categories
        - Always 1 -> 1 or 1 -> *
      - Temporal Dimension
        - Store temporal dimension more precise then a timestamp
          - Usually store the timestamps, year, month, day etc...
          - Devide into to dimension table
            - Date dimension
            - Time of day dimension into a sinle column
        - Slowly changing dimension
          - Dimension information usually doesn't change
          - Type 1 -> Overwritte data
            - Now impossible to analyze the data at a moment in the past
          - Type 2 -> Adding two column : effective and expired date
            - When updating a dimension entry, we create a new entry with the 
              updated values and changing the expired date
          - Type 3 -> Adding an old_ columns for each columns that we have that
            can change
  - Non-normalized data to reduce the amount of joins
  - PROS
    - Easier to understand
    - Increase performance
  
### DATA WAREHOUSE ARCHITECTURE
- **DATAMART BUS**
  - Datamart
    - Contains a part of the data warehouse content
    - Concentrate on only a single analytic subject 
    - Simple analysis and usually represented by a single star schema
  - Conceptual data warehouse formed of multiple datamart interlinked by some middlewares
  - Bottom-up approach where we create the most important datamart each time
  - Incremental approach (Agile)
- **HUB-AND-SPOKES**
  - Top-down approach
  - Hub contains all the normalized atomic data (3FN)
  - Spokes (datamarts) contains agregated data and following a dimensional model
    - Spokes are used for analytic queries
  - Takes a longer time to develop since we need a ETL
  - Better data quality then datamart bus
- **FEDERATED**
  - Data warehouse is distributed on multiple heterogeneous system
  - Data is added logicly or physicaly with the help of meta-data (XML configuration)
  - Used when we already have a data warehouse and we want to add a new one

### OPTIMIZING ANALYTIC QUERIES

#### STAR JOIN
- Use a BITMAP JOIN INDEX (Oracle)
- Instead of creating a BITMAP INDEX on the queried table, we create
  an index on the join table
  - If we join Inventory, Product and Supplier and we want to get the amount of stock
    for a given product and supplier, we can pass that product and that supplier to the index
    to get the information that we want without doing a full scan of the table inventory

#### PREAGREGATION
- From an atomic table, we create a agregated table based on popular queries
- **ROLAP**
  - Agregation by creating materialized view
  - Physical table sync with the query results in real time, batch or on demand
  - Since it's a view, we can create index
  - Possibility of creating an agregation hierarchy by creating views on top of another
- **MOLAP**
  - Use of multi-dimensional cube that represent data
  - Each axel of a cube represent an analytical dimension
    - Each position in the cube represent a analytical point
  - CONS
    - Takes a lot of storage
    - Most of the values will be 0
    - Need to compress those cube using sparse compression algorithm
    - Updating data can be expensive

### OLAP
- Operation that we can make on cube to analyze the data
  - Slice
    - Take a slice of the cube to analyze specific data
    - Where clause alike
  - Rotation
    - Rotate the cube on different axel to get different analysis
  - Drill-down
    - Start from the grain that you are currently and zoom in the next 
      dimension hierarchy grain. 
  - Roll-up
    - Start from the grain that you are currently and zoom out the previous
      dimension hierarchy grain
      

