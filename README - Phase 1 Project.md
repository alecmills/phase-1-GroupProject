# 1. Overview

The purpose of this project is to enhance and apply our exploratory data analysis, data cleansing and data visualization skills to a real-world problem or scenario.
   - Link to Technical Notebook: https://github.com/alecmills/phase-1-GroupProject/blob/master/student.ipynb
   - Link to final presentation:
   - Link to original data sources: https://github.com/alecmills/phase-1-GroupProject/tree/master/zippedData


# 2. Business Understanding

Microsoft has decided to directly enter the entertainment industry, specifically, by creating a new movie studio. However, the new Head of the Movie Studio does not have significant experience in this space, and needs our help in understanding what types of films are doing the best at the box office. After requesting additional detail from the new Head, she is really interested in the following:

   - What genres of movies are the most profitable at the box office (i.e. released in theatres)?
   - Do ratings of movies seem to have any type of relationship with how well they do in theatres?
   - What timeline for release should Microsoft aim for?

While answering these key questions, Microsoft's Head of the Movie Studio is looking for three concrete recommendations or actionable insights that can guide her in deciding what type of movie(s) to create!



# 3. Data Understanding and Analysis

We were provided data from a few different movie databases including:
   * [Box Office Mojo](https://www.boxofficemojo.com/)
   * [IMDB](https://www.imdb.com/)
   * [Rotten Tomatoes](https://www.rottentomatoes.com/)
   * [TheMovieDB](https://www.themoviedb.org/)
   * [The Numbers](https://www.the-numbers.com/)


We then performed exploratory data analysis on each of these databases including:
   * Opening and saving CSV and TSV files using Pandas read_csv command to dataframes
   * Opening and saving the zipped SQLite database tables using xxxx
   * Reviewing the contents of each database to identify relevant financial metrics, such as budget and sales
   * Reviewing the contents of each database to identify other potentially relevant metrics, such as genre, release dates, run-times, directors/cast
   * Selecting the specific databases for our analysis 
   * Understanding the unique IDs or other fields (e.g. movie title) within each database and other potential fields for performing merges / joins 

As a result of our exploratory data analysis, we decided to select and begin cleansing the following databases:
   * The Numbers: includes production budget, domestic and worldwide sales, and release date
   * IMDB - Movie Basics: includes unique movie id, original title, start year (release), runtime minutes, and genres
   * IMDB - Ratings: includes unique movie id, average rating and number of votes
    
Similarly, we decided to exclude the other databases for such reasons including but not limited to:
   * BOM had some financial measures, but no production budget data and had significantly fewer records in total than The Numbers
   * Rotten Tomatoes database did not have movie titles, only had 1,560 records, and genres seemed a little more nuanced (e.g. Science Fiction and Fantasy or Mystery and Suspense) Although some of the other information did seem potentially useful, we felt that not having a movie title could prove difficult when comparing to other databases and felt better information was available in databases identified above.
   * Due to time constraints and a firm deadline, we wanted to focus on identifying data that would help us respond to the business case in an efficient and effective manner
 

After identifying the pertinent databases and fields, we performed data cleansing, conversion and analysis. These include the following:
   *The Numbers
       - Dropping the ID field, as it went from 1 - 100 and would loop again
       - Removing commas and dollar signs, and converting budget, domestic and worldwide sales from string to integer type
       - Converting release date from string to datetime format
       - Adding calculated columns including Net Income (Worldwide gross minus production budget), Net Income Ratio (Net Income divided by worldwide gross), and ROI (Net Income divided by production budget)
       - Added a column for release year based on the release date field
 
   *IMDB Movie Basics
       - Drop records that have a non-null value using .dropna()
       - Remove duplicate entries by first sorting the dataframe on runtime minutes (highest to smalles) and then removing duplicates based on original title and release year
      
    *IMDB Ratings - no cleansing was necessary on this dataframe
     
We then performed a left merge between the cleansed IMDB Movie Basics database and the IMDB Ratings database on the movie id field. After merging the IMDB tables, we then performed an inner merge between the merged IMDB table and the cleansed The Numbers database ('TN_clean') on two columns - movie title and release year.

After analyzing the makeup of the merged Movies_DF dataframe, we further reduced the dataset by applying the following filters:
   - Movies with a production budget of over $10,000,000. We believe Microsoft will want to focus in on generally bigger budget films, and this would remove independent films and any movies that had "0" as the production budget (i.e. incomplete).
   - Movies with domestic sales over $0. We saw that some of the movies were international with $0 as domestic, and therefore wanted to remove these from our analysis. Microsoft will presumably want to have a local box office release in english as its first box office film.
   - Movies release after 2012. We felt that we should focus our analysis on the most recent 10 year period.
        
        
We then analyzed the resulting dataset for trends and relationships to profitability metrics with genres, the month of release, and ratings.

Our analysis resulted in the following visualizations and underlying observations:

   1. IMDB Ratings vs. Profitability ![image](/Images/Net Income vs Rating - Scatter.png)
    






   2. Genres vs. Profitability ![image](https://github.com/alecmills/phase-1-GroupProject/blob/master/Images/Genre%20-%20Bar.png)








   3. Release Month vs. Profitability ![image](/Images/NI v Month - Bar.png)









# 4. Recommendations / Conclusion


Based on our data analysis and the visualizations above, our 3 recommendations are as follows:

   1. Sci-Fi / Action-Adventure Movie - June/July Release
       - Microsoft should produce a big, action-packed sci-fi / action-adventure movie on existing IP. We think "Gears of War" would be a great first movie. They could consider making it slightly horror, which also does well overall.
        - This would also allow Microsoft to feature one of its own, and very successful, IP products.
        - The movie should be release in or around June or July (US big summer hit). These are when many of the big Marvel, DC, and Star Wars movies are released. You may want to stay away from holiday weekends, so as not to compete with those established franchiises.
        
    
    
   2. Animated / Family - December release
        - Microsoft should produce a family-friendly animated movie, that will further expand their viewership to kids and others who are not interested in the "Gears of War" franchise.
        - This movie should be released in December, when families are together for the holidays or consider mid-December to avoid competitor releases.



   3. Comedy (Possibly Romantic) - November release
        - Finally, Microsoft should invest in a Comedy, potentially a Rom-Com.
        - This would again, expand their following and possibly obtain new viewers (more females, couples, etc.).
        - This movie should be released in November, which is a very successful month in terms of ROI and Net Income.


