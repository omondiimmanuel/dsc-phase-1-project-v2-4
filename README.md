# FINAL PRJECT SUBMISSION DETAILS
 Student name: OMONDI IMMANUEL OCHIENG 
 Student pace: part time 
 Scheduled project review date/time: 16/04/2023
 Instructor name: Noah kandie  
# TITLE: ANALYSIS TO FIND OUT POTENTIAL MOVIES FOR MICROSOFT NEWS STUDIO. 
 BUSINESS UNDERSTANDING
Microsoft had been observing how major companies had been creating movie content and decided to come up with their own movie studio. To do this however, they required an in-depth analysis of which movies had been performing well in the box office. This notebook will bring all the data sources together on movies for further analysis. 
# DATA UNDERSTANDING
 In order for there to be accurate, easier and proper data analysis, for this project i will make use of database files and some csv files stored on my local computer. My reason for using csv and database file is that they are easier to read and open using inbuilt python libraries. They are also not as cumbersome as json files.
# DATA SOURCES: 
bom.movie_gross.csv.gz
rt.movie_info.tsv.gz
rt.reviews.tsv.gz 
tmdb.movies.csv.gz 
tn.movie_budgets.csv.gz 
# DATA PREPARATION 
The steps i would follow during data gathering and preparation are as follows:
   1) importing of necessary libraries in order to read the data files. 
     the libraries i will be using are pandas and  matplotlib 
   3) python import pandas as pd 
     importing of pandas will enable me read directly from the csv files using pandas read csv files function.
   5) import matplotlib.pyplot as plt
   6) Set %matplotlib inline 
     i also include matplotlib inline to enable inline plotting on the notebook
   8) import style import warnings so as to get rid of any warnings  
   9) importing of matplotlib will aid in illustrating of my data findings. Matplotlib comes with an attribute called pyplot for easier plotting. 
   10) The next step of my data preparation process would be to open and read the necessary files and assign them to variables.
   11)   The first file of interest is (imdb.movies.csv.gz)
       We open it using the code: (tmdb= pd.read_csv('tmdb.movies.csv.gz') 
        tmdb.head(18)
       # This code works by reading files using the pandas attribute read_csv to access the information 
       # tmdb.head() function then displays the first 8 rows of the dataset.
       
 # Data analysis   
 Some of the movies encountered in the first data set:
1)	Harry Potter and the Deathly Hallows, Date:	2010-11-19	
2)	How to Train Your Dragon, date:2010-03-26	
3)	Iron Man , date:	2010-05-07	
4)	Toy Story	, date:	1995-11-22	
5)	[28, 878, 12]	27205	en	Inception	27.920	2010-07-16	Inception	8.3
6)	Percy Jackson & the Olympians: The Lightning T

  tmdb.info() 
 # the code gives us a general overview of the structure of the dataset. 
 # It is a pandasdataframe with 9 columns by 26517 rows 
 
  tmdb.columns
getting all columns of the dataset
  
tmdb.tail()
 This command gives back the last 5 rows of the dataset
 From there we  can now see the dataset has 26516 not 26517 rows  
 
# data cleaning 
 The next step is to perform some data cleaning. 
 The data_set has some null values in some columns and some rows are displaying unreal values
 
 tmdb.isnull()
  This code identifies null values in the dataset 
  tmdb.shape 
  checks the shape of the dataset, it has 26517 columns by 9 rows. 
  
  tmdb.dropna(how ='all').shape 
   This code checks for null values in all rows, drops them if null, since the shape remains the same, it proves that the dataset has no rows reading null
  
  tmdb.isnull().sum() 
  getting count of all null values
   
tmdb.shape
 this code shows there has been a reduction in number of rows showing they have been dropped.
 ``` (26381, 10) ``` 
 tmdb= tmdb.loc[tmdb['vote_count'] > 10000]  
  in this cell we selected the rows whose (VOTE_COUNT) was greater than 10,000  
  
tmdb.shape 
 judging by this output, we can see definitely some rows were dropped. ``` (72, 10) ```
 
tmdb= tmdb['vote_count'].sort_values(ascending= True) 
 This code sorts all the values in the VOTE_COUNT column in ascending order
 
tmdb.describe()
This code gives a return of mathematical operations performed in the dataset:
count 72.000000
mean 12347.972222 - mean
std 2605.554014 -standard deviation
min 10019.000000- minimum value
max 22186.000000 -maximum value

tmdb = tmdb.loc[tmdb['vote_average'] > 7.7 ]
 In this code we are selecting only the rows with a vote_average greater than 7.7
 
  #lets now drop the unwanted column 
tmdb.drop(tmdb.columns[[0]], axis= 1) 

 # lets now select the rows containing vote_count > 500 
 tmdb= tmdb.loc[tmdb['vote_count'] > 500 ] tmdb.head(8) 
 

 # Data analysis
 
Next i  will plot a histogram using vote_count columns and popularity columns to compare which movies are most popular.
The function for plotting histogram is illustrated as follows:

 plt.style.use('ggplot') plt.hist(votes, bins= 10, edgecolor= 'red', color= 'blue', rwidth= 0.9) plt.title('vote_Counts vs voters') plt.xlabel('vote_range') plt.ylabel('Vote_Counts') 
 ![image](https://user-images.githubusercontent.com/127987316/232332029-6b990a77-bbc6-4b7e-9a88-e06d0760d69a.png)

 i also plotted a third histogram
 tmdb.hist(bins= 10, edgecolor= 'red') 
 ![image](https://user-images.githubusercontent.com/127987316/232332062-ccd1d711-c1ad-4034-ac9f-5566030fc671.png)
 
 Next i plotted a scatterplot of the dataset
  tmdb.plot.scatter(x= 'vote_average', y= 'vote_count', s= 0.5) 
  ![image](https://user-images.githubusercontent.com/127987316/232332153-e926d665-bd71-4aff-baf8-914fd00999a0.png)
  
Lets now try comparing movie data of a second dataset
the dataset is tn.movie_budgets.csv.gz
lets proceed with opening it
  rt= pd.read_csv('tn.movie_budgets.csv.gz', index_col= 0)
 
  We open it using the pd.read function.
	

Lets now check the dataframe for general info
  #rt.info() 

 #rt.tail()
 getting last few rows of the dataset
 

 checking for null values
 
# rt.isnull().head()  ``` 

lets now get a mathematical count of the dataset
#rt.describe()  ``` 

#Data cleaning
 -lets start by converting the columns with dollar signs to integers

 #rt['production_budget']= rt['production_budget'].str.replace('$','').str.replace(',','') rt['production_budget']= pd.to_numeric(rt['production_budget']) 
 #rt['production_budget'].head()

 lets do the same for the remainig columns
 #rt['domestic_gross']= rt['domestic_gross'].str.replace('$','').str.replace(',','') rt['domestic_gross']= pd.to_numeric(rt['domestic_gross']) 
 #rt['domestic_gross'].head() 
 #rt['worldwide_gross']= rt['worldwide_gross'].str.replace('$','').str.replace(',','') rt['worldwide_gross']= pd.to_numeric(rt['worldwide_gross'])  

Lets get ing rid of rows where production budget is not equal to 0
# rt= rt[rt['production_budget'] != 0] 

getting rid of rows where domestic_gross is not eaqual to 0
 # rt= rt[rt['domestic_gross']!= 0 ]

getting rid of rows where worldwide gross is not equal to 0 
 # rt= rt[rt['worldwide_gross'] != 0]  

checking for null values
 #rt.isnull().value_counts

 Lets now select only rows where production_budget is greater than/equal to 500000
 
 # rt= rt[rt['production_budget'] >= 500000 ]
   We will do the same for domestic_gross and worldwide_gross columns.
 
 #rt= rt[rt['domestic_gross'] >= 500000] 
 #rt= rt[rt['worldwide_gross'] >= 500000] rt.head(8) 

 # data visualization 
 
 In these section we are going to visualize the data and performe various comparisons
 
 Lets start by gettin an overall plot
  #rt.plot() 
  ![image](https://user-images.githubusercontent.com/127987316/232333788-b25e4208-bb28-48d3-ba11-6aad379d3a4b.png)
  
Lets now generate subplots
  #rt.plot(title= 'comparison', subplots= True, figsize= (10,15)) 
  ![image](https://user-images.githubusercontent.com/127987316/232333854-cc335256-7353-4e99-9d81-bded6655c212.png)


 Lets now work with the last dataset 
 
   opening the file
  # bm= pd.read_csv('bom.movie_gross.csv.gz', index_col= 0) bm.head() 
  

Getting general info on the dataset
  #bm.info 
  
Checking the dataset columns
  #bm.columns
   
 getting last few rows of data
  #bm.tail()
  
Getting mathematical counts of the dataset
bm.describe()


# data cleaning  
 lets start by checking null values in the dataset 
 
#bm.isnull() 
 the output below shows we have some null values indicated by the string (true) ``` 

...	...	...	...	...
The Quake	False	False	True	False
Edward II (2018 re-release)	False	False	True	False
El Pacto	False	False	True	False
The Swan	False	False	True	False
An Actor Prepares	False	False	True	False```

lets count the number of these null values 

 #bm.isnull().sum()
 output:
 ```studio 5 domestic_gross 28 foreign_gross 1350 year 0 dtype: int64 ```
 
The output above shows we have null values in 3 columns

lets proceed to drop them 
 #bm= bm.dropna() 
 
#bm.isnull().sum()
Counting to check for null values

 lets now sort the dataframe by the column(years) 
  #bm = bm.sort_values('year') 
  
# data visualization 

Lets start by a basic plot
  #bm.plot() plt.title('comparison')  
  ![image](https://user-images.githubusercontent.com/127987316/232336906-a72d8ff0-2fd2-4042-8070-4c1f06edeb1d.png)
  
Lets proceed plotting a bar graph
 #plt.bar(years, domestic) plt.ylabel('domestic_gross') plt.xlabel('years') plt.title('domestic gross over the years')
 ![image](https://user-images.githubusercontent.com/127987316/232337163-4b7ea8e5-9cab-45ab-a481-4425712630e1.png)
 
 Lets proceed with plotting another bar graph.
 #plot.bar(title= 'Bm_Movie_Production', subplots= True, figsize= (21,20))
 ![image](https://user-images.githubusercontent.com/127987316/232337478-790efd52-330c-4a2e-9611-d9a1da6edf06.png)
 
Final bar graph plot
In this plot we selected the first 10 values of the dataset
 #bm.head(10).plot( 'studio', 'domestic_gross', kind='bar', color= 'g', figsize= (15,6)) plt.title(' movie by domestic_gross comparison') 
![image](https://user-images.githubusercontent.com/127987316/232337554-9ef34af6-0ef1-46c2-9352-9aa3882cdaad.png)

I also plotted a scatter plot
 #bm.head(10).plot( 'domestic_gross', 'foreign_gross', kind='scatter', color= 'r', figsize= (10,5)) plt.title(' domestic_gross by foreign_gross comparison') 
 ![image](https://user-images.githubusercontent.com/127987316/232337609-de320626-3dcb-4fa7-af7f-f9f3be9d93ef.png)



