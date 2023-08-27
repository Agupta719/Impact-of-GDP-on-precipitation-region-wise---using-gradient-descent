# Impact-of-GDP-on-precipitation-region-wise---using-ML
This document states the steps undertaken to find out the optimum coefficient between the relationship of precipitation (dependent variable) and GDP (independent variable) for the year 2020.

The data was downloaded from World Bank. Please refer to the file titled ‘References.xlsx’ for more information on the data.

Variable	Description
GDP_df	GDP per capita, PPP (constant 2017 international $) (Country Wise)
precipitation_df	Average precipitation in depth (mm per year) (Country Wise)
region_wise_country_df	World countries and their associated regions for 2017

Jupyter Notebook Documentation

1.	Import the necessary libraries
a.	Pandas
b.	Matplotlib.pyplot
c.	Random
2.	Create functions for efficient coding
a.	Splitting the dataset into 2 parts – testing dataset and training dataset
b.	Splitting the list of tuples containing x and y coordinates into two lists of x coordinate and y coordinate
c.	Functions for performing linear regression using OLS estimator
i.	Finding beta0
ii.	Finding beta1
iii.	Finding the mean
d.	Functions for performing linear regression using gradient descent algorithm
i.	Calculating mean squared error
ii.	Finding partial derivative of beta0
iii.	Finding partial derivative of beta1
iv.	Finding the new value of beta0
v.	Finding the new value of beta1
vi.	Finding y_hat values for every value of x
3.	Import the necessary files
a.	GDP file
b.	Precipitation file
c.	Region-wise list of countries’ file
4.	Clean the GDP_df dataframe
a.	Created new column containing GDP values, all in numeric data type
b.	Removed the rows with NaN values. Presence of even a single NaN value in the GDP column, turned the coefficient value to be NaN for that particular region. 
c.	Removed redundant rows
d.	Rounded off the values to 2 decimal places to keep calculations simple
5.	Clean the precipitation_df dataframe
a.	Created new column containing precipitation values, all in numeric data type
b.	Removed the rows with NaN values. Presence of even a single NaN value in the GDP column, turned the coefficient value to be NaN for that particular region. 
c.	Removed redundant rows
6.	Clean region_wise_country_df dataframe
a.	Removed redundant columns like Year as the regions remained the same from 2017 till 2020.
b.	Renamed necessary variables
7.	Merge all dataframes
a.	Merged GDP and precipitation datagrams
b.	Merged the above dataframe with the region_wise_country_df dataframe and name it merged_df
c.	Dropped multiple columns with country names
d.	Dropped rows with NaN values
8.	For every region, these steps repeat:
a.	Create a subset of the merged_df dataframe grouped by a particular region
b.	From the dataframe extract, GDP and precipitation values and insert them in a list of tuples as x and y coordinates in the form of a dataset
c.	Split the above dataset in two parts – training dataset (containing 80% of the data points) and testing dataset (containing 20% of the data points)
d.	From the training dataset, create two lists containing x coordinate and y coordinate respectively 
e.	Initially use OLS estimator on the training dataset to find the optimum coefficient. This would later be used to validate the coefficient obtained from gradient descent.
i.	Find the y_hat values for every x using the functions defined above for OLS estimation
f.	Use gradient descent to find the optimum coefficient on the training dataset. 
i.	To find the y_hat value for every x, use ‘findYcoordinatesFromGradientDescent’ function. So, first define the configuration, i.e., the parameters required for this function. These parameters can be changed as per the user’s preference. 
ii.	alphaOfBeta0 and alphaOfBeta1 are the step sizes that are subtracted from the current beta0 and beta1 respectively to obtain new beta values. These new beta values are used to estimate the new mean squared error. This process keeps repeating for the number of maxIter, i.e., the maximum number of iterations, mentioned. Our goal is to minimize the mean squared error. These values can be changed to see how the graph is changing.
iii.	The final value of beta1 is the optimum coefficient for each region.
g.	Graphs are plotted to visualize the relationship
i.	The blue dots are the scattered training data points (GDP, precipitation) representing a country
ii.	The red line is the linear regression curve derived from OLS estimation. It is not visible as it is completely overlapped by the blue line. If one twerks the configuration of y_hat using gradient descent, and then run the maps, the red line will become visible. 
iii.	The blue line is the linear regression curve derived from gradient descent.
h.	From the testing dataset, create two lists containing x coordinate and y coordinate respectively 
i.	Using the above derived constant and slope from gradient descent algorithm, a linear curve is tried to fit the testing dataset.
j.	Graphs are plotted to visualize the relationship
i.	The blue dots are the scattered testing data points (GDP, precipitation) representing a country
ii.	The blue line is the linear regression curve is derived from gradient descent.
k.	Note: due to extremely small dataset, the linear curves are not accurate. 
l.	The below table displays the optimum coefficient for every region. 
i.	Note: Since the training and testing dataset are constructed by randomly choosing any datapoints, the coefficient can be slightly different every time the .ipynb file is run
ii.	Note: Since, North America has merely two datapoints, it is not possible to use gradient descent on this region to find the optimum coefficient. Hence, it’s value is N/A.

Region	Optimum coefficient
South Asia	0.0724559234491282
Europe and Central Asia	0.0073974166353089925
Middle East and North Africa	-0.0013061881793588633
Sub-Saharan Africa	0.037024338045527766
Latin America and Caribbean	0.0007320031556047729
East Asia and Pacific	-0.0032110215273598603
North America	N/A
