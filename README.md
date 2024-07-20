# Movie-recomendation-system
Worried what to watch ?
we have got ya!

# Movie Recommendation System

## Overview
This repository contains a movie recommendation system that suggests similar movies based on a user's favorite movie. The system utilizes Natural Language Processing (NLP) techniques to analyze movie overviews and compute similarity scores.

## Features
- Load and explore a movie dataset.
- Extract features using TF-IDF vectorization.
- Calculate cosine similarity scores between movies.
- Recommend top 30 similar movies based on a user's input.

## Dataset
The dataset used in this project is sourced from [YBI Foundation's Movie Recommendation Dataset](https://github.com/YBI-Foundation/Dataset/raw/main/Movies%2@Recommendation.csv). It contains various attributes of movies such as title, genre, language, budget, popularity, release date, revenue, runtime, vote count, homepage, keywords, overview, production house, production country, spoken language, tagline, cast, crew, and director.

## Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/movierecommendation.git
   cd movierecommendation
   ```

2. Install the required libraries:
   ```sh
   pip install pandas numpy scikit-learn
   ```

## Usage

1. Load the dataset and explore its structure:
   ```python
   import pandas as pd
   import numpy as np
   df = pd.read_csv("https://github.com/YBI-Foundation/Dataset/raw/main/Movies%2@Recommendation.csv")
   print(df.head())
   ```

2. Check the dataset information:
   ```python
   print(df.info())
   ```

3. Extract features using TF-IDF vectorizer:
   ```python
   from sklearn.feature_extraction.text import TfidfVectorizer
   tfidf = TfidfVectorizer()
   x = tfidf.fit_transform(df['Movie Overview'].values.astype('U'))
   print(x.shape)
   ```

4. Calculate cosine similarity:
   ```python
   from sklearn.metrics.pairwise import cosine_similarity
   similarity_score = cosine_similarity(x)
   print(similarity_score.shape)
   ```

5. Get movie recommendations:
   ```python
   favorite_movie_name = input('Enter your favourite movie name: ').lower()
   all_movies_title_list = df['Movie Title'].tolist()
   sorted_similar_movies = sorted(enumerate(similarity_score[all_movies_title_list.index(favorite_movie_name)]), key=lambda x: x[1], reverse=True)

   print("Top 30 movies suggested for you:\n")
   for i, movie in enumerate(sorted_similar_movies[1:31], 1):
       index = movie[0]
       title_from_index = df[df.index == index]['Movie Title'].values[0]
       print(f"{i}. {title_from_index}")
   ```

## Example Output
```
Enter your favourite movie name: kung fu panda
Top 30 movies suggested for you:
1. Glengarry Glen Ross
2. Let's Kill Ward's Wife
3. Shade
4. Magic Mike
5. All That Jazz
6. Donnie Brasco
7. Scarface
8. The Son of No One
9. Sea of Love
10. The Hunt for Red October
11. Insomnia
12. Thomas and the Magic Railroad
13. Miss Congeniality
14. Mercury Rising
15. Still Alice
16. The Godfather: Part III
17. Parole
...
```

## Contributing
Feel free to open issues or submit pull requests for improvements and new features.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Thanks to [YBI Foundation](https://github.com/YBI-Foundation) for the dataset.
