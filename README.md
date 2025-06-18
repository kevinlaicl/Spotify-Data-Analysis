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
1. Identify high-performing content
Prioritise promotion on vital content
2. Map artist-album relationships
Analyse artist productivity and release frequency
3. Engagement on licensed content
Are licensed tracks getting strong user engagement to validate licensed investment
4. Format-based performance
Want to support decisions on whether to push single releases
5. Artist Output Volume
Highlight highly active artists that Spotify may want to support or spotlight
## Analyse Audio Features Trends
1. Understand musical feature values by album
Used for mood-based playlist targeting
2. Highlight High Energy Tracks
Used for gym, party, mood-based playlist targeting
3. Content performance by format
Tested whether official content performs better
4. Viewers by albums
Useful for album-focused campaign planning
5. Platform performance comaprison
Could reveal audio-only streaming behaviour
