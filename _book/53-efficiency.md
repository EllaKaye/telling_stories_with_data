
# Efficiency

**Required material**

- Watch *Code smells and feels*, [@codesmells].
- Read *Notes from a data witch: Getting started with Apache Arrow*, [@navarro2021getting].

**Key concepts and skills**

- Refactoring code
- Developing an appreciation for SQL

**Key libraries**

- `arrow` [@arrow]
- `tictoc` [@Izrailev2014]

**Key functions**

- `arrow::read_parquet()`
- `arrow::write_parquet()`
- `tictoc::tic()`
- `tictoc::toc()`


## Introduction

For much of this book we have been largely concerned with just getting something done. Not necessarily getting it done in the best or most efficient way. To a large extent, being worried about getting something done in the best or most efficient way is almost always a waste of time. Until it is not. Eventually inefficient ways of storing data, ugly or slow code, and an insistence on using R do have an effect. And it is at that point that we need to be open to new approaches to ensure efficiency.

In this chapter we briefly cover ways to be more efficient with data, by using SQL, feather and parquet. We then discuss code efficiency, particularly, the need to measure and refactor code. Then we discuss experimental efficiency, in particular, the multi-armed bandit which enables us to more quickly test different effects. Finally, we briefly introduce other languages, such as Python and Julia, that have an important role to play in data science.

## Code efficiency

By and large, worrying about performance is a waste of time. For the most part we are better off just pushing things into the cloud, letting them run for a reasonable time, and using that time to worry about other aspects of the pipeline. But, eventually this becomes unfeasible. For instance, if something takes more than a day, then it becomes a pain because of the need to completely switch tasks and then return to it. There is rarely a most common area for obvious performance gains. Instead it is important to develop the ability to measure and then refactor code.

Being fast is valuable but it is mostly about being able to iterate fast not necessarily that the code runs fast. The first thing we should do if we find that the speed at which code is running is becoming a bottle neck is to shard. Then we should throw more machines at it. But eventually we should go back and refactor the code.

To refactor code means to re-write it so that the new code achieves the same outcome as the old code, it is just that the new code does it better. We can use `tic()` and `toc()` from `tictoc` [@Izrailev2014] to time various aspects of our code and find where the largest delays are.


```r
library(tictoc)
tic("First bit of code")
print("Fast code")
#> [1] "Fast code"
toc()
#> First bit of code: 0.041 sec elapsed

tic("Second bit of code")
Sys.sleep(3)
print("Slow code")
#> [1] "Slow code"
toc()
#> Second bit of code: 3.006 sec elapsed
```

And so we know that there is something slowing down the code; which in this artificial case is `Sys.sleep()` causing a delay of 3 seconds.

When we start to refactor our code, we want to make sure that the re-written code achieves the same outcomes as the original code. This means that it is important to have tests written. We generally want to reduce the size of functions, by breaking them into smaller ones.


<!-- Start with an example of bad code, and then how it gets fixed. -->





## Data efficiency

### SQL

While it may be true that the SQL is never as good as the original, SQL is a popular way of working with data. Advanced users probably do a lot with it alone, but even just having a working knowledge of SQL increases the number of datasets that we can access. We can use SQL within RStudio 

SQL is a straightforward variant of the `dplyr` verbs that we have used throughout this book. Having used `mutate()`, `filter()` and `left_join()` in the `tidyverse` means that much of the core commands will be familiar. That means that the main difficulty will be getting on top of the order of operations because SQL can be pedantic.

SQL ("see-quell" or "S.Q.L.") is used with relational databases. A relational database is just a collection of at least one table, and a table is just some data organized into rows and columns. If there is more than one table in the database, then there should be some column that links them. Using it feels a bit like HTML/CSS in terms of being halfway between markup and programming. One fun aspect is that line spaces mean nothing: include them or do not, but always end a SQL command in a semicolon;

We can create an empty table of three columns of type: int, text, int:


```sql
CREATE TABLE table_name (
  column1 INTEGER,
  column2 TEXT,
  column3 INTEGER
);
```

Add a row of data:


```sql
INSERT INTO table_name (column1, column2, column3)
  VALUES (1234, 'Gough Menzies', 32);
```

Add a column:


```sql
ALTER TABLE table_name
  ADD COLUMN column4 TEXT;
```

We can view particular aspects of the data, using SELECT in a similar way to `select()`.


```sql
SELECT column2
  FROM table_name;
```
See two columns:


```sql
SELECT column1, column2
  FROM table_name;
```

See all columns:


```sql
SELECT *
  FROM table_name;
```

