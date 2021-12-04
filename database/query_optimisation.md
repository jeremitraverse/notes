# QUERY OPTIMISATION

## DATA SELECTION BY KEY
- Sweep (FULL TABLE SCAN)
  - Sequentilly reading all the blocks in a table
  - Things to consider
    - Amount of blocks in a table
    - Time that take the head to reposition itself. Can't block a process for a large amount of 
      time, so we break the read when other request have to be made
  - Situation when it's acceptable to make a full table scan
    - When we have a small table
    - Reading from a intermediary table
      - Result of a select
      - When the table doesn't have an index
      - When there's no other options
