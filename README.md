<h1>Analytics Project #1</h1>

<h2>Table of Contents</h2>
1. Description<br/>
2. Languages and Utilities Used<br/>
3. Insights Display<br/>
4. SQL Codes Display<br/>
<br /><hr>

<h2>1. Description</h2>
This project utilizes Netflix data which includes country, genre, type, year and directors to dive into Netflix's selection of media. Using R, SQL and Excel, I was able to wrangle, manipulate the data, and visualize it by type, countries, year, genre and more. <br/>
<br/>
Due to the database not containing any consumer data, this insights will primarily cater to movie lovers and streaming service competitors for Netflix's content evaluation purpose.<br />
<br /><hr>

<h2>2. Languages and Environment Used</h2>
- MySQL - 95%<br/> 
- R Studio -5%<br/>
- Environment used: Macbook 13<br />
<br/><hr>


<h2>3. Insights Display:</h2>

<div class="section1">
  <img src="https://imgtr.ee/images/2023/06/09/Koedz.png" alt="Koedz.png" border="0" width=800px />
  <h4> - Netflix media & media length by type: </h4>
  <p>As shown above, more than 96% of Netflix's media is made up of movies. While TV only makes up less than 4% of the total media, its individual length is much longer than its movie counterpart.</p>
  <p>When comparing the two types by length, the media type of TV makes up about 30% of the total media content length, which shows that it is a very important media type for Netflix. In this chart, I converted "Season" to "min" to match the movie length. (Here we assume 1 season = 12 episodes, and 1 episode = 55 minutes according to thrillist.com.)</p><hr>
</div>
<br />
<br />


 <div class="section2">
  <a href='https://postimg.cc/jDvQgSH3' target='_blank'><img src='https://i.postimg.cc/43RL3KmG/by-countries.png' border='0' width=800px alt='by-countries'/></a>
  <h4> - Netflix media by country & year: </h4>
  <p>When looking at the data by countries, we can see that the U.S., India, and the U.K. are the top three countries for the most media output on Netflix. It is worth noting that the U.S., U.K., and Spain had the most TV shows output on Netflix, while India has a relatively heavy-up on movies.</p>
  <p>When looking at countries' media output by decades, Netflix has media from as old as the 1940s for movies such as "Prelude to War". But most of the Netflix media were made in the 2010s, followed by recent (2020 or after).</p><hr>
</div>
<br />
<br />

<div class="section3">
  <a href='https://postimg.cc/CnRW18mt' target='_blank'><img src='https://i.postimg.cc/gjsdgqRY/genre-by-decade.png' border='0' width=800px alt='genre-by-decade'/></a>
  <h4 align="left"> - Netflix media genre by decade: </h4>
  <p align=left> When ordering the genres in a descending order, we know that these are the most popular five genres at all times on Netflix: </p>
  <p> - 'Dramas,International Movie', 'Documentaries', 'Stand-Up Comedy', 'Comedies, Dramas, International Movies', 'Dramas, Independent Movies, International Movies'</p> 
  <p>The pie charts above display the top five genres in each decade, and the "most popular genres all times" are highlighted in red. As seen above, "doumentaries" started to popularize since the 40s, while genres like "stand up comedies" did not stand out till recent years (past 2020). </p>
 <p>It is also worth noting here that, due to the amounts of recent medias being larger than their past counterparts, we tend to see the "all time popular movies" being skewed by recent decades data. </p><hr>
</div>
<br/>
<br/>

<div class="section4">
  <a href='https://postimg.cc/Z0MtGyLQ' target='_blank'><img src='https://i.postimg.cc/ncHFQ49n/by-Ratings.png' border='0' width=800px alt='by-Ratings'/></a>
  <h4 align="left"> - Netflix media genre by ratings: </h4>
<hr>
</div>
<br/>
<br/>


</br>
<h2>4. SQL Codes Walk-through</h2>

  <p align="left"> After uploading the raw CSV file to MySQL, I realized that there were two issues: </p>
  <p>1. There were null values  2. The units in 'duration' column weren't unified. </p>
  <p> Hence, I dropped the null values, after which, there are nine columns for analysis: show_id,type,title, director,country,year,rating,duration and genre.</p>
  
  <pre><code class="language-sql" style="color: blue;">><p style="font-size:4.5px;">
  mysql&gt; UPDATE netflix_data
        -&gt; SET duration=CONCAT(SUBSTRING_INDEX(duration,' ',1)*12*55,' min')
        -&gt; WHERE duration LIKE '%Season%';
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
  5 rows in set (0.01 sec);
  </p></code></pre><hr>


<br/>
<br/>
  <p style=left-aligned> To unify the "duration" column, I then wrangled the data by using "substring()" and "concat()" functions to update "season" to "min": </p>
  <pre><code class="language-sql"><p="font-size:4.5px; color: blue;x;">
UPDATE netflix_duplicate
SET duration= CONCAT(SUBSTRING_INDEX(duration,' ',1)*12*55,' min')
WHERE duration LIKE '%Season%';
  </p></code></pre><hr>
 
 
<br/>
<br/>
  <p align="Left"> Using the case statement, I pulled genre information by decade and excluded genres that contains 5 or less movies or TV shows across all decades. The information is pulled in a descending order through the sum of media. </p>
  <pre><code class="language-sql"><p style="font-size:4.5px; color: blue;;">
  mysql> SELECT genre,
    ->     SUM(CASE WHEN year >= 1940 AND year < 1950 THEN 1 ELSE 0 END) AS '1940s_count',
    ->     SUM(CASE WHEN year >= 1950 AND year < 1960 THEN 1 ELSE 0 END) AS '1950s_count',
    ->     SUM(CASE WHEN year >= 1960 AND year < 1970 THEN 1 ELSE 0 END) AS '1960s_count',
    ->     SUM(CASE WHEN year >= 1970 AND year < 1980 THEN 1 ELSE 0 END) AS '1970s_count',
    ->     SUM(CASE WHEN year >= 1980 AND year < 1990 THEN 1 ELSE 0 END) AS '1980s_count',
    ->     SUM(CASE WHEN year >= 1990 AND year < 2000 THEN 1 ELSE 0 END) AS '1990s_count',
    ->     SUM(CASE WHEN year >= 2000 AND year < 2010 THEN 1 ELSE 0 END) AS '2000s_count',
    ->     SUM(CASE WHEN year >= 2010 AND year < 2020 THEN 1 ELSE 0 END) AS '2010s_count',
    ->     SUM(CASE WHEN year >= 2020 THEN 1 ELSE 0 END) AS 'recent_count'
    -> FROM netflix_duplicate
    -> GROUP BY genre
    -> HAVING (SUM(CASE WHEN year >= 1940 AND year < 1950 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 1950 AND year < 1960 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 1960 AND year < 1970 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 1970 AND year < 1980 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 1980 AND year < 1990 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 1990 AND year < 2000 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 2000 AND year < 2010 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 2010 AND year < 2020 THEN 1 ELSE 0 END) +
    ->         SUM(CASE WHEN year >= 2020 THEN 1 ELSE 0 END)) >= 5
    -> ORDER BY SUM(year) DESC;
  </p></code></pre><hr>


</br>
</br>
  <pre><code class="langugae-sql"><p style="font-size:4.5px; color: blue;">
  CREATE TABLE netflix_rating AS(
  SELECT DISTINCT rating,counts,
  ROW_NUMBER() OVER(ORDER BY counts DESC) AS ranking
    FROM(
      SELECT rating, COUNT(rating) AS counts
      FROM netflix_duplicate
      GROUP BY rating
      ) AS subquery);
  </p></code></pre><br/>
