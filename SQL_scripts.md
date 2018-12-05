Compare Two Tables using UNION ALL
UNION allows you to compare data from two similar tables or data sets. It also handles the NULL values to other NULL values which JOIN or WHERE clause doesn’t handle. It allows quickly checking what are the data missing or changed in either table.

Select * from ( 
Select Id_pk, col1, col2...,coln from table1, ‘Old_table’ 
Union all 
Select Id_pk, col1, col2...,coln from table2, 'New_tbale' 
) cmpr order by Id_pk;
The above query returns the all rows from both tables as old and new. You can quickly verify the differences between two tables.

Compare Two Table using MINUS
You can compare the two similar tables or data sets using MINUS operator. It returns all rows in table 1 that do not exist or changed in the other table.

Select Id_pk, col1, col2...,coln from table1 
MINUS
Select Id_pk, col1, col2...,coln from table2;
You can quickly check how many records are having mismatch between two tables.

The only drawback with using UNION and MINUS is that the tables must have the same number of columns and the data types must match.

Compare Two Table using JOIN
This is the easiest but user has to do some additional work to get the correct result. In this approach you can join the two tables on the primary key of the two tables and use case statement to check whether particular column is matching between two tables.

Select case when A.col1 = B.col1 then ‘Match’ else ‘Mismatch’ end as col1_cmpr, 
case when A.col2 = B.col2 then ‘Match’ else ‘Mismatch’ end as col2_cmpr, ….. 
from table1 A
Join table2 B
on (A.id_pk = B.id_pk) ;
The only drawback of using JOIN is, it cannot compare the NULL values, and you should use the NVL on the column that may have null values in it.

Compare Two Table using NOT EXISTS
The other faster method is to use the NOT EXISTS in WHERE clause of the query. This method is faster and performs well on the large volume of data.

Select id_pk, col1, col2,col,…
From table1 A
Where NOT EXISTS
( select 1 from table2 B
Where A.id_pk = B.id_pk
and A.col1 = B.col1
and A.col2 = B.col2
and…
);
In this approach also you have to use the NVL on the columns which contains NULL in it.

References:
http://dwgeek.com/quick-best-way-compare-two-tables-sql.html/
