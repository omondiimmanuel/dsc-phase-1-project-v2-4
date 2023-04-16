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
 #Shows all the columns of the dataset.
  Index(['Unnamed: 0', 'genre_ids', 'id', 'original_language', 'original_title', 'popularity', 'release_date', 'title', 'vote_average', 'vote_count'], dtype='object') 
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
  tmdb.dropna(how= 'any').shape
    The two codes run above show that the dataset has no null values since the shape of the dataframe hasnt changed. 
  tmdb.isnull().sum() 
    Here we sum all the total values in each row, the output diplayed below further shows there no null values. 
    ``` Unnamed: 0 0 genre_ids 0 id 0 original_language 0 original_title 0 popularity 0 release_date 0 title 0 vote_average 0 vote_count 0 dtype: int64 ``` tmdb= tmdb[tmdb['vote_average'] != 0.0 ] tmdb.head(10)
    # In this code we dropped rows where ('vote_average')one of the columns, was equal to 0 to get rid of empty votes 
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
tmdb= pd.read_csv('tmdb.movies.csv.gz', index_col= 0) 
  Here we are just getting rid of unwanted columns

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
here is a sample of the movies found:
			
1)dec 18, 2009	Avatar	
2)May 20, 2011	Pirates of the Caribbean: On Stranger Tides	
3)un 7, 2019	Dark Phoenix	
4)May 1, 2015	Avengers: Age of Ultron
5	Dec 15, 2017	Star Wars Ep. VIII: The Last Jedi	

Lets now check the dataframe for general info
  #rt.info() 
 Int64Index: 5782 entries, 1 to 82 Data columns (total 5 columns):
 Column Non-Null Count Dtype --- ------ -------------- ----- 0 release_date 5782 non-null object 1 movie 5782 non-null object 2 production_budget 5782 non-null object 3 domestic_gross 5782 non-null object 4 worldwide_gross 5782 non-null object dtypes: object(5) memory usage: 271.0+ KB 
 Getting the columns of the dataset
 #rt.columns #getting the columns from the dataset 
   Index(['release_date', 'movie', 'production_budget', 'domestic_gross', 'worldwide_gross'], dtype='object') 
  Getting last few rows of dataset
 #rt.tail() # checking last few columns of the dataset 
	 this is a sample of the output:
0)id					
!)78	Dec 31, 2018	Red 11	$7,000	$0	$0
2)79	Apr 2, 1999	Following	$6,000	$48,482	$240,495
3)80	Jul 13, 2005	Return to the Land of Wonders	$5,000	$1,338	$1,338
4)81	Sep 29, 2015	A Plague So Pleasant	$1,400	$0	$0
5)82	Aug 5, 2005	My Date With Drew	$1,100	$181,041	$181,041
 checking for null values
# rt.isnull().head()  ``` 
	release_date	movie	production_budget	domestic_gross	worldwide_gross
id					
1	False	False	False	False	False
2	False	False	False	False	False
3	False	False	False	False	False
4	False	False	False	False	False
5	False	False	False	False	False ```
Null values are generally denoted by the output false
lets now get a mathematical count of the dataset
#rt.describe()  ``` 
	release_date	movie	production_budget	domestic_gross	worldwide_gross
