# recommendation_algorithm

### Goal
To build a collaborative filtering recommendation system that predicts movie ratings for a new user (User 0) based on the rating patterns of similar users in the ML-20M dataset, and to evaluate the quality of those predictions

## 2. Dataset
### Source
**MovieLens 20M (ML-20M)** - published by GroupLens Research, University of Minnesota.  
Full dataset: ~20 million ratings, ~138,000 users, ~27,000 movies.  
This project loads the first **10,000 rows** of each file for prototyping purposes and to manage memory/processing time

### Files Used
| File | Columns | Description |
|---|---|---|
| `movies.csv` | `movieId`, `title`, `genres` | Movie metadata |
| `ratings.csv` | `userId`, `movieId`, `rating`, `timestamp` | User-movie ratings |

### Method: Pipeline Overview
| Step | Action |
|---|---|
| 1 | Ratings split 80/20 into training and test sets |
| 2 | Personal ratings (User 0, 20 movies) added to training set |
| 3 | User-item matrix built; missing values filled with per-user means |
| 4 | NMF (`n_components=20`, `init='nndsvda'`, `max_iter=500`) trained |
| 5 | Full ratings matrix reconstructed via `W × H` |
| 6 | RMSE computed on held-out test ratings |
| 7 | Top 20 recommendations for User 0 extracted from unrated movies |
| 8 | Cold-start fallback implemented using Pearson correlation |
