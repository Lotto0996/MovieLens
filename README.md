# MovieLens

Objective: Using movies and their coresponding ratings data, try to find out:
1. If one user tends to rate similar movies same or similar ratings (Reflect his/her taste)
2. Is there any positive linear relationship between number of movies a user rated and the rating he/she gave.
Thus, we could recommend the similar movie that he/she hasn't rated (watched).

Drama and Comedy are the most movie genre, Thriller, Action, Romance and Adventure are the following ones.

Tried clustering, didn't seem to be reasonable. It's simply use movieId to cluster. So I exported the data into SQL, and use market basket analysis similar methoid, to combine two genres to find out the most frequent conbination.

SELECT genre_1,genre_2, COUNT(movieId) movie_COUNT FROM ( SELECT a.movieId, a.genres genre_1, b.genres genre_2, b.movieId bm FROM ash.Tredence a, ash.Tredence b WHERE a.movieId=b.movieId and a.genres <> b.genres and a.genres < b.genres ) Temp GROUP BY genre_1,genre_2 order by movie_COUNT desc;

Yes, this user did give different cluster significantly different ratings, according to the p value of cluster 1,2 as oppose to Cluster 0. Cluster 1 and cluster 2 have lower ratings comparing to cluster 0.

Opposite to I assumed, turns out the more same genre movie a user watched, the lower average of rating he/she will give. Since the coef of count is negative, means if 1 more movie is watched, the average rating will decrease 0.001.
