<h1>Netflix Categorical SQL Project</h1>

<h2>Table of Contents</h2>
1. Description<br/>
2. Languages and Utilities Used<br/>
3. Insights Display<br/>
4. SQL Codes Display<br/>
<br /><hr>

<h2>1. Description</h2>
  <p>This project utilizes Netflix data which includes eight columns of categorical data: <br>
     <br><strong> Show_id(index column):</strong>  Netflix's internal show id, not used in the projects
     <br><strong> Type: </strong>  film or TV
     <br><strong> Title: </strong>  title of each film/TV
     <br><strong> Director: </strong>  director, producer names of each film/TV
     <br><strong> Country: </strong>  country of origin of production
     <br><strong> Release Year: </strong>  released year of each film/TV
     <br><strong> Rating: </strong>  ratings for recommended audience age
     <br><strong> Duration: </strong>  media durations in seasons or episodes for TVs, and minutes for movies
     <br><strong> Listed In: </strong>  genres for each film/TV
     
   <br> I broke down the eight variables into two groups:</br></p>
    

        - audience analysis (type, country, rating, listed in)
        - productions analysis (type, title, director, country, release year, duration, and listed_in)
        
Due to the database not containing any numeric consumer data, this insight will primarily cater to movie lovers and streaming service evaluation for Netflix's content evaluation purpose.</p>
<br />
<br /><hr>

<h2>2. Languages and Environment Used</h2>
- MySQL - 95%<br/> 
- R Studio -5%<br/>
- Environment used: Macbook 13<br />
<br/><hr>


<h2>3. Insights Display | Audience Analysis:</h2>
<div class="section4">
  <a href="https://yourimageshare.com/ib/PNWOTg1YGQ"><img src="https://yourimageshare.com/ib/PNWOTg1YGQ.webp" width=800px alt="by-ratings"></a>
  <h4 align="left"> - Netflix media genre by ratings: </h4>
  <p align=left> The ordinal categorical data of ratings can be ordered from strictest to unlimited as shown above. We can see the percentage of each rating category accordingly in the stacked chart: more than 50% of Netflix's shows and movies are 18+ contents. Hence, it can be inferred that Netflix prioritizes its adult audiences. 
</div>
<br/>
<br/>
<hr>


<div class="section3">
  <a href='https://postimg.cc/V5CfcHx5' target='_blank'><img src='https://i.postimg.cc/sfnv7kKP/by-decade.jpg' border='0' width=800px alt='by-decade'/></a>
  <h4 align="left"> - Netflix media genre by decade: </h4>
  <p align=left> When ordering the genres in descending order, we know that these are the most popular five genres at all times on Netflix: </p>
  <p> 1. Dramas, International Movie: such as 'The Dig' (2021) by Simon Stone. </br>
      2. Documentaries: such as 'Kiss the Ground' (2020) by Joshua Tickell, Rebecca Harrel.</br>
      3. Stand-Up Comedy: such as 'Ali Wong: Don Wong' (2022) by Ali Wong. </br>
      4. Comedies, Dramas, International Movies: such as 'Mimi' (2021) by Laxman Utekar. </br>
      5. Dramas, Independent Movies, International Movies: such as 'Atlantics' (2019) by Mati Diop. </p> 
  
  <p>The pie charts above display the top five genres in each decade, and the "most popular of all times" are highlighted in red. As seen above, "documentaries" started to popularize in the 40s, while genres like "stand-up comedies" did not stand out till recent years (past 2020). </p>
 <p>It is also worth noting here that, due to the amounts of recent media being larger than their past counterparts, we tend to see the "all-time popular movies" being skewed by recent decades' data. </p><hr>
</div>
<br/>
<br/>


<h2>3. Insights Display | Production Analysis:</h2>

<div class="section1">
  <a href='https://postimg.cc/5HBr3LT4' target='_blank'><img src='https://i.postimg.cc/43qTX119/by-number-VSlength.jpg' border='0' width=800px alt='by-number-VSlength'/></a>
  <h4> - Netflix media & media length by type: </h4>
      <p>As shown above, more than 96% of Netflix's media is made up of movies. While TV only makes up less than 4% of the total media, its individual length is much longer than its movie counterpart.</p>
      <p>When comparing the two types by length, the media type of TV makes up about 30% of the total media content length, which shows that it is a very important media type for Netflix. In this chart, I converted "Season" to "min" to match the movie length. (Here we assume 1 season = 12 episodes, and 1 episode = 55 minutes according to thrillist.com.)</p><hr>
</div>
<br />
<br />


<div class="section2">
  <a href='https://postimg.cc/Z9S7C0R1' target='_blank'><img src='https://i.postimg.cc/Zq91sdhK/by-country.jpg' border='0' width=800px alt='by-country'/></a>
    <h4> - Netflix media by country & year: </h4>
    <p>When looking at the data by countries, we can see that the U.S., India, and the U.K. are the top three countries for the most media output on Netflix. It is worth noting that the U.S., U.K., and Spain had the most TV-show output on Netflix, while India has a relatively heavy-up on movies.</p>
    <p> Most of the Netflix media was made in the 2010s, followed by recent (2020 or after).</p><hr>
</div>
<br />
<br />



<div class="section4">
  <a href='https://postimg.cc/ppzgswgY' target='_blank'><img src='https://i.postimg.cc/VLVmk1gT/data-viz.jpg' border='0' width=800px alt='data-viz'/></a>
  <h4 align="left"> - Netflix media genre by director & by type: </h4>
<hr>
</div>



  
<h2>4. SQL Codes Walk-through</h2>

  <p> Process: </br>
    1. data loading: loading csv file to Sequel</br>
    2. data cleansing: removing null values, unifying measurements </br>
    3. data analysis</p><hr>
  
<p> 2. In the data cleansing process, I dropped the null values and noticed that there are two types of units under the "duration" column: "Season" and "min". I then unified them using "concat()" and "substring()".</p>

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

  
  <p align="Left"> 3. (Production Analysis) Using the case statement, I pulled genre information by decade and excluded genres that contain 5 or fewer movies or TV shows across all decades. The information is pulled in descending order through the sum of media. </p>
  
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


  <p align="Left"> 4. Using window function, I pulled the unique ratings and their counts from the dataset, ranked in descending order. 

  <pre><code class="langugae-sql"><p style="font-size:4.5px; color: blue;">
  CREATE TABLE netflix_rating AS(
  SELECT DISTINCT rating,counts,
  ROW_NUMBER() OVER(ORDER BY counts DESC) AS ranking
    FROM(
      SELECT rating, COUNT(rating) AS counts
      FROM netflix_duplicate
      GROUP BY rating
      ) AS subquery);
  </p></code></pre>
