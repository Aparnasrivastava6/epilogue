# Epilogue
### Personalized Book Discovery & Recommendation System

## 1. Project Overview

Epilogue is a machine-learning-based book discovery system designed to help readers find books that genuinely align with their interests, reading preferences, and evolving tastes.

Rather than relying solely on popularity, ratings, or predefined genres, Epilogue aims to develop an understanding of individual readers and provide increasingly personalized recommendations as they interact with the system.

## 2. Problem Statement

Readers often struggle to discover their next book. Traditional recommendation platforms frequently rely on popularity, average ratings, broad genre classifications, or recommendations similar to books a reader has already consumed.

These approaches may repeatedly recommend familiar books while failing to discover books that align with a reader's deeper interests, preferences, and reading patterns.

Epilogue aims to make book discovery more personalized, meaningful, and exploratory.

## 3. Project Objectives

- Build a personalized book recommendation system using machine learning.
- Explore content-based and collaborative recommendation approaches.
- Develop a system capable of learning reader preferences over time.
- Provide recommendations for new users who have little or no interaction history.
- Explore ways to recommend books beyond a reader's explicitly selected genres.
- Create an interactive book discovery experience.
- Develop a project that demonstrates practical understanding of machine learning, data processing, NLP, recommendation systems, and software development.

## 4. Personalization Strategy

Epilogue will gradually develop a reader profile using multiple sources of preference information:

### Explicit Preferences
Information directly provided by readers, such as genres they enjoy during onboarding.

### User Interactions
Reader activity such as rating books, saving books, marking books as read, expressing interest, or rejecting recommendations.

### Inferred Preferences
Patterns learned by the system from reader behavior, book characteristics, and interactions.

### Exploratory Discovery
Recommendations that introduce readers to books outside their usual preferences while remaining relevant to their interests.

The reader's preference profile should evolve rather than remain static.

## 5. Initial User Onboarding

New users will initially be presented with genres available within Epilogue's dataset and invited to select genres they enjoy.

These selections will provide an initial understanding of their interests and help generate their first recommendations without requiring them to have an existing reading history or select a fixed number of favorite books.

This approach addresses the initial cold-start problem for new users.

## 6. Machine Learning Goals

The project will explore and implement machine-learning techniques relevant to book recommendation, including:

- Content-based recommendation
- Collaborative filtering
- Natural Language Processing
- Book feature representation
- User preference modeling
- Similarity measurement
- Recommendation evaluation
- Personalized ranking

The final techniques and model architecture will be selected through experimentation and evaluation rather than predetermined.

## 7. Dataset

Epilogue currently uses datasets containing book metadata, user ratings, user information, and book genre information.

The datasets will be explored, validated, and analyzed before being used for model development.

Original datasets will be preserved in their raw form. Any cleaning, transformation, feature engineering, or derived data will be stored separately.

## 8. Guiding Principles

- Personalization over generic popularity.
- Exploration over repetitive recommendations.
- Data-driven decisions over assumptions.
- Explainability and understanding over blindly implementing models.
- Preserve original data.
- Evaluate recommendation quality rather than relying on intuition.
- Build incrementally and document important decisions.

## 9. Learning Objectives

Epilogue is also a learning project. Its development will be used to understand and apply:

- Python and data processing
- Data analysis
- Machine learning fundamentals
- Natural Language Processing
- Recommendation systems
- Model evaluation
- Software architecture
- API and application development

All major implementation decisions should be understood, documented, and justified.

## 10. Long-Term Vision

The long-term vision for Epilogue is to create an intelligent and personalized book discovery experience that understands not only what readers have enjoyed, but also the patterns behind their interests.

Epilogue should help readers discover books they might never have found themselves—not merely recommend more of the same.

## 11. Current Development Status

**Phase:** Project restart and foundational planning

**Completed:**
- Initial project concept defined
- Dataset acquisition
- Initial dataset documentation
- Project structure created
- Initial personalization concept established

**Current focus:**
- Dataset understanding
- Project planning
- Establishing the technical foundation
- Learning recommendation-system fundamentals

No final recommendation architecture or machine-learning model has been selected yet.




### Finding 02 — Metadata availability is source-dependent

Metadata completeness varies substantially across the dataset's sources.

- All 7,976 Book-Crossing-only books are missing genre, Goodreads rating metadata, and language information.
- Goodreads metadata is present for the Goodbooks records, including books belonging to both sources.
- Publisher information is available for all Book-Crossing-only books, but missing for all 10,000 records associated with Goodbooks.
- Genre information is almost complete for the Goodbooks records, with only 12 missing values in Goodbooks-only records and 1 in the overlapping group.
- Language information is also incomplete within the Goodbooks records.

**Implication:** Metadata availability is structured by data source, rather than being random. Any content-based recommendation model must account for uneven feature availability to avoid systematically disadvantaging books from a particular source.





### Catalog integrity — Finding 03
Unique book identifiers

No repeated non-missing ISBNs

