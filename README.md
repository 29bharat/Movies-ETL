# Movies-ETL

## Resources
  
Wiki Json Data
  
Kaggle Metadata - movies_metadata.csv
  
Kaggle ratings data - Ratings.csv
## Objective
  
Extract the data from the three sources.
  
Clean up all three data sourced above and merge them by applying correct tramsformations.
  
Load the cleanedup and tramsformed data to the tables in PostgreSQL.

## Process Followed
  
Wiki data was imported from the json file and loaded into wiki_movies_df dataframe.
  
movies_metadata.csv was imported into kaggle_metadata dataframe and ratings.csv was imported into ratings dataframe.
  
We cleanedup the wiki json file by combining alternate titles into one list and renaming and merging all the duplicate columns. thsi data was reloaded into the wiki_movies_df.
  
A master function movies_etl is created to comb through the wiki dataframe further and correct all the discrepancies after merging with the kaggle metadata. This function calls two other functions parse_dollar and fill_missing_kaggle_data to format and realign the data in a single dataframe movies_df by further extracting only the required and relevant columns.
  
Ratings dataframe was regrouped and pivoted and finally merged wiith the movies_df to get final dataframe with the ratings info for each movie.
  
Lastly, these two dataframes were loaded into tables in postgresql by replacing any existing data in these tables - movies and movies_with_ratings.
  
## Assumptions
  
1. We have captured only those rows where imdb_link has 7 digits as id's assuming that all data has only 7 digits. i fthere was any imdb_link with a diff id format - we have mssed those in our ETL.
  
2. We dropped columns where 90% of values is null. Wiki being not a very reliable source, its possibel that we have dropped some valuable datapoints that could have changed our final analysis.
  
3. If a movie was lengthy and made in more than 1 part - we would drop them.
  
4. All rows where video was null is dropped assuming that its a dummy row.
  
5. We might have dropped more accurate data when dropping columns coming from wiki - i.e'title_wiki','release_date_wiki','Language','Production company(s)' .  For few other columns, we picked up data from wiki only when kaggle data was missing assuming that kaggle is more accurate and reliable.
  
There are quite a few more assumptions that have been made in this ETL process avoiding which could have resulted in a different outcome.
