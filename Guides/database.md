# PostgreSQL

- `\list` or `\l`: list all databases

- `\c <db name>`: connect to a certain database

- `\dt`: list all tables in the current database

- This deletes all rows and resets identity sequences

  ```sql
  TRUNCATE TABLE your_table RESTART IDENTITY;
  
  ```

  