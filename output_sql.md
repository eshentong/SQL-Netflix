mysql> UPDATE netflix_data
    -> SET duration=CONCAT(SUBSTRING_INDEX(duration,' ',1)*12*55,' min')
    -> WHERE duration LIKE '%Season%';
Query OK, 219 rows affected (0.22 sec)
Rows matched: 219  Changed: 219  Warnings: 0

mysql> SELECT* FROM netflix_data
    -> LIMIT 5;
+---------+---------+----------------------------------+-----------------+---------------+------+--------+----------+---------------------------------------------------------------+
| show_id | type    | title                            | director        | country       | year | rating | duration | genre                                                         |
+---------+---------+----------------------------------+-----------------+---------------+------+--------+----------+---------------------------------------------------------------+
| s1      | Movie   | Dick Johnson Is Dead             | Kirsten Johnson | United States | 2020 | PG-13  | 90 min   | Documentaries                                                 |
| s3      | TV Show | Ganglands                        | Julien Leclercq | France        | 2021 | TV-MA  | 660 min  | Crime TV Shows, International TV Shows, TV Action & Adventure |
| s6      | TV Show | Midnight Mass                    | Mike Flanagan   | United States | 2021 | TV-MA  | 660 min  | TV Dramas, TV Horror, TV Mysteries                            |
| s14     | Movie   | Confessions of an Invisible Girl | Bruno Garotti   | Brazil        | 2021 | TV-PG  | 91 min   | Children & Family Movies, Comedies                            |
| s8      | Movie   | Sankofa                          | Haile Gerima    | United States | 1993 | TV-MA  | 125 min  | Dramas, Independent Movies, International Movies              |
+---------+---------+----------------------------------+-----------------+---------------+------+--------+----------+---------------------------------------------------------------+
5 rows in set (0.01 sec)

mysql> notee
