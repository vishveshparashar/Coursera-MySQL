# Coursera-MySQL
hi

%load_ext sql

Now that the SQL library is loaded, we need to connect to a database. The following command will log you into the MySQL server at mysqlserver as the user 'studentuser' and will select the database named 'dognitiondb' :
%sql mysql://studentuser:studentpw@mysqlserver/dognitiondb

Once you are connected, the output cell (which reads "Out" followed by brackets) will read: "Connected:studentuser@dognitiondb". To make this the default database for our queries, run this "USE" command:
%sql USE dognitiondb

SELECT breed
FROM dogs LIMIT 10 OFFSET 5;
10 rows of data will be returned, starting at Row 6.
An alternative way to write the OFFSET clause in the query is:
SELECT breed
FROM dogs LIMIT 5, 10;


%load_ext sql
%sql mysql://studentuser:studentpw@mysqlserver/dognitiondb
%sql USE dognitiondb


SELECT dog_guid, weight
FROM dogs
WHERE weight BETWEEN 10 AND 50;

SELECT dog_guid, breed
FROM dogs
WHERE breed IN ("golden retriever","poodle");

SELECT dog_guid, breed
FROM dogs
WHERE breed LIKE ("s%");

%%sql
SELECT dog_guid, subcategory_name, test_name
FROM reviews
WHERE YEAR(created_at) = 2014
LIMIT 10;

%%sql
SELECT user_guid, gender, breed
FROM dogs
WHERE gender = "female" AND breed LIKE ("%terrier%")
LIMIT 5;

SELECT dog_guid, created_at AS time_stamp
FROM complete_tests

Note that if you use an alias that includes a space, the alias must be surrounded in quotes:
SELECT dog_guid, created_at AS "time stamp"
FROM complete_tests

You could also make an alias for a table:
SELECT dog_guid, created_at AS "time stamp"
FROM complete_tests AS tests

When the DISTINCT clause is used with multiple columns in a SELECT statement, the combination of all the columns together is used to determine the uniqueness of a row in a result set.

SELECT DISTINCT user_guid, (median_ITI_minutes * 60) AS median_ITI_sec
FROM dogs 
ORDER BY median_ITI_sec DESC
LIMIT 5

breed_list = %sql SELECT DISTINCT breed FROM dogs ORDER BY breed;
breed_list.csv('breed_list.csv')

SELECT DISTINCT breed,
REPLACE(breed,'-','') AS breed_fixed
FROM dogs
ORDER BY breed_fixed

