# TensorFlow/models/official/recommendation
### Data
* `movielens/ratings.csv`
```
userId,movieId,rating,timestamp

# official/recommendation/movielens.py L68
RATING_COLUMNS = [USER_COLUMN, ITEM_COLUMN, RATING_COLUMN, TIMESTAMP_COLUMN] 
```
* `movielens/movies.csv`
```
MovieID,Title,Genres

# official/recommendation.movielens.py L69
MOVIE_COLUMNS = [ITEM_COLUMN, TITLE_COLUMN, GENRE_COLUMN]
```

## ratings.csv
* Sorting : (1) userId (2) timestamp
* All users had rated at least 20 movies(=items)
* ratings : 0.5 ~ 5.0

## movies.csv
* movieId : 1 ~ 3952

### `movielens.py`
```python3
def ratings_csv_to_dataframe(data_dir, dataset):
  with tf.io.gfile.GFile(os.path.join(data_dir, dataset, RATINGS_FILE)) as f:
    return pd.read_csv(f, encoding="utf-8")

def csv_to_joint_dataframe(data_dir, dataset):
  ratings = ratings_csv_to_dataframe(data_dir, dataset)

  with tf.io.gfile.GFile(os.path.join(data_dir, dataset, MOVIES_FILE)) as f:
    movies = pd.read_csv(f, encoding="utf-8")

  df = ratings.merge(movies, on=ITEM_COLUMN)
  df[RATING_COLUMN] = df[RATING_COLUMN].astype(np.float32)

  return df
```
**TEST CODE**
```python3
import pandas as pd
import numpy as np

#ratings.csv : userId,movieId,rating,timestamp
data = [[1,11,3.5,0],[2,22,0.5,1],[3,33,1.0,2],[4,44,2.0,3],[5,55,5.0,4]]
df_ratings = pd.DataFrame(data)
df_ratings.columns = ['User','Movie','Rating','Timestamp']
print("df_ratings")
print(df_ratings)
print("---------------------------------\n")
#movie.csv : movieId,Title,Genres
data_movie = [[11,"Avengers","Hero"],[22,"Spider-man","Hero"],[33,"The Conjuring","Horror"],[44,"Inside Out","Kids"],[55,"Frozen 2","Kids"]]
df_movies = pd.DataFrame(data_movie)
df_movies.columns = ['Movie','Title','Genre']
print("df_movies")
print(df_movies)
print("-------------------------------\n")
df = df_ratings.merge(df_movies, on='Movie')
df['Rating'] = df['Rating'].astype(np.float32)
print("Merged DataFrame(df.ratings + df.movies)")
print(df)
```
**RESULT**
```
df_ratings
   User  Movie  Rating  Timestamp
0     1     11     3.5          0
1     2     22     0.5          1
2     3     33     1.0          2
3     4     44     2.0          3
4     5     55     5.0          4
---------------------------------

df_movies
   Movie          Title   Genre
0     11       Avengers    Hero
1     22     Spider-man    Hero
2     33  The Conjuring  Horror
3     44     Inside Out    Kids
4     55       Frozen 2    Kids
-------------------------------

Merged DataFrame(df.ratings + df.movies)
   User  Movie  Rating  Timestamp          Title   Genre
0     1     11     3.5          0       Avengers    Hero
1     2     22     0.5          1     Spider-man    Hero
2     3     33     1.0          2  The Conjuring  Horror
3     4     44     2.0          3     Inside Out    Kids
4     5     55     5.0          4       Frozen 2    Kids
```
---------
> **RATING_COLUMN**
> `official/recommendation/neumf_model.py`
> ```python3
>   # Final prediction layer
>  logits = tf.keras.layers.Dense(
>      1,
>      activation=None,
>      kernel_initializer="lecun_uniform",
>      name=movielens.RATING_COLUMN)(
>          predict_vector)
> ```
