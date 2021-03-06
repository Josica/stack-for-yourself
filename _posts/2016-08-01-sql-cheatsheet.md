---
layout: post
title: "SQL cheatsheet"
shortnote: "Cool SQL cheatsheet for SQL commands."
tags: [databases, back-end, all]
published: false
---

## Running from the console, and other things to know
To run SQLite3 from console:
sqlite3 [filename.sqlite]

Operators: [ =, !=, >, <, >=, <=]  # testing equality is done with one equal sign
Wildcards: [ * (any),
                     _ (inside string, meaning can be substituted for whatever),
                    % (inside string, meaning can be of any length or whatever after),

## Commands and syntax (remember to add the ';')

CREATE (makes new table)
CREATE TABLE (table name) (arg type, arg type, … etc);

INSERT (adds row)
INSERT INTO table (arg, arg, .. etc) VALUES (arg, arg, .. etc);

UPDATE (alters value in a row)
UPDATE table SET cell = new_value WHERE other_cell = something;

ALTER (adds column)
          ALTER TABLE table ADD COLUMN column_name TYPE;
          # => ALTER TABLE students ADD COLUMN grade INTEGER;

DELETE FROM (deletes rows)
         DELETE FROM table WHERE column IS VALUE;
         # => DELETE FROM students WHERE id IS NULL;

SELECT (pulls from table)
          SELECT column FROM table;

SELECT column, second_column FROM table;

SELECT DISTINCT genre FROM movies;

SELECT * FROM table WHERE column > VALUE;

SELECT * FROM table WHERE column LIKE ‘given_value’;

SELECT * FROM table WHERE column LIKE ‘a%’;

SELECT * FROM movies WHERE name BETWEEN 'A' AND 'J';

SELECT * FROM movies WHERE year BETWEEN 1990 AND 2000;
select * from movies where year between 1990 and 2000 and genre = 'comedy';

SELECT * FROM movies WHERE genre = 'comedy' OR year < 1980

SELECT * FROM movies ORDER BY imdb_rating DESC;

SELECT * FROM movies ORDER BY imdb_rating ASC LIMIT 3;

++ LIMIT : specifies how many items you want, maximum
++ ORDER BY spots results in ASC or DESC order

Aggregate functions:

          SELECT * FROM fake_apps;

          SELECT COUNT(*) FROM fake_apps;  # will return a count of the column
          # COUNT will count the num of rows for given column arg where value of cell is not NULL

          SELECT COUNT(*) FROM fake_apps WHERE price = 0;

          SELECT COUNT(*) FROM fake_apps WHERE price = 0; # returns two columns, one of price and second of count per price

          SELECT price, COUNT(*) FROM fake_apps WHERE downloads > 20000 GROUP BY price;

          SELECT SUM(downloads) FROM fake_apps; # returns total number of downloads

SELECT MAX(downloads) FROM fake_apps; # returns total downloads for most popular app

SELECT name, category, MAX(downloads) FROM fake_apps GROUP BY category;
  # returns most number of times an app has been downloaded, returns name and category columns

SELECT MIN(downloads) FROM fake_apps;

SELECT name, category, MIN(downloads) FROM fake_apps GROUP BY category;

SELECT AVG(downloads) FROM fake_apps;

SELECT price, AVG(downloads) FROM fake_apps GROUP BY price;

SELECT price, ROUND(AVG(downloads), 2) FROM fake_apps GROUP BY price;

Multiple tables

SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;

## Notes

Primary Key: column that serves as unique identifier for row in the table; values must be unique and not NULL
Foreign Key: column that contains the primary key to another table i the database, used to identify a particular row in referenced foreign table.
Joins: combine data from multiple table during queries.
INNER JOIN: combine rows from different tables if JOIN condition is true
LEFT OUTER JOIN return every row in the left table, and if join conditions are not met, NULL values are used to full in the columns from the RIGHT table.
AS is a keyword that allows you to rename a column or table using a given alias.
