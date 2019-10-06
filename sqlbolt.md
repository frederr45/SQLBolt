SQLBolt
=======
SQL Lesson 10: Queries with aggregates (Pt. 1)
---
    1. Find the longest time that an employee has been at the studio
    ```
        SELECT MAX(years_employed)
        FROM employees;
    ```
    2. For each role, find the average number of years employed by employees in that role
    ```
        SELECT role, AVG(years_employed) AS avg_year 
        FROM employees group by role;
    ```
    3. Find the total number of employee years worked in each building
    ```
        SELECT building, SUM(years_employed) AS sum_year
        FROM employees 
        GROUP BY building;
    ```
SQL Lesson 11: Queries with aggregates (Pt. 2)
---
    1. Find the number of Artists in the studio (without a HAVING clause)
    ```
        SELECT role, COUNT(*) as Num_art
        FROM employees
        WHERE role = "Artist";
    ```
    2. Find the number of Employees of each role in the studio
    ```
        SELECT role, COUNT(*) 
        FROM employees 
        GROUP BY role;
    ```
    3. Find the total number of years employed by all Engineers
    ```
        SELECT SUM(years_employed) 
        FROM employees 
        WHERE role = 'Engineer'
    ```
SQL Lesson 12: Order of execution of a Query
---
    1. Find the number of movies each director has directed
    ```
        SELECT director, COUNT(*) AS Films
        FROM movies 
        GROUP BY director;
    ```
    2. Find the total domestic and international sales that can be attributed to each director
    ```
        SELECT director, SUM(Domestic_sales + International_sales) AS total FROM movies
        INNER JOIN boxoffice 
        ON movies.id = boxoffice.movie_id
        GROUP BY director;
    ```
SQL Lesson 13: Inserting rows
---
    1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
    ```
        INSERT INTO movies
        VALUES(15, 'Toy Story 4', 'John Lasseter', 2014, 101);
    ```
    2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the  BoxOffice table.
    ```
        INSERT INTO boxoffice
        VALUES(15, 8.7, 340000000, 270000000);
    ```
SQL Lesson 14: Updating rows
---
    1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
    ```
        UPDATE movies
        SET director = 'John Lasseter'
        WHERE title = "A Bug's Life";
    ```
    2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
    ```
        UPDATE movies
        SET year = 1999
        WHERE title = "Toy Story 2";
    ```
    3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
    ```
        UPDATE movies
        SET director = 'Lee Unkrich',
        title = 'Toy Story 3'
        WHERE id = 11;
    ```
SQL Lesson 15: Deleting rows
---
    1. This database is getting too big, lets remove all movies that were released before 2005.
    ```
        DELETE FROM movies
        WHERE year < 2005;
    ```
    2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
    ```
        DELETE FROM movies
        WHERE director = 'Andrew Stanton';  
    ```
SQL Lesson 16: Creating tables
---
    1. Create a new table named  Database with the following columns:
        – Name A string (text) describing the name of the database
        – Version A number (floating point) of the latest version of this database
        – Download_count An integer count of the number of times this database was downloaded
    ```
        CREATE TABLE Database (
            Name TEXT,
            Version FLOAT,
            Download_count INTEGER
        );
    ```
SQL Lesson 17: Altering tables
---
    1.Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
    ```
        ALTER TABLE movies
        ADD Aspect_ratio FLOAT
            DEFAULT Null;
    ```
    2.Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
    ```
        ALTER TABLE movies
        ADD Language TEXT
            DEFAULT 'English';
    ```
SQL Lesson 18: Dropping tables
---
    1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
    ```
        DROP TABLE movies;
    ```
    2. And drop the BoxOffice table as well
    ```
        DROP TABLE boxoffice;
    ```