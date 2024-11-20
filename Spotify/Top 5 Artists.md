## Problem

Assume there are three Spotify tables: artists, songs, and global_song_rank, which contain information about the artists, songs, and music charts, respectively.

Write a query to find the top 5 artists whose songs appear most frequently in the Top 10 of the global_song_rank table. Display the top 5 artist names in ascending order, along with their song appearance ranking.

If two or more artists have the same number of song appearances, they should be assigned the same ranking, and the rank numbers should be continuous (i.e. 1, 2, 2, 3, 4, 5).

## Solution

    SELECT
      A.artist_name, A.dense_rank AS artist_rank
    FROM
      (
        SELECT A.artist_name, 
        DENSE_RANK() OVER (ORDER BY COUNT(G.rank) DESC)
        FROM 
          global_song_rank AS G,
          artists AS A,
          songs AS S
        WHERE
          G.rank <=10
          AND A.artist_id = S.artist_id
          AND S.song_id = G.song_id
        GROUP BY A.artist_name

      ) AS A
    WHERE 
      dense_rank <=5
  