575 records without ISBNs

Repeated titles are common and mostly represent different author entries

Two exact title–author combinations occur twice, with different ISBNs






### Finding 04 — Preliminary conclusions
- Ratings from the two sources use different original scales.
- Goodbooks ratings are on a 1–5 scale.
- Book-Crossing ratings are on a 1–10 scale.
- The dataset is heavily dominated by Goodbooks interactions.
- Ratings are skewed toward the higher end in both sources.
- The normalized rating column contains fractional values for Book-Crossing.
- Sentiment labels are derived features and need their transformation logic verified.







### Finding 05 — Rating Distribution

The rating distribution in the 100,000-interaction sample is strongly concentrated toward higher ratings. Ratings of 4.00 and 5.00 account for 67.51% of all interactions, with 4.00 being the most frequent rating at 34.89%, followed by 5.00 at 32.62%. This indicates a positive skew in the observed rating distribution, suggesting that high ratings are more commonly assigned than low ratings.

However, this pattern may reflect user rating behavior, selection effects, or differences between the underlying data sources rather than the quality of books alone.







### Finding 06 — Rating Distribution Varies by Source

The rating distributions differ between Goodbooks and Book-Crossing. Goodbooks ratings are concentrated around whole-number values, particularly 4.00 and 5.00, whereas Book-Crossing ratings are distributed across a wider range of fractional values on the normalized scale.

Although both sources show a tendency toward higher ratings, their distributions are not identical. Normalizing ratings to a common scale does not necessarily eliminate differences in rating behavior between datasets. Therefore, source-level differences should be considered in subsequent analyses and recommendation model development







### Finding 07 — Rating Frequency per Book

The 100,000-interaction sample contains ratings for 10,661 unique books. The average number of ratings per book is 9.38, while the median is only 4. The rating count ranges from 1 to 392, with a standard deviation of 20.55. The considerable difference between the mean and median, along with the high maximum, indicates that rating activity is unevenly distributed across books, with a relatively small number of books receiving substantially more ratings than the majority.



### Finding 08 — Concentration of Rating Activity

Rating activity is concentrated among a relatively small portion of the rated books. Approximately 62.05% of books received five or fewer ratings, while 80.45% received ten or fewer ratings. Only 108 books received more than 100 ratings. This indicates that most books have limited interaction data available, while a small subset receives considerably more engagement.




### Finding 09 — Long-Tail Distribution of Rating Counts

The histogram of rating counts per book reveals a strongly right-skewed, long-tail distribution. A large number of books are clustered at low rating counts, while progressively fewer books have higher numbers of ratings. The distribution extends to 392 ratings, but books with such high interaction counts represent a small fraction of the rated catalog. This pattern highlights the uneven distribution of user interactions and suggests a potential popularity bias in recommendation systems, where highly rated books by frequency of interaction may receive greater visibility than books with limited interaction data.




### Finding 10 — Rating Activity Is Distributed Across Books, but Popularity Is Uneven

The ten most frequently rated books account for 2.997% of all interactions in the 100,000-rating sample. Although these books receive substantially more ratings individually than most books in the dataset, collectively they represent only a small proportion of total rating activity.

The top-rated-by-frequency books include popular titles such as *The Hunger Games*, the *Harry Potter* series, *To Kill a Mockingbird*, *The Great Gatsby*, *Twilight*, and *The Hobbit*.

This suggests that interaction activity is spread across a large number of books rather than being dominated entirely by a small group of titles. However, rating frequency remains unevenly distributed, with certain books receiving substantially more interactions than others.





### Finding 11 — User Rating Activity Is Extremely Sparse

The user rating activity distribution shows that users contribute relatively few ratings to the dataset. Across 46,184 unique users, the average number of ratings per user is 2.17, while the median is 2.

The distribution indicates that 25% of users have rated only one book, and 75% of users have rated three or fewer books. Although the most active user has rated 38 books, this level of activity is considerably higher than that of the typical user.

This suggests that the dataset contains limited information about the reading preferences of most users. Consequently, building reliable user preference profiles may be challenging, particularly for recommendation approaches that depend heavily on individual rating histories.




### Finding 12 — The User–Book Interaction Matrix Is Extremely Sparse

The interaction matrix constructed from the 100,000-rating sample contains 46,184 unique users and 10,661 unique books, resulting in 492,367,624 possible user–book combinations.

Only 100,000 unique user–book interactions are observed, corresponding to a matrix density of approximately 0.02031% and sparsity of 99.97969%.

This indicates that the dataset contains very limited observed interaction information relative to the number of possible user–book relationships. Most user–book pairs have no recorded rating, creating a significant challenge for recommendation models that depend on interaction patterns.

The absence of an interaction cannot be interpreted as a negative preference, since it only indicates that no rating is observed for that user–book pair in the dataset.

The extreme sparsity, combined with low user rating activity, suggests that collaborative recommendation approaches may face significant difficulties learning reliable user preferences from this sample alone.