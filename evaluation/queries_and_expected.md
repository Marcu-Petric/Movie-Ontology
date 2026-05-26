# 1 All Films in the catalog

```sparql
PREFIX : <http://semantics.id/ns/example/film#>
SELECT ?film WHERE { ?film a :Film . }
```

Expected: 13 results
movie_432, movie_barbie, movie_chuck, movie_colectiv, movie_dark_knight, movie_dune_2, movie_gladiator, movie_inception, movie_interstellar, movie_matrix, movie_oppenheimer, movie_parasite, movie_spirited


# 2 Subscribers who watched at least one sci-fi film

```sparql
PREFIX : <http://semantics.id/ns/example/film#>
SELECT DISTINCT ?subscriber WHERE {
  ?subscriber a :Subscriber ;
              :watched ?film .
  ?film :hasGenre :genre_science_fiction .
}
```
Expected: 8 results
user_alex, user_andrei, user_carmen, user_david, user_emma, user_ken, user_lucas, user_maria

# 3 Reviews with score ≥ 9

```sparql
PREFIX : <http://semantics.id/ns/example/film#>
SELECT ?review ?score WHERE {
  ?review a :Review ;
          :reviewScore ?score .
  FILTER(?score >= 9)
}
```

Expected: 29 results 

# 4 SciFiFilm instances (inference-dependent)

```sparql
PREFIX : <http://semantics.id/ns/example/film#>
SELECT ?film WHERE { ?film a :SciFiFilm . }
```

Expected: 4 results
movie_dune_2, movie_inception, movie_interstellar, movie_matrix

# 5 Friend pairs who co-watched an artwork 

```sparql
PREFIX : <http://semantics.id/ns/example/film#>
SELECT DISTINCT ?subA ?subB ?artwork WHERE {
  ?subA :friendOf ?subB ;
        :watched ?artwork .
  ?subB :watched ?artwork .
  FILTER(STR(?subA) < STR(?subB))
}
```

Expected: 24 results
