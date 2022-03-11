# Instacart Data Analysis Project

![](https://user-images.githubusercontent.com/101165108/157609279-583fc458-1fe8-41aa-ae70-3fee6cb203a3.png)

## **Overview and Purpose**

Instacart is an online grocery store that operates through an app. Instacart already has very good sales, but they want to uncover more information about their sales patterns. My task is to perform an initial data and exploratory analysis of some of their data in order to derive insights and suggest strategies for better segmentation based on the provided criteria.

## **Context**

The Instacart stakeholders are most interested in the variety of customers in their database along with their purchasing behaviors. They assume they can't target everyone using the same methods, and they’re considering a targeted marketing strategy. They want to target different customers with applicable marketing campaigns to see whether they have an effect on the sale of their products.

See the data dictionary [here](https://github.com/CBoyd424/Instacart_Python_Project/blob/main/Data%20Dictionary)

## **Objective**

The Instacart Vice President of Marketing and Senior Vice President of Sales have asked a series of business questions and they expect data-driven answers that they can use for their upcoming marketing and sales strategies.

Here are the key questions they&#39;d like to answer:

  - The sales team needs to know what the busiest days of the week and hours of the day are (i.e., the days and times with the most orders) in order to schedule ads at times when there are fewer orders.
  - They also want to know whether there are particular times of the day when people spend the most money, as this might inform the type of products they advertise at these times.
  - Instacart has a lot of products with different price tags. Marketing and sales want to use
simpler price range groupings to help direct their efforts.
  - Are there certain types of products that are more popular than others? The marketing
and sales teams want to know which departments have the highest frequency of product
orders.
  - The marketing and sales teams are particularly interested in the different types of
customers in their system and how their ordering behaviors differ. For example:
       * What’s the distribution among users in regards to their brand loyalty (i.e., how
often do they return to Instacart)?
       * Are there differences in ordering habits based on a customer’s loyalty status?
       * Are there differences in ordering habits based on a customer’s region?
       * Is there a connection between age and family status in terms of ordering habits?
       * What different classifications does the demographic information suggest? Age? Income? Certain types of goods? Family status?
       * What differences can you find in ordering habits of different customer profiles? Consider the price of orders, the frequency of orders, the products customers are ordering, and anything else you can think of.

## **Tools and Skills**

![](https://user-images.githubusercontent.com/101165108/157611999-2a78835e-5a94-428c-8d19-34583dc132ec.png)
### **Python:**   Anaconda Data Analysis and Visualizations Following Code Etiquette

  - NumPy, pandas, os, Matplotlib, and Seaborn libraries

  - Data wrangling and subsetting

  - Data consistency checks

  - Crosstabs

  - Combining/merging multiple dataframes

  - Deriving new variables (columns, using for-loops

  - Grouping and aggregating data, creating and analyzing flags

  - Create histograms, bar charts, line charts, scatterplots for different variables and relationships between variables

  - Exporting results to .pkl files and .csv and crosstabs into Microsoft Excel

![](https://user-images.githubusercontent.com/101165108/157404857-78432359-3535-46e6-8c46-4bc01e31acde.png) 
### **Tableau:**  Further Visualization of Results Following Visual Design Standards

  - Spatial analysis using point maps, heat maps, choropleth maps, graduated symbol maps, and combination maps

  - Textual analysis using word clouds and packed bubble charts

  - Scatterplots and bubble charts

  - Statistical visualizations such as histograms and boxplots

  - Composition and comparison charts such as treemaps and pie charts

  - Frequencies and distributions

  - Temporal charts such as line charts, bar and column charts, area charts

  - Forecasting using linear extrapolation, averaging, and exponential smoothing

  - Create dashboards and a storyboard for presentation purposes.

## **Project Steps**

Note that my scripts folder contains scripts with numeric prefixes ranging from 4.2 to 4.10. This corresponds to order of the exercises and tasks I completed to learn skills and work on the project. Below, I only detail the script writing that is pertinent to the project--skill building aside.

First, I imported the data into Jupyter notebook as a pandas dataframe. Then, I conducted exploratory analyses of the data. This helped me gain a better understanding of the data, which informed future steps in the analysis. After this step, and all others, I exported the dataframes to .pkl files. This formed a version history of the data as I made manipulations.

Next, I carried out data wrangling steps, which included creating a data dictionary, dropping irrelevant columns, renaming nondescriptive columns, and changing data types where necessary (e.g.: I changed user_id from integer to string). This streamlined the dataframes and made the data more manageable.

With the desired data in hand, I performed consistency checks. This included finding and addressing missing values, duplicates, and columns with mixed-type data. This step was necessary to ensure an accurate analysis moving forward. One difficulty I faced here occured when I had over 200,000 null values in the "days_since_prior_order" variable. I made a crosstab of that column and the "order_number" variable, and I found that all of the observations with a "order_number" of "1" that had a null value in the "days_since_prior_order" column. Then, I confidently decided to make no change to the null values in that column.

Once I had wrangled and cleaned the data, it was time to combine/merge them. It was important to wrangle and clean first, as this reduced the size of the final dataframe and increased the likelihood of fully-matched combinations, respectively. The data sets were designed with combination in mind; there were primary and foreign keys present. So, I was well equipped to merge the dataframes. I included an indicator to check for a full match, and a value count of the indicator showed that all observations of each merged dataframe contained data from 'both' dataframes. There were no issues with this step. Nevertheless, it was important to create a single dataframe for the succeeding analyses.

![](https://user-images.githubusercontent.com/101165108/157616310-24039786-b08f-426b-acce-61ec98b5a4dd.png)

Creating flag columns for user profiles constituted most of the work before generating visualizations. The region column was based off of the observation's state column. The max_order column grouped the dataframe by "user_id" and found the user's max "order_number" (i.e.: this was the number of orders the user had placed). Then, I created a subset of the dataframe that only contained active users, excluding users with less than 5 orders. With this subset, I created several other flag columns: an income flag, which categorized users by their income quartile (relative to other users); an age flag, with young in Q1, middle-aged in Q2 and Q3, and senior in Q4; a dependents flag, classifying users as a parent or non-parent; and a shopping habits flag. Creating the shopping habits flag required several intermediate steps, culminating in a column that gave each user a ratio of food purchases to non-food purchases. I used this ratio, as well as a check for null values in the food purchase and non-food purchase columns, to classify users' shopping habits. Addressing the null values was the most difficult part of user profiling. I was able to use the null values to my advantage, though, by using them to classify users as 'Food only' or 'Non-food only'.

![](https://user-images.githubusercontent.com/101165108/157617036-43cf910d-1b87-447e-bcd7-1e9a579069d9.png)

With all of the separate user flag columns in place, I used a list comprehension method to effectively concatenate the income, age, dependent, and shopping habits column values for each observation, yielding a profile for each user. Finding a method that could quickly handle the mass of data took experimentation with subsets, but I landed on a list comprehension after just one other method failed to function in a timely manner due to only having 16gb of RAM in my iMac.

Once I had the user profiles, it was time to leverage visualization tools to come up with recommendations for Instacart's requests. Several of the visualizations I could make in Jupyter, using Matplotlib and Seaborn. However, I chose to execute a few more steps in tableau, and then narrow down a few to use in my final report. Because there were 134 (4x3x2x6) profiles, a bar chart in python was inappropriate. To make a tree map, I implemented a similar method for a crosstab of the profiles and regions, with which I made a series of bar charts in Tableau.

![](https://user-images.githubusercontent.com/101165108/157617830-7381e21c-3a3f-4b86-8a9a-12d7c052ea97.png)

Finally, I rounded out the project with a formatted report in Excel, which contained the population flow of the data, my wrangling steps and consistency checks, details on each derived column, some of my visualizations, and my final recommendations. This was the final derivable to Instacart.

## **Conclusion**

I was able to answer all the questions that Instacart's Stakeholders requested. The most challenging aspect of the project was profiling the users, especially their shopping habits. With 24 (4 'income' by 3 'age' by 2 'dependents') profile combinations before including shopping habits, I attempted to limit the amount of possibilities for that column. However, with 6 shopping habit categories, I ended up with 134 profile combinations.

If I were to change anything, I would have expanded what was required in my final project, because I started to discover some other interesting stories from my additional visualizations I made, sifting through the  final dataframe. Also, if this were a real project for a paying role, I would address the 200k null values with a data engineer on the team, my direct report, and anyone else involved. 

View my final Excel report [here](https://coach-courses-us.s3.amazonaws.com/exercises/1054/44753/2ce7ad8426ccf76531020d2587128f01/Data_Imm_3.10_PPT_Cboyd_PDF.pdf)