count	5782	5782	5782	5782	5782
unique	2418	5698	509	5164	5356
top	Dec 31, 2014	Halloween	$20,000,000	$0	$0
freq	24	3	231	548	367```
#Data cleaning
lets start by converting the columns with dollar signs to integers
 #rt['production_budget']= rt['production_budget'].str.replace('$','').str.replace(',','') rt['production_budget']= pd.to_numeric(rt['production_budget'])  #rt['production_budget'].head()
 From this code we can see column(production_budget) does not have dollar signs``` id 1 425000000 2 410600000 3 350000000 4 330600000 5 317000000 Name: production_budget, dtype: int64 ```
 lets do the same for the remainig columns
 #rt['domestic_gross']= rt['domestic_gross'].str.replace('$','').str.replace(',','') rt['domestic_gross']= pd.to_numeric(rt['domestic_gross']) 
 #rt['domestic_gross'].head() 
 #rt['worldwide_gross']= rt['worldwide_gross'].str.replace('$','').str.replace(',','') rt['worldwide_gross']= pd.to_numeric(rt['worldwide_gross'])  

Lets get ing rid of rows where production budget is not equal to 0
# rt= rt[rt['production_budget'] != 0] 
#rt.head() 
output:
	release_date	movie	production_budget	domestic_gross	worldwide_gross
id					
1	Dec 18, 2009	Avatar	425000000	760507625	2776345279
2	May 20, 2011	Pirates of the Caribbean: On Stranger Tides	410600000	241063875	1045663875
3	Jun 7, 2019	Dark Phoenix	350000000	42762350	149762350
4	May 1, 2015	Avengers: Age of Ultron	330600000	459005868	1403013963
5	Dec 15, 2017	Star Wars Ep. VIII: The Last Jedi	317000000	620181382	1316721747
getting rid of rows where domestic_gross is not eaqual to 0
 # rt= rt[rt['domestic_gross']!= 0 ]
 output:
	release_date	movie	production_budget	domestic_gross	worldwide_gross
id					
1	Dec 18, 2009	Avatar	425000000	760507625	2776345279
2	May 20, 2011	Pirates of the Caribbean: On Stranger Tides	410600000	241063875	1045663875
3	Jun 7, 2019	Dark Phoenix	350000000	42762350	149762350
4	May 1, 2015	Avengers: Age of Ultron	330600000	459005868	1403013963
5	Dec 15, 2017	Star Wars Ep. VIII: The Last Jedi	317000000	620181382	1316721747

getting rid of rows where worldwide gross is not equal to 0 
 # rt= rt[rt['worldwide_gross'] != 0]  
 output:
	release_date	movie	production_budget	domestic_gross	worldwide_gross
id					
1	Dec 18, 2009	Avatar	425000000	760507625	2776345279
2	May 20, 2011	Pirates of the Caribbean: On Stranger Tides	410600000	241063875	1045663875
3	Jun 7, 2019	Dark Phoenix	350000000	42762350	149762350
4	May 1, 2015	Avengers: Age of Ultron	330600000	459005868	1403013963
5	Dec 15, 2017	Star Wars Ep. VIII: The Last Jedi	317000000	620181382	1316721747

checking for null values
 #rt.isnull().value_counts

 Lets now select only rows where production_budget is greater than/equal to 500000
 # rt= rt[rt['production_budget'] >= 500000 ]
   We will do the same for domestic_gross and worldwide_gross columns.
   output: ``` 
	release_date	movie	production_budget	domestic_gross	worldwide_gross
id					
1	Dec 18, 2009	Avatar	425000000	760507625	2776345279
1	Jun 13, 1962	Lolita	2000000	9250000	9250000
1	Jul 16, 1999	Lake Placid	27000000	31770413	31770413
1	Sep 19, 1990	Goodfellas	25000000	46743809	46777347
1	Feb 7, 1974	Blazing Saddles	2600000	119500000	119500000
...	...	...	...	...	...
100	Dec 18, 2009	Nine	80000000	19676965	53508858
100	Oct 19, 2012	Alex Cross	35000000	25888412	35426759
100	Apr 8, 2016	Hardcore Henry	2000000	9252038	17187434
100	Dec 1, 2017	The Disaster Artist	10000000	21120616	28717667
100	Oct 21, 2005	The Work and the Glory: American Zion	6500000	2025032	2025032
5041 rows Ã— 5 columns```
  rt= rt[rt['domestic_gross'] >= 500000] 
  
 rt= rt[rt['worldwide_gross'] >= 500000] rt.head(8) 

 # data visualization 
 in these section we are going to visualize the data and performe various comparisons
 Lets start by gettin an overall plot
  #rt.plot() 
  ![image](https://user-images.githubusercontent.com/127987316/232333788-b25e4208-bb28-48d3-ba11-6aad379d3a4b.png)
Lets now generate subplots
  #rt.plot(title= 'comparison', subplots= True, figsize= (10,15)) 
  ![image](https://user-images.githubusercontent.com/127987316/232333854-cc335256-7353-4e99-9d81-bded6655c212.png)


 Lets now work with the last dataset 
   opening the file
  # bm= pd.read_csv('bom.movie_gross.csv.gz', index_col= 0) bm.head() #opening the dataset
  
 The sample of movies gotten were as follows:
1)Toy Story 3	BV	415000000.0	652000000	2010
2)Alice in Wonderland (2010)	BV	334200000.0	691300000	2010
3)Harry Potter and the Deathly Hallows Part 1	WB	296000000.0	664300000	2010
4)Inception	WB	292600000.0	535700000	2010
5)Shrek Forever After	P/DW	238700000.0	513900000	2010

Getting general info on the dataset
  #bm.info 
Checking the dataset columns
  #bm.columns
  output: Index(['studio', 'domestic_gross', 'foreign_gross', 'year'], dtype='object') 
  
 getting last few rows of data
  #bm.tail()
  
Getting mathematical counts of the dataset
bm.describe()
Output:```
	domestic_gross	year
count	3.359000e+03	3387.000000- overall count
mean	2.874585e+07	2013.958075- mean
std	6.698250e+07	2.478141- standard deviation
min	1.000000e+02	2010.000000 - minimum value
25%	1.200000e+05	2012.000000- lower quartile
50%	1.400000e+06	2014.000000- median
75%	2.790000e+07	2016.000000- upper quartile
max	9.367000e+08	2018.000000 -maximum value```
# data cleaning  
 lets start by checking null values in the dataset 
#bm.isnull() 
 the output below shows we have some null values indicated by the string (true) ``` 
	studio	domestic_gross	foreign_gross	year
title				
Toy Story 3	False	False	False	False
Alice in Wonderland (2010)	False	False	False	False
Harry Potter and the Deathly Hallows Part 1	False	False	False	False
Inception	False	False	False	False
Shrek Forever After	False	False	False	False
...	...	...	...	...
The Quake	False	False	True	False
Edward II (2018 re-release)	False	False	True	False
El Pacto	False	False	True	False
The Swan	False	False	True	False
An Actor Prepares	False	False	True	False
3387 rows Ã— 4 columns```
lets count the number of these null values 
 #bm.isnull().sum()
 output:``` studio 5 domestic_gross 28 foreign_gross 1350 year 0 dtype: int64 ```
The output above shows we have null values in 3 columns
lets proceed to drop them 
 #bm= bm.dropna() 
bm.isnull().sum()
Counting to check for null values
output:``` studio 0 domestic_gross 0 foreign_gross 0 year 0 dtype: int64 ```
 From the output above we no longer have null values ``` ```
 lets now sort the dataframe by the column(years) 
  #bm = bm.sort_values('year') 
# data visualization 
Lets start by a basic plot
  #bm.plot() plt.title('comparison') plt 
  ![image](https://user-images.githubusercontent.com/127987316/232336906-a72d8ff0-2fd2-4042-8070-4c1f06edeb1d.png)
Lets proceed plotting a bar graph
 #plt.bar(years, domestic) plt.ylabel('domestic_gross') plt.xlabel('years') plt.title('domestic gross over the years')
 ![image](https://user-images.githubusercontent.com/127987316/232337163-4b7ea8e5-9cab-45ab-a481-4425712630e1.png)
 
 Lets proceed with plotting another bar graph.
 #plot.bar(title= 'Bm_Movie_Production', subplots= True, figsize= (21,20))
 ![image](https://user-images.githubusercontent.com/127987316/232337478-790efd52-330c-4a2e-9611-d9a1da6edf06.png)
 
Final bar graph plot
In this plot we selected the first 10 values
 #bm.head(10).plot( 'studio', 'domestic_gross', kind='bar', color= 'g', figsize= (15,6)) plt.title(' movie by domestic_gross comparison') 
![image](https://user-images.githubusercontent.com/127987316/232337554-9ef34af6-0ef1-46c2-9352-9aa3882cdaad.png)

I also plotted a scatter plot
 #bm.head(10).plot( 'domestic_gross', 'foreign_gross', kind='scatter', color= 'r', figsize= (10,5)) plt.title(' domestic_gross by foreign_gross comparison') 
 ![image](https://user-images.githubusercontent.com/127987316/232337609-de320626-3dcb-4fa7-af7f-f9f3be9d93ef.png)



