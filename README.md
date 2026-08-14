# concert-rank
As an avid concert goer and music enjoyer, I want to build a schema to keep track of which shows I enjoy the most. SQL seems like a fun way to make it happen.
This builds a relational database project for tracking concerts attended and ranking/reviewing them. Easier to keep track of overall experience across multiple shows and festivals.

## Schema Overview

| Table       | Purpose                                               |
|-------------|-------------------------------------------------------|
| `artists`   | Musicians/bands (name, genre, formed year, country)   |
| `venues`    | Concert venues (name, city, capacity)                 |
| `concerts`  | A specific artist playing a specific venue on a date  |
| `users`     | People doing the ranking                              |
| `rankings`  | A user's rating (1-10) + review of a concert          |
| `setlists`  | Songs played at a given concert, in order             |

```
artists ─┐
         ├─< concerts >─┐
venues ──┘              ├─< rankings >-users
                         └─< setlists
```

## Files

- `schema.sql` — table definitions, keys, constraints, indexes
- `seed_data.sql` — sample data (6 artists, 3 venues, 6 concerts, 3 users, 6 rankings)
- `queries.sql` — 8 example queries: top-rated concerts, personal top 5, artist averages, venue popularity, per-user ranking (window function), unranked concerts, full setlist, above-average raters

## Getting Started

Works with PostgreSQL or SQLite (SQLite users: swap `SERIAL` for
`INTEGER PRIMARY KEY AUTOINCREMENT` and `BOOLEAN` for `INTEGER` in `schema.sql`).

**PostgreSQL:**
```bash
createdb concert_rankings
psql concert_rankings -f schema.sql
psql concert_rankings -f seed_data.sql
psql concert_rankings -f queries.sql
```

**SQLite:**
```bash
sqlite3 concert_rankings.db < schema.sql
sqlite3 concert_rankings.db < seed_data.sql
sqlite3 concert_rankings.db < queries.sql
```

## Future options to expand on

- Add a `friends` or `follows` table for a social ranking feed
- Add `ticket_price` to `concerts` and analyze price vs. rating
- Add a view for "most improved artist" (rating trend over multiple tours, only applicable to a few artists)
