<img width="671" height="376" alt="image" src="https://github.com/user-attachments/assets/43cfd4e5-3452-4655-a81d-67575b80bb2c" />


# Spotify Advanced SQL Project and Query Optimization P-6
Project Category: Advanced


## Overview
This project involves analyzing a Spotify dataset with various attributes about tracks, albums, and artists using **SQL**. It covers an end-to-end process of normalizing a denormalized dataset, performing SQL queries of varying complexity (easy, medium, and advanced), and optimizing query performance. The primary goals of the project are to practice advanced SQL skills and generate valuable insights from the dataset.

```sql
-- create table
DROP TABLE IF EXISTS spotify;
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);
```
## Project Steps

### 1. Data Exploration
Before diving into SQL, it’s important to understand the dataset thoroughly. The dataset contains attributes such as:
- `Artist`: The performer of the track.
- `Track`: The name of the song.
- `Album`: The album to which the track belongs.
- `Album_type`: The type of album (e.g., single or album).
- Various metrics such as `danceability`, `energy`, `loudness`, `tempo`, and more.

### 4. Querying the Data
After the data is inserted, various SQL queries can be written to explore and analyze the data. Queries are categorized into **easy**, **medium**, and **advanced** levels to help progressively develop SQL proficiency.

#### Easy Queries
- Simple data retrieval, filtering, and basic aggregations.
  
#### Medium Queries
- More complex queries involving grouping, aggregation functions, and joins.
  
#### Advanced Queries
- Nested subqueries, window functions, CTEs, and performance optimization.

### 5. Query Optimization
In advanced stages, the focus shifts to improving query performance. Some optimization strategies include:
- **Indexing**: Adding indexes on frequently queried columns.
- **Query Execution Plan**: Using `EXPLAIN ANALYZE` to review and refine query performance.
  
---
## 15 Practice Questions

### Easy Level
1. Retrieve the names of all tracks that have more than 1 billion streams.
---
<img width="411" height="51" alt="image" src="https://github.com/user-attachments/assets/a2da8f17-fc8d-4c2f-b9d9-fcdfa36b33f5" />

---
2. List all albums along with their respective artists.
---
<img width="365" height="27" alt="image" src="https://github.com/user-attachments/assets/49b4a515-2b5a-426f-97a2-b3dda32a4a71" />

---
3. Get the total number of comments for tracks where `licensed = TRUE`.
---
<img width="580" height="45" alt="image" src="https://github.com/user-attachments/assets/914f5e41-cbb1-4a17-8d01-04db9fefcfb1" />

---
4. Find all tracks that belong to the album type `single`.
---
<img width="321" height="42" alt="image" src="https://github.com/user-attachments/assets/59cd5dfd-ec55-44de-980d-79a104dd3833" />

---
5. Count the total number of tracks by each artist.
---
<img width="528" height="45" alt="image" src="https://github.com/user-attachments/assets/a2546ce0-8d2b-4909-8be6-f5a8e3d23d3c" />

---
### Medium Level
1. Calculate the average danceability of tracks in each album.
---
<img width="587" height="40" alt="image" src="https://github.com/user-attachments/assets/7fcc0a12-5b1c-49af-9c07-bb71ffdec4d3" />

---
2. Find the top 5 tracks with the highest energy values.
---
<img width="590" height="47" alt="image" src="https://github.com/user-attachments/assets/5314ee10-e72f-41b7-9a53-308abac7bd48" />

---
3. List all tracks along with their views and likes where `official_video = TRUE`.
---
<img width="481" height="46" alt="image" src="https://github.com/user-attachments/assets/070f8785-1285-4da0-a82b-9e9c6b13bdd7" />

---
4. For each album, calculate the total views of all associated tracks.
---
<img width="479" height="50" alt="image" src="https://github.com/user-attachments/assets/29d01cce-90cc-4aa4-b858-ab1070a1b8d7" />

---
5. Retrieve the track names that have been streamed on Spotify more than YouTube.
---
<img width="886" height="86" alt="image" src="https://github.com/user-attachments/assets/906398b6-f3ce-4b8d-ae19-828ba1e6a10f" />

---
### Advanced Level
1. Find the top 3 most-viewed tracks for each artist using window functions.
2. Write a query to find tracks where the liveness score is above the average.
3. **Use a `WITH` clause to calculate the difference between the highest and lowest energy values for tracks in each album.**
```sql
WITH cte
AS
(SELECT 
	album,
	MAX(energy) as highest_energy,
	MIN(energy) as lowest_energery
FROM spotify
GROUP BY 1
)
SELECT 
	album,
	highest_energy - lowest_energery as energy_diff
FROM cte
ORDER BY 2 DESC
```
   
5. Find tracks where the energy-to-liveness ratio is greater than 1.2.
6. Calculate the cumulative sum of likes for tracks ordered by the number of views, using window functions.


Here’s an updated section for your **Spotify Advanced SQL Project and Query Optimization** README, focusing on the query optimization task you performed. You can include the specific screenshots and graphs as described.

---

## Query Optimization Technique 

To improve query performance, we carried out the following optimization process:

- **Initial Query Performance Analysis Using `EXPLAIN`**
    - We began by analyzing the performance of a query using the `EXPLAIN` function.
    - The query retrieved tracks based on the `artist` column, and the performance metrics were as follows:
        - Execution time (E.T.): **7 ms**
        - Planning time (P.T.): **0.17 ms**  

- **Index Creation on the `artist` Column**
    - To optimize the query performance, we created an index on the `artist` column. This ensures faster retrieval of rows where the artist is queried.
    - **SQL command** for creating the index:
      ```sql
      CREATE INDEX idx_artist ON spotify_tracks(artist);
      ```

- **Performance Analysis After Index Creation**
    - After creating the index, we ran the same query again and observed significant improvements in performance:
        - Execution time (E.T.): **0.153 ms**
        - Planning time (P.T.): **0.152 ms**
    - Below is the **screenshot** of the `EXPLAIN` result after index creation:
      ![EXPLAIN After Index](https://github.com/Emmanul-wekesa-bit-Spotify-Data-Analysis-using-SQL/blob/main/spotify_explain_after_index.png)



This optimization shows how indexing can drastically reduce query time, improving the overall performance of our database operations in the Spotify project.
---

## Technology Stack
- **Database**: PostgreSQL
- **SQL Queries**: DDL, DML, Aggregations, Joins, Subqueries, Window Functions
- **Tools**: pgAdmin 4 (or any SQL editor), PostgreSQL (via Homebrew, Docker, or direct installation)

## How to Run the Project
1. Install PostgreSQL and pgAdmin (if not already installed).
2. Set up the database schema and tables using the provided normalization structure.
3. Insert the sample data into the respective tables.
4. Execute SQL queries to solve the listed problems.
5. Explore query optimization techniques for large datasets.

---

## Next Steps
- **Visualize the Data**: Use a data visualization tool like **Tableau** or **Power BI** to create dashboards based on the query results.
- **Expand Dataset**: Add more rows to the dataset for broader analysis and scalability testing.
- **Advanced Querying**: Dive deeper into query optimization and explore the performance of SQL queries on larger datasets.

---

## Contributing
If you would like to contribute to this project, feel free to fork the repository, submit pull requests, or raise issues.

---


