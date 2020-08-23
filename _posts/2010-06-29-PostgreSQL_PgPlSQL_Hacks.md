---
title: PostgreSQL PgPlSQL Hacks
permalink: index.php/PostgreSQL_PgPlSQL_Hacks/
layout: single
categories: postgres
---

Moving rows between 2 tables
----------------------------

These two functions can move data between two tables.

The first version realises that with a cursor: Please note the row
`query := 'INSERT INTO ' || target || ' VALUES (($1::text::' ||
target::regclass || ').\*)';` and how the values pasted into the
statement. 

Dont't forget to use `quote\_ident(...)` - so the function
isn't vulnerable for SQL-injections
{: .notice--warning}

``` sql

CREATE OR REPLACE FUNCTION moveToParent(sourceTable VARCHAR, 
        sourceTableSchema VARCHAR, targetTable VARCHAR, targetTableSchema VARCHAR )

RETURNS text VOLATILE AS $$
DECLARE
        r RECORD;
        curs refcursor;
        query VARCHAR;
        delStmt VARCHAR;
        target  VARCHAR;
        source VARCHAR;
BEGIN
        target := '"' || quote_ident(targetTableSchema) || '".' || quote_ident(targetTable);
        source := '"' || quote_ident(sourceTableSchema) || '".' || quote_ident(sourceTable);

        OPEN curs NO SCROLL FOR EXECUTE 'SELECT * FROM ONLY ' || source;
        LOOP
                FETCH curs INTO r;
                EXIT WHEN NOT FOUND;
                        query := 'INSERT INTO ' || target || ' VALUES (($1::text::' || target::regclass || ').*)';

                EXECUTE query USING r;
                delStmt := 'DELETE FROM ONLY ' || source || ' WHERE CURRENT OF $1'; 
                EXECUTE delStmt USING curs; 
        END LOOP;

        CLOSE curs;

        RETURN 'done';

END; 
$$ LANGUAGE plpgsql;
```

A much more elegant version, which should also be more efficient:

``` sql

CREATE OR REPLACE FUNCTION moveToParent(sourceTable VARCHAR,
        sourceTableSchema VARCHAR, targetTable VARCHAR, targetTableSchema VARCHAR )

RETURNS text VOLATILE AS $$
DECLARE
        target  VARCHAR;
        source VARCHAR;
BEGIN
        target := '"' || quote_ident(targetTableSchema) || '".' || quote_ident(targetTable);
        source := '"' || quote_ident(sourceTableSchema) || '".' || quote_ident(sourceTable);


        EXECUTE 'INSERT INTO ' || target || ' SELECT * FROM ONLY ' || source; 

        EXECUTE 'DELETE FROM ONLY ' || source;

END; 
$$ LANGUAGE plpgsql;
```
