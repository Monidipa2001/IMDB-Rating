**Contents of the dataset** 
Series_Title 
Released_Year 
Certificate  
Runtime 
Genre 
IMDB_Rating 
Director 
Star1, Star2, Star3, Star4 
No_of_votes 
Earning 

QUERIES  
1.   **Displaying the directors in descending order based on the count of high-rating series: -**
2.   
          SELECT Director, COUNT(*) AS HighRatingSeriesCount 
          FROM project.imdb 
          WHERE IMDb_Rating > 8.0 
          GROUP BY Director 
          ORDER BY HighRatingSeriesCount DESC;
     
4.   **Retrieving all the columns from the imdb table where the Series_Title is equal to 'The Lord of the Rings: The Return of the King’: -**
5.   
          SELECT *  
          FROM project.imdb 
          WHERE Series_Title = 'The Lord of the Rings: The Return of the King';

7.   **Retrieving the total earnings for movies released in different years from imdb table: -**
8.   
          SELECT Released_Year, SUM(Earning) AS TotalEarnings 
          FROM project.imdb 
          GROUP BY Released_Year 
          ORDER BY Released_Year;
     
10.   **Retrieving all rows from the "imdb" table where the "Released_Year" is greater than 1950.**
11.   
          SELECT * 
          FROM project.imdb 
          WHERE Released_Year > 1950;
      
13.   **Retrieving information about pairs of stars who have appeared together in movies or series, and it counts how many times they have worked together.**
14.    
          SELECT Star1, Star2, COUNT(*) AS SeriesCount 
          FROM project.imdb 
          GROUP BY Star1, Star2 
          ORDER BY SeriesCount DESC 
          LIMIT 5;
   
16.   **Retrieving all rows from the "imdb" table where the "Certificate" column is 'A' and the "Genre" column is 'Drama'.**
17.   
          SELECT * 
          FROM project.imdb 
          WHERE Certificate = 'A' AND Genre = 'Drama';
      
19.   **Retrieving specific columns from the "imdb" table in the database based on certain conditions**
20.         
          SELECT Series_Title, Certificate, IMDB_Rating 
          FROM project.imdb 
          WHERE Certificate = 'UA' OR IMDB_Rating = '9';
        
22.   **Retrieving the "Series_Title" and "IMDb_Rating" columns from the "imdb" table for the series released in the year 2001 with the highest IMDb rating.**
23.   
          SELECT Series_Title, IMDb_Rating 
          FROM project.imdb 
          WHERE Released_Year = 2001 
          ORDER BY IMDb_Rating DESC 
          LIMIT 1;
      
25.    **Retrieving the "Series_Title" and "Genre" columns from the "imdb" table for series that do not have the genre 'Crime, Drama'.**
26.
          SELECT Series_Title, Genre 
          FROM project.imdb 
          WHERE NOT Genre = 'Crime,Drama';
   
28.   **Retrieving specific columns from the "imdb" table in the database based on certain conditions**
29.   
          SELECT Series_Title, Certificate, Genre, IMDB_Rating 
          FROM project.imdb 
          WHERE (Genre = 'Action, Adventure, Sci-Fi' OR Genre = 'Crime, Drama')AND IMDB_Rating < 9;
      
31.   **Retrieving the "Series_Title" column from the "imdb" table for series titles that contain the word "Game".**
32.   
          SELECT Series_Title 
          FROM project.imdb 
          WHERE Series_Title LIKE '%Game%';
      
12.   **Retrieving the rounded IMDb ratings (rounded to the nearest whole number) and the count of how many series have each rounded rating.**
13.    
          SELECT ROUND(IMDB_Rating) AS Rating, COUNT(*) AS Count 
          FROM project.imdb 
          GROUP BY ROUND(IMDB_Rating) 
          ORDER BY Rating;
    
15.   **Retrieving the "Series_Title," "IMDB_Rating," and "No_of_votes" columns from the "imdb" table for the series that have both the maximum IMDb rating and the maximum number of votes in the dataset.**
16.   
          SELECT Series_Title, IMDB_Rating, No_of_votes 
          FROM project.imdb 
          WHERE IMDB_Rating = (SELECT MAX(IMDB_Rating) FROM project.imdb) 
          AND No_of_votes = (SELECT MAX(No_of_votes) FROM project.imdb);
      
