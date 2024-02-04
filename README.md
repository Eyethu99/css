# css
# -*- coding: utf-8 -*-
"""
Created on Sun Feb  4 16:39:20 2024

@author: Eyethu Thwala
"""

import pandas as pd

# specifying the first column as index column
df = pd.read_csv("movie_dataset.csv", index_col=0)

# replacing spaces with underscore in a dataframe
df.columns = df.columns.map(lambda x : x.replace('.', '_').replace(' ', '_'))

# Allows you to see all rows
pd.set_option('display.max_rows',None)

x = df["Revenue_(Millions)"].mean()

df["Revenue_(Millions)"].fillna(x, inplace = True) 

x2 = df["Metascore"].mean()

df["Metascore"].fillna(x2, inplace = True) 

# -----------------------------------------------------------------------------------------------------------------------
# Answer for question 1

# Find the index of the highest-rated movie
index_highest_rated = df['Rating'].idxmax()

# Retrieve the details of the highest-rated movie
highest_rated_movie = df.loc[index_highest_rated]

print(highest_rated_movie)

# ------------------------------------------------------------------------------------------------------------------------
# Answer for question 2

average_revenue = df['Revenue_(Millions)'].mean()
print("Average revenue is: " , average_revenue)

# ------------------------------------------------------------------------------------------------------------------------
# Answer for question 3

# Create a boolean mask to filter rows for the desired time period
mask = (df['Year'] >= 2015) & (df['Year'] <= 2017)

# Apply the mask to filter the DataFrame
filtered_df = df[mask]

# Calculate the average for the specified column in the filtered DataFrame
average_revenue_2015_2017 = filtered_df['Revenue_(Millions)'].mean()

print("The average revenue between year 2015 to 2017 is: ", average_revenue_2015_2017)

# ------------------------------------------------------------------------------------------------------------------------
# Answer for question 4

# Create a boolean mask to filter rows for the year 2016
mask_2016 = (df['Year'] == 2016)

# Apply the mask to filter the DataFrame
movies_2016 = df[mask_2016]

# Count the number of rows in the filtered DataFrame
num_movies_2016 = len(movies_2016)

print("The number of movies is: " , num_movies_2016)

# ------------------------------------------------------------------------------------------------------------------------
#Answer for question 5

# Create a boolean mask to filter rows directed by Christopher Nolan
mask_nolan = (df['Director'] == 'Christopher Nolan')

# Apply the mask to filter the DataFrame
movies_nolan = df[mask_nolan]

# Count the number of rows in the filtered DataFrame
num_movies_nolan = len(movies_nolan)

print("The number of movies is directed by Christopher Nolan: " , num_movies_nolan)

# -------------------------------------------------------------------------------------------------------------------------
#Answer for question 6

# Create a boolean mask to filter rows with a rating of at least 8.0
mask_high_rating = (df['Rating'] >= 8.0)

# Apply the mask to filter the DataFrame
high_rated_movies = df[mask_high_rating]

# Count the number of rows in the filtered DataFrame
num_high_rated_movies = len(high_rated_movies)

print("The number of movies with a rating of at least 8.0 is: ", num_high_rated_movies)

# -------------------------------------------------------------------------------------------------------------------------
#Answer for question 7

# Create a boolean mask to filter rows directed by Christopher Nolan
mask_nolan = (df['Director'] == 'Christopher Nolan')

# Apply the mask to filter the DataFrame
movies_nolan = df[mask_nolan]

# Calculate the median rating for movies directed by Christopher Nolan
median_rating_nolan = movies_nolan['Rating'].median()

print("The median is: ", median_rating_nolan)

# ----------------------------------------------------------------------------------------------------------------------------
#Answer for question 8

# Group the data by 'year' and calculate the mean rating for each year
average_rating_by_year = df.groupby('Year')['Rating'].mean()

# Find the year with the highest average rating
max_avg_rating_year = average_rating_by_year.idxmax()

print("The year is: ", max_avg_rating_year)

# --------------------------------------------------------------------------------------------------------------------------------
#Answer for question 9

# Create a boolean mask to filter rows for the years 2006 and 2016
mask_years = (df['Year'] == 2006) | (df['Year'] == 2016)

# Apply the mask to filter the DataFrame
movies_2006_2016 = df[mask_years]

# Calculate the number of movies made in 2006 and 2016
num_movies_2006 = len(movies_2006_2016[movies_2006_2016['Year'] == 2006])
num_movies_2016 = len(movies_2006_2016[movies_2006_2016['Year'] == 2016])

# Calculate the percentage increase
percentage_increase = ((num_movies_2016 - num_movies_2006) / num_movies_2006) * 100

print("The percentage increase is: ", percentage_increase)

# -------------------------------------------------------------------------------------------------------------------------------------
#Answer for question 10

# Combine all actors from all movies into a single list
all_actors = df['Actors'].str.split(',').explode()

# Count the occurrences of each actor
actor_counts = all_actors.str.strip().value_counts()

# Get the most common actor
most_common_actor = actor_counts.idxmax()
num_movies_with_most_common_actor = actor_counts.max()

print("The most common actor is: ", most_common_actor)

# -------------------------------------------------------------------------------------------------------------------------------------
#Answer for question 11

# Get the unique genres
unique_genres = df['Genre'].str.split(',').explode().str.strip().unique()

# Count the number of unique genres
num_unique_genres = len(unique_genres)

print("The number of unique genres is: ", num_unique_genres)