See unique rows in a column (similar to R's distinct):


```sql
SELECT DISTINCT column2
  FROM table_name;
```

See the rows that match a criteria (similar idea to R's which or filter):


```sql
SELECT *
  FROM table_name
    WHERE column3 > 30;
```

All the usual operators are fine with WHERE: =, !=, >, <, >=, <=. Just make sure the condition evaluates to true/false.

See the rows that are pretty close to a criteria:


```sql
SELECT *
  FROM table_name
    WHERE column2 LIKE  '_ough Menzies';
```

The _ above is a wildcard that matches to any character e.g. 'Cough Menzies' would be matched here, as would 'Gough Menzies'. LIKE is not case-sensitive: 'Gough Menzies' and 'gough menzies' would both match here.

Use % as an anchor to matches pieces:


```sql
SELECT *
  FROM table_name
    WHERE column2 LIKE  '%Menzies';
```

That matches anything ending with 'Menzies', so 'Cough Menzies', 'Gough Menzies', 'Sir Menzies' etc, would all be matched here. Use surrounding percentages to match within, e.g. %Menzies% would also match 'Sir Menzies Jr' whereas %Menzies would not.

This is wild: NULL values (!) (True/False/NULL) are possible, not just True/False, but they need to be explicitly matched for:


```sql
SELECT *
  FROM table_name
    WHERE column2 IS NOT NULL;
```

This too is wild: There's an underlying ordering build into number, date and text fields that allows you to use BETWEEN on all those, not just numeric! The following looks for text that starts with a letter between A and M (not including M) so would match 'Gough Menzies', but not 'Sir Gough Menzies'!


```sql
SELECT *
  FROM table_name
    WHERE column2 BETWEEN 'A' AND 'M';
```

If you look for a numeric (as opposed to text) then BETWEEN is inclusive.

Combine conditions with AND (both must be true to be returned) or OR (at least one must be true):


```sql
SELECT *
  FROM table_name
    WHERE column2 BETWEEN 'A' AND 'M'
    AND column3 = 32;
```

You can order the result:


```sql
SELECT *
  FROM table_name
    ORDER BY column3;
```

Ascending is the default, add DESC for alternative:


```sql
SELECT *
  FROM table_name
    ORDER BY column3 DESC;
```

Restrict the return to a certain number of values by adding LIMIT at the end:


```sql
SELECT *
  FROM table_name
    ORDER BY column3 DESC
    LIMIT 1;
```

(This doesn't work all the time - only certain SQL databases.)

We can modify data and use logic. For instance we can edit a value.


```sql
UPDATE table_name
  SET column3 = 33
    WHERE column1 = 1234;
```

Implement if/else logic:


```sql
SELECT *,
  CASE
    WHEN column2 = 'Gough Whitlam' THEN 'Labor'
    WHEN column2 = 'Robert Menzies' THEN 'Liberal'
    ELSE 'Who knows'
  END AS 'Party'
  FROM table_name;
```
This returns a column called 'Party' that looks at the name of the person to return a party.

Delete some rows:


```sql
DELETE FROM table_name
  WHERE column3 IS NULL;
```

Add an alias to a column name (this just shows in the output):


```sql
SELECT column2 AS 'Names'
  FROM table_name;
```

We can use COUNT, SUM, MAX, MIN, AVG and ROUND in the place of `summarize()`. COUNT counts the number of rows that are not empty for some column by passing the column name, or for all using *.


```sql
SELECT COUNT(*)
  FROM table_name;
```

Similarly, we can pass a column to SUM, MAX, MIN, and AVG.


```sql
SELECT SUM(column1)
  FROM table_name;
```

ROUND takes a column and an integer to specify how many decimal places.


```sql
SELECT ROUND(column1, 0)
  FROM table_name;
```

SELECT and GROUP BY is similar to group_by in R.


```sql
SELECT column3, COUNT(*)
  FROM table_name
    GROUP BY column3;
```

We can GROUP BY column number instead of name e.g. 1 instead of column3 in the GROUP BY line or 2 instead of COUNT(*) if that was of interest.

HAVING for aggregates, is similar to filter in R or the WHERE for rows from earlier. Use it after GROUP BY and before ORDER BY and LIMIT.

We can combine two tables using JOIN or LEFT JOIN.


```sql
SELECT *
  FROM table1_name
  JOIN table2_name
    ON table1_name.colum1 = table2_name.column1;
```

Be careful to specify the matching columns using dot notation. Primary key columns uniquely identify rows and are: 1) never NULL; 2) unique; 3) only one column per table. A primary key can be primary in one table and foreign in another. Unique columns have a different value for every row and there can be many in one table.

UNION is the equivalent of cbind if the tables are already fairly similar.


<!-- ### Feather -->



### Parquet

While the use of CSVs is great because they are so widely used and have very little overhead, they are also very minimal. This can lead to issues, especially in terms of class. There are various modern alternatives, including `arrow` [@arrow]. Where we use `write_csv()` and `read_csv()` we can use `write_parquet()` and `read_parquet()`. One advantage is that it should retain the class between R and Python. It should also be faster than CSV.



```r
library(arrow)
library(tictoc)
library(tidyverse)

number_of_draws <- 1000000

some_data <- 
  tibble(
    first = runif(n = number_of_draws),
    second = sample(x = LETTERS, size = number_of_draws, replace = TRUE)
  )

tic("CSV")
write_csv(x = some_data,
          file = "some_data.csv")
read_csv(file = "some_data.csv")
#> # A tibble: 1,000,000 × 2
#>    first second
#>    <dbl> <chr> 
#>  1 0.514 I     
#>  2 0.878 X     
#>  3 0.913 B     
#>  4 0.519 V     
#>  5 0.243 B     
#>  6 0.362 Q     
#>  7 0.749 X     
#>  8 0.827 U     
#>  9 0.130 P     
#> 10 0.780 C     
#> # … with 999,990 more rows
toc()
#> CSV: 0.393 sec elapsed

tic("parquet")
write_parquet(x = some_data,
              sink = "some_data.parquet")
read_parquet(file = "some_data.parquet")
#> # A tibble: 1,000,000 × 2
#>    first second
#>    <dbl> <chr> 
#>  1 0.514 I     
#>  2 0.878 X     
#>  3 0.913 B     
#>  4 0.519 V     
#>  5 0.243 B     
#>  6 0.362 Q     
#>  7 0.749 X     
#>  8 0.827 U     
#>  9 0.130 P     
#> 10 0.780 C     
#> # … with 999,990 more rows
toc()
#> parquet: 0.225 sec elapsed
```







<!-- ## Experimental efficiency -->

<!-- Multi-armed bandit -->

<!-- ## Other languages -->

<!-- ### Python -->

<!-- ### Julia -->


<!-- Reproducibilty -->
<!-- renv -->


## Exercises and tutorial

### Exercises


### Tutorial


### Paper

At about this point, the Final Paper (Appendix \@ref(final-paper)) would be appropriate.