18.   **Retrieving data where the value in the "Star1" column begins with the letter 'J'.**
19.    
          SELECT Series_Title, Star1 
          FROM project.imdb 
          WHERE Star1 LIKE 'J%';
   
21.   **Counting the number of unique genres present in the "Genre" column.**
22.    
          SELECT COUNT(DISTINCT Genre) 
          FROM project.imdb;
   
24.   **Renaming the columns "Series_Title" and "Earning" to "Movie_name" and "Gross_earnings"**
25.    
          SELECT Series_Title AS Movie_name, Earning AS Gross_earnings 
          FROM project.imdb;
   
27.   **Retrieving the "Series_Title," "Runtime," and "Director" columns for the first 5 rows of the table. The "LIMIT 5" clause limits the result set to only 5 rows.**
28.    
          SELECT Series_Title, Runtime, Director 
          FROM project.imdb 
          LIMIT 5;
   
30.   **Retrieving the "Series_Title," "Star1," "Star2," "Star3," and "Star4" columns for 9 rows, starting from the 6th row (offset 5)**
31.    
          SELECT Series_Title, Star1, Star2, Star3, Star4 
          FROM project.imdb 
          LIMIT 9 OFFSET 5;
   
33.   **Retrieving the "Series_Title" and "Certificate" columns for rows where the "Certificate" column has the value 'UA'**
34.    
          SELECT Series_Title, Certificate 
          FROM project.imdb 
          WHERE Certificate IN('UA');
   
36.   **Retrieving the "Series_Title," "Director," and "Earning" columns for rows where the "Earning" column falls within the range between 422,783,777 and 600,000,000**
37.     
          SELECT Series_Title, Director, Earning 
          FROM project.imdb 
          WHERE Earning BETWEEN 422783777 AND 600000000;
      
38.  **Retrieving the "Series_Title," "Released_Year," "Certificate," "Director," and "Earning" columns for rows where the "Earning" is equal to the minimum earning value in the entire "imdb" table**
39.   
          SELECT Series_Title, Released_Year, Certificate,Director,Earning 
          FROM project.imdb 
          WHERE Earning = ( 
               SELECT MIN(Earning) 
          FROM project.imdb 
                );
      
40.  **Returning counts for those "Certificates" where the count of rows with that "Certificate" value is greater than 8.**
41.   
          SELECT COUNT(IMDB_Rating), Certificate 
          FROM project.imdb 
          group by Certificate 
          HAVING COUNT(IMDB_Rating)> 8;
      
42.  **Selecting the "Series_Title," "IMDB_Rating," and "Earning" columns for rows where the "IMDB_Rating" is not equal to '7'. It then orders the result set in descending order based on the "Series_Title" column.**
43.   
          SELECT Series_Title, IMDB_Rating, Earning 
          FROM project.imdb 
          WHERE NOT IMDB_Rating = '7' 
          ORDER BY Series_Title DESC;
      
44.  **If the "Earning" is greater than or equal to 60,000,000, it assigns the value 'BLOCKBUSTER' to the "BLOCKBUSTER" column; otherwise, it assigns 'NOT BLOCKBUSTER'**
45.  
          SELECT Series_Title, Director, Earning, 
          CASE  
          WHEN Earning >= 60000000 THEN 'BLOCKBUSTER' 
          ELSE 'NOT BLOCKBUSTER' 
          END AS BLOCKBUSTER 
          FROM project.imdb;
      
46.   **If the "Director" is 'Christopher Nolan', it assigns the value 'BEST DIRECTOR' to the "BLOCKBUSTER" column. If the "Director" is 'Francis Ford Coppola', it assigns 'AVERAGE DIRECTOR' to the "BLOCKBUSTER" column**
47.   
          SELECT Series_Title, Director, 
          CASE  
        	WHEN Director = 'Christopher Nolan' THEN 'BEST DIRECTOR' 
          WHEN Director = 'Francis Ford Coppola' THEN 'AVERAGE DIRECTOR' 
          END AS BLOCKBUSTER 
          FROM project.imdb; 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 
