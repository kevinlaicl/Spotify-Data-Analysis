# Spotify-Data-Analysis
## Project Overview

## Dataset Overview
```sql
CREATE TABLE IF NOT EXISTS public.spotify
(
    artist character varying(255) COLLATE pg_catalog."default",
    track character varying(255) COLLATE pg_catalog."default",
    album character varying(255) COLLATE pg_catalog."default",
    album_type character varying(50) COLLATE pg_catalog."default",
    danceability double precision,
    energy double precision,
    loudness double precision,
    speechiness double precision,
    acousticness double precision,
    instrumentalness double precision,
    liveness double precision,
    valence double precision,
    tempo double precision,
    duration_min double precision,
    title character varying(255) COLLATE pg_catalog."default",
    channel character varying(255) COLLATE pg_catalog."default",
    views bigint,
    likes bigint,
    comments bigint,
    licensed boolean,
    official_video boolean,
    stream bigint,
    energyliveness double precision,
    most_playedon character varying(50) COLLATE pg_catalog."default"
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.spotify
    OWNER to postgres;
```
## Understand Popularity Patterns
1. Identify high-performing content to prioritise promotion on vital content
2. Map artist-album relationships to analyse artist productivity and release frequency
3. Engagement on licensed content to see whether licensed tracks getting strong user engagement for validating licensed investment
4. Format-based performance to support decisions on whether to push single releases
5. Artist Output Volume to highlight highly active artists that Spotify may want to support or spotlight

## Analyse Audio Features Trends
** Understand musical feature values by album
Used for mood-based playlist targeting
** Highlight High Energy Tracks
Used for gym, party, mood-based playlist targeting
** Content performance by format
Tested whether official content performs better
** Viewers by albums
Useful for album-focused campaign planning
** Platform performance comaprison
Could reveal audio-only streaming behaviour

## Artist-Level Insights
**Identify Top Visual Hits per Artist**  
Find the top 3 most-viewed track for each artist so that we could show the popular songs on artist pages
```sql
WITH ranking_artist
AS
(SELECT
	artist,
	track,
	SUM(views) AS total_views,
	DENSE_RANK() OVER(PARTITION BY artist ORDER BY SUM(views) DESC) AS rank
FROM spotify
GROUP BY 1, 2
ORDER BY 1, 3 DESC
)
SELECT * FROM ranking_artist
WHERE rank <= 3
```
**Identify Live-Feeling Tracks**  
Find tracks where the liveness score is above the average so that we could create live-vibe playlists or promote concert-related content
```sql
SELECT
	album,
	artist,
	liveness
FROM spotify
WHERE liveness > (SELECT AVG(liveness) FROM spotify)
ORDER BY 3 DESC
```

**Analyse Audio Energy Diversity**  
The variety in energy each album has so that we could distinguish album with emotional range vs. consistent tone
```sql
WITH energy_table
AS
(SELECT
	album,
	MAX(energy) AS highest_energy,
	MIN(energy) AS lowest_energy
FROM spotify
GROUP BY 1)
SELECT
	album,
	highest_energy - lowest_energy AS energy_difference
FROM energy_table
ORDER BY 2 DESC
```
