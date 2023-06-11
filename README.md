<h1>Analytics Project #1</h1>

<h2>Table of Contents</h2>
1. Description<br/>
2. Languages and Utilities Used<br/>
3. Insights Display<br/>
4. SQL Codes Display<br/>
<br />

<h2>1. Description</h2>
This project utilizes Netflix data which includes country, genre, type, year and directors to dive into Netflix's selection of media. Using R, SQL and Excel, I was able to wrangle and manipulate and data, and visualize it by type, countries, year, genre and more.<br />
<br />

<h2>2. Languages and Environment Used</h2>
- SQL - 95%<br/> 
- R -5%<br/>
- Environment used: Macbook 13<br />
<br/>


<h2>3. Insights Display:</h2>

<h4 align="left">
- Netflix media & media length by type </h4>
<img src="https://imgtr.ee/images/2023/06/09/Koedz.png" alt="Koedz.png" border="0" />
<p align=left> As shown above, more than 96% of Netflix's media is made up by movies. While TV only makes up less than 4% of the total media, its individual length is much longer than its movie counterpart. </p><br/>
<p align=left> When comparing the two types by length, the media type of TV makes up about 30% of the total media content length, which shows that it is a very important media type for Netflix. In this chart, I converted "Season" to "min" to match the movie length. (Here we assume 1 season = 12 episodes, and 1 episode = 55 minutes according to thrillist.com.) </p>
<br />

<h4 align="left">
 -Netflix media by country & year</h4>
 


<pre><code class="language-sql">
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
5 rows in set (0.01 sec);
</code></pre>




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
