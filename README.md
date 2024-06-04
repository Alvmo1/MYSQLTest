# MYSQLTest
```sql
mysql> INSERT INTO Movies (Title, Runtime, Genre, IMDB_Score, Rating)VALUES
    ->   ('The Matrix', 136, 'Sci-Fi', 8.7, 'R'),
    -> ('Toy Story', 81, 'Animation', 8.3, 'G');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from Movies;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| The Matrix        |     136 | Sci-Fi      |        8.7 | R      |
| Toy Story         |      81 | Animation   |        8.3 | G      |
+-------------------+---------+-------------+------------+--------+
8 rows in set (0.00 sec)

mysql>  SELECT * FROM Movies WHERE Genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| Title             | Runtime | Genre  | IMDB_Score | Rating |
+-------------------+---------+--------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
| The Matrix        |     136 | Sci-Fi |        8.7 | R      |
+-------------------+---------+--------+------------+--------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM Movies WHERE IMDB_Score >= 6.5;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| The Matrix        |     136 | Sci-Fi      |        8.7 | R      |
| Toy Story         |      81 | Animation   |        8.3 | G      |
+-------------------+---------+-------------+------------+--------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM Movies WHERE (Rating = 'G' OR Rating = 'PG') AND Runtime < 100;
+---------------+---------+-----------+------------+--------+
| Title         | Runtime | Genre     | IMDB_Score | Rating |
+---------------+---------+-----------+------------+--------+
| Spaceballs    |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc. |      92 | Animation |        8.1 | G      |
| Toy Story     |      81 | Animation |        8.3 | G      |
+---------------+---------+-----------+------------+--------+
3 rows in set (0.00 sec)

mysql>  SELECT Genre, AVG(Runtime) AS AverageRuntime FROM Movies WHERE IMDB_Score < 7.5 GROUP BY Genre;
+--------+----------------+
| Genre  | AverageRuntime |
+--------+----------------+
| Sci-Fi |       119.5000 |
| Horror |        83.0000 |
| Comedy |        96.0000 |
+--------+----------------+
3 rows in set (0.00 sec)

mysql>  UPDATE Movies SET Rating = 'R' WHERE Title = 'Starship Troopers';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from Movies;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| The Matrix        |     136 | Sci-Fi      |        8.7 | R      |
| Toy Story         |      81 | Animation   |        8.3 | G      |
+-------------------+---------+-------------+------------+--------+
8 rows in set (0.00 sec)

mysql> ALTER TABLE Movies ADD COLUMN Id INT AUTO_INCREMENT PRIMARY KEY FIRST;
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SELECT Id, Rating FROM Movies WHERE Genre IN ('Horror', 'Documentary');
+----+--------+
| Id | Rating |
+----+--------+
|  2 | TV-14  |
|  4 | R      |
+----+--------+
2 rows in set (0.00 sec)

mysql> SELECT Rating, AVG(IMDB_Score) AS AvgScore, MAX(IMDB_Score) AS MaxScore, MIN(IMDB_Score) AS MinScore FROM Movies GROUP BY Rating;
+--------+----------+----------+----------+
| Rating | AvgScore | MaxScore | MinScore |
+--------+----------+----------+----------+
| PG     |  5.85000 |      7.1 |      4.6 |
| TV-14  |  4.70000 |      4.7 |      4.7 |
| R      |  7.96667 |      8.7 |      7.2 |
| G      |  8.20000 |      8.3 |      8.1 |
+--------+----------+----------+----------+
4 rows in set (0.00 sec)

mysql> SELECT Rating, AVG(IMDB_Score) AS AvgScore, MAX(IMDB_Score) AS MaxScore, MIN(IMDB_Score) AS MinScore FROM Movies GROUP BY Rating HAVING COUNT(*) > 1;
+--------+----------+----------+----------+
| Rating | AvgScore | MaxScore | MinScore |
+--------+----------+----------+----------+
| PG     |  5.85000 |      7.1 |      4.6 |
| R      |  7.96667 |      8.7 |      7.2 |
| G      |  8.20000 |      8.3 |      8.1 |
+--------+----------+----------+----------+
3 rows in set (0.00 sec)

mysql> DELETE FROM Movies WHERE Rating = 'R';
Query OK, 3 rows affected (0.01 sec)

mysql> select * from Movies;
+----+-----------------+---------+-----------+------------+--------+
| Id | Title           | Runtime | Genre     | IMDB_Score | Rating |
+----+-----------------+---------+-----------+------------+--------+
|  1 | Howard the Duck |     110 | Sci-Fi    |        4.6 | PG     |
|  2 | Lavalantula     |      83 | Horror    |        4.7 | TV-14  |
|  5 | Spaceballs      |      96 | Comedy    |        7.1 | PG     |
|  6 | Monsters Inc.   |      92 | Animation |        8.1 | G      |
|  8 | Toy Story       |      81 | Animation |        8.3 | G      |
+----+-----------------+---------+-----------+------------+--------+
5 rows in set (0.00 sec)

mysql> DROP TABLE Movies;
Query OK, 0 rows affected (0.02 sec)

mysql> DROP DATABASE MOVIES_DB1;
Query OK, 0 rows affected (0.02 sec)
