# FirstSQL
## Create a database.
CREATE DATABASE movies;

## Add Movies to the movies table using an insert statement:
USE movies;
CREATE TABLE movies(
title VARCHAR(30),
runtime INT,
genre VARCHAR(30),
IMBscore DECIMAL(2,1),
rating VARCHAR(6)
);
INSERT INTO movies VALUES ('Howard the Duck', 110, 'Sci-Fi', 4.6, 'PG');
INSERT INTO movies VALUES('Lavalantula', 83,'Horror',4.7,'TV-14');
INSERT INTO movies VALUES('Starship Troopers',	129,'Sci-Fi', 7.2, 'PG-13');
INSERT INTO movies VALUES('Waltz With Bashir',90, 'Documentary',8.0	,'R');
INSERT INTO movies VALUES('Spaceballs',96,	'Comedy',7.1,'PG');
INSERT INTO movies VALUES('Monsters Inc.',92,'Animation',8.1,'G');
INSERT INTO movies VALUES('The Matrix', 136, 'Sci-Fi',8.7,'R');
INSERT INTO movies VALUES('Friday',91,'Comedy',7.3, 'R'); 

## Create a query to find all movies in the Sci-Fi genre

SELECT * FROM movies WHERE genre = 'Sci-Fi';

## Create a query to find all films that scored at least a 6.5 on IMDB

SELECT * FROM movies WHERE IMBscore >= 6.5;

## For parents who have young kids, but who don't want to sit through long children's movies,
create a query to find all of the movies rated G or PG that are less than 100 minutes long

SELECT * FROM movies WHERE runtime < 100 AND rating = 'PG' OR 'G';

## Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres
 
SELECT AVG(runtime) FROM movies WHERE IMBscore < 7.5 GROUP BY genre;

## There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R

ALTER TABLE movies ADD PRIMARY KEY (title);
UPDATE movies SET rating = 'R' WHERE title = 'Starship Troopers';

## Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query

SELECT title, rating FROM movies WHERE genre IN ('Horror' ,'Documentary');

## This time let's find the average, maximum, and minimum IMDB score for movies of each rating

SELECT rating, MAX(IMBscore), MIN(IMBscore), AVG(IMBscore) FROM movies GROUP BY rating

##That last query isn't very informative for ratings that only have 1 entry. Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing

HAVING COUNT(*) > 1;



## THREE EXTRA QUERIES :)

SELECT * FROM movies WHERE title LIKE 's%';
SELECT title, runtime FROM movies ORDER BY runtime ASC;
SELECT * FROM movies WHERE title LIKE '%st%' ORDER BY title ASC;
