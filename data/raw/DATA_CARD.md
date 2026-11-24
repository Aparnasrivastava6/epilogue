# Epilogue book-recommendation dataset

Merged and cleaned from two public research datasets. Nothing here is synthetic or scraped by me.

## Sources
- **Goodbooks-10k** (Zygmunt Zając, github.com/zygmuntz/goodbooks-10k): 10,000 books, ~6M ratings (1-5), shelf tags. Goodreads data collected in 2017. Check the repo's LICENSE before redistributing.
- **Book-Crossing** (Ziegler et al., 2004 crawl, mirrored on GitHub): explicit ratings (1-10) and coarse user demographics. Academic/research dataset; cite Ziegler et al. (WWW 2005) if you publish.

## Files
| file | rows | what it is |
|---|---|---|
| books.csv | 17,976 | one row per book (duplicate editions merged) |
| ratings.csv.gz | 6,140,665 | user-book ratings, no duplicates |
| users.csv | 67,017 | user_uid, source, age, country, activity stats |
| book_genres.csv | ~39k | up to 4 genres per book with shelf counts (Goodbooks books only) |
| ratings_sample_100k.csv | 100,000 | random sample for quick experiments |

## Key columns
- `ratings.rating_raw`: native scale (1-5 Goodbooks, 1-10 Book-Crossing). `rating_5`: both on a 1-5 scale. `sentiment`: 1 = liked (>= 4/5), -1 = disliked (<= 2/5), 0 = neutral.
- `books.genres`: pipe-separated, from the most common Goodreads shelves (whitelist of 70 genre tags, min 10 shelvings).
- `books.goodreads_*`: Goodreads' own average, rating count and text-review count (counts only, not review text).
- `user_uid`: Goodbooks users keep their id; Book-Crossing users are offset by 10,000,000.

## Cleaning done
- Book-Crossing: dropped implicit 0 ratings, invalid ISBNs, bad years (<1500 or >2026), ages outside 5-100; fixed HTML entities, ALL-CAPS names, nested "(series)" suffixes.
- Merged editions of the same book (ISBN-13 match, then normalized title + first author).
- Recomputed Goodbooks ISBN-13 (the source column loses its last digit); blanked ISBNs shared by different books.
- Book-Crossing-only books kept only if they have >= 5 ratings; Book-Crossing users kept only with >= 3 ratings.
- Zero duplicate (user, book) pairs, zero orphan ratings.

## Known limits
- No free-text review bodies are included, only review counts.
- Genres, language and Goodreads stats exist only for the 9,987 books that came from Goodbooks-10k (about 56%).
- Book-Crossing is from 2004 and skews to US/Canada readers; Goodbooks is from 2017.
