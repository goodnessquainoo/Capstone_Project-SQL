

Famous Ghanaian Entertainers Database
This project is a structured relational database developed using SQL that captures detailed information about some of the most famous entertainers in Ghana. It demonstrates how to model real-world entities and their relationships—such as people, their music, movies, awards, possessions, and contributions—into a normalized SQL database.

The database is created to showcase how SQL can be used not only to design relational schemas but also to answer complex real-life analytical queries.

Database Overview
The following tables were created:

People – Stores information about celebrities, including name, date of birth, nationality, region, and occupation.

Movies – Contains data about movies and links them to the celebrities.

Music – Holds records of music tracks, including genre, album, streams, and the performing celebrity.

Awards – Stores awards received by celebrities, including category and year.

Contributions – Captures the roles celebrities play in both the music and movie industries.

Possessions – Contains assets owned by celebrities, including type, value, and purchase year.

SQL Queries and Analysis
This section outlines the specific questions the database answers and the SQL queries used.

1. Find celebrities who have won an award and starred in a movie with box office revenue greater than 400,000
sql
Copy
Edit
SELECT People.Celebrity_name, Awards.Category, Movies.Box_office_revenue
FROM People
JOIN Awards ON People.Person_id = Awards.Person_id
JOIN Movies ON People.Person_id = Movies.Person_id
HAVING Movies.Box_office_revenue > 400000;
2. List the celebrities who have released music in the 'Afrobeats' genre and have a net worth greater than 50,000
sql
Copy
Edit
SELECT People.Celebrity_name, Music.Genre, Possessions.Networth 
FROM People
JOIN Music ON People.Person_id = Music.Person_id
JOIN Possessions ON People.Person_id = Possessions.Person_id
WHERE Music.Genre = 'Afrobeats'
AND Possessions.Networth > 50000;
3. Retrieve celebrities who have won an award in 2018 or later and have a music album released after 2017
sql
Copy
Edit
SELECT People.Celebrity_name, Awards.Category, Awards.Award_year, Music.Album_name
FROM People
JOIN Awards ON People.Person_id = Awards.Person_id
JOIN Music ON People.Person_id = Music.Person_id
WHERE Awards.Award_year >= 2018
AND Music.Release_year > 2017;
4. Find celebrities who acted in ‘Drama’ movies and also released music in the ‘Afrobeats’ genre
sql
Copy
Edit
SELECT People.Celebrity_Name, Movies.Genre, Music.Album_name
FROM People
JOIN Movies ON People.Person_id = Movies.Person_id
JOIN Music ON People.Person_id = Music.Person_id
WHERE Movies.Genre = 'Drama'
AND Music.Genre = 'Afrobeats';
5. List celebrities who own an island and released a song with more than 7,000,000 streams
sql
Copy
Edit
SELECT People.Celebrity_name, Possessions.Possession_type, Music.Streams
FROM People
JOIN Possessions ON People.Person_id = Possessions.Person_id
JOIN Music ON People.Person_id = Music.Person_id
WHERE Possessions.Possession_type = 'Island'
AND Music.Streams > 7000000;
6. List celebrities who purchased a possession in or after 2018 and released a song in the same time period
sql
Copy
Edit
SELECT People.Celebrity_name, Possessions.Purchase_year, Music.Release_year
FROM People
JOIN Possessions ON People.Person_id = Possessions.Person_id
JOIN Music ON People.Person_id = Music.Person_id
WHERE Possessions.Purchase_year >= 2018
AND Music.Release_year >= 2018
ORDER BY Possessions.Purchase_year DESC;
7. Calculate and compare average net worths of celebrities in the music and movie industries
Music Industry:

sql
Copy
Edit
SELECT Music.Genre, AVG(Networth) AS Avg_Networth
FROM Possessions
JOIN Music ON Possessions.Person_id = Music.Person_id
GROUP BY Music.Genre
ORDER BY Avg_Networth DESC;
Movie Industry:

sql
Copy
Edit
SELECT Movies.Genre, AVG(Networth) AS Avg_Networth
FROM Possessions
JOIN Movies ON Possessions.Person_id = Movies.Person_id
GROUP BY Movies.Genre
ORDER BY Avg_Networth DESC;
Getting Started
To use this project:

Clone the repository.

Use a MySQL or compatible RDBMS to run the script.

Explore the queries or extend the schema with more insights and data types.

Purpose
This project demonstrates:

How to model entertainment-related data in a normalized database.

How to answer real-life analytical questions with SQL.

How to join multiple tables and apply filters based on business logic.
