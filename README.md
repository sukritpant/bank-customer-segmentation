# Bank Customer Segmentation Data Exploration, Visualization and Hypothesis

The project analyzes the Bank Customer Segmentation data with more than 1 million datapoints collected between August and October 2016 that is available in Kaggle. The data was preprocessed and explored using various visualization tools along with statistical test for hypothesis testing. This project was performed as a part of Integrify Data Science and Machine Learning Project when I was part of the program. As there are multiple transactions and rows of data, there are a lot of information that can be extracted from the data and this was only a small portion that I used as the proof of concept for this particular dataset.

## About the Dataset

The dataset was taken from Kaggle <https://www.kaggle.com/datasets/shivamb/bank-customer-segmentation> as a CSV file and loaded into a Jupyter Notebook. The CSV file is larger than what is supported by Github so it might be truncated so for running the dataset, it would be better if you use the dataset that you can download from Kaggle from the given link. The following columns are available in the dataset: Since,

1. TransactionID: UniqueID for each transaction (Used as row index for dataset)
2. CustomerID: ID of an individual customer
3. CustomerDOB: Customers Date of birth as string converted to datetype (There are some unreasonable dates that are removed during preprocessing which will be discussed in the preprocessing section)
4. CustGender: Male and Female (There is one 'T' value which is removed during data cleaning)
5. CustLocation: City(Location) of the transaction Categorical
6. CustAccountBalance: Balance in customer account as float
7. TransactionDate: Transaction date as string converted to datetime format
8. TransactionTime: Time the transaction took place as integer converted to time
9. TransactionAmount: Amount spent by the customer as float

#### Additional Columns after Preprocessing
10. CustomerAge: Difference between the CustomerDOB and TransactionDate
11. DayOfWeek: Day of the week that the transaction took place

### Packages
Following packages were loaded for the analysis:
Packages loaded for these analysis are as follows but not all the packages have been utilized:
- pandas
- numpy
- seaborn
- matplotlib
- datetime
- time
- scipy
- sklearn
- plotly

### Data Preprocessing

#### Date Implementation
The date was in a DD/MM/YY format for CustomerDOB and TransactionDate so both were converted to datetime. However, the datetime package converted the data before 1973 to 20XX format so there were date such as 2072 and others which were after the transaction dates, therefore a datefixer function was created assuming the customer was at least 16 when the transaction was made so there are no dates showing 20XX as the CustomerDOB. There were also some dates which were 1/1/1800 which were considered improper and due to the large dataset all the transaction from these accounts were removed.

#### Time Implementation
The time ranges from 0 to 235959 in the TransactionTime columnand the dataset mentions that it is a UNIX timestamp but the problem with that is that 235959 means there are more than 86400 seconds in a day however, it made more sense that the value were 000000 to 235959 format which would mean that the time is stored as HHMMSS which made more sense. So for any value below 10000 they were considered as value before 1 AM, with this assumption, I filled the transaction time as string and made sure that there are at least 6 letters by filling it with zeros for any value shorter than six digits and converted to time format in HH:MM:SS formatting.

## Data Exploration
As there are some null values in few columns all these columns were dropped before performing the analysis in the discretion of the person working with the data. Some central and spread measures were extracted from the dataset to perform further analysis with the dataset with dataframe.describe() function for the numeric columns.

### Data Visualization
A correlation was checked among the numeric columns of the dataset. Also, as the dataset is quite large, an outlier analysis were performed on all of the numeric columns with box plot initially then the outliers were checked from the dataset with at least 10% of the data being oultiers for customer account balance and transaction amount.

Furthermore, the data were visualized to check for the location of the transaction and based on count and transaction amount after which further analysis were made to see if the transaction mean are different which showed some large transaction from outside the country the dataset belonged to showing that a lot of single large transactions are being performed abroad from India where the dataset is extracted. Also, some highest transacting customers were analyzed to see if there are large amount being transacted by few people which was also plotted into a graph.

Similarly, a transaction based of the day of the week was also visualized which helped show when the transaction were being made along with voilin plot for for the transaction amount based on the customer gender was created.

### Hypothesis Testing
With the completion of the data analysis, a hypothesis was necessary to be formed before which a normality test was performed for the data with Shapiro test. As the data was not normally distributed, an assumption was made before choosing the method that the data was normally distributed for hypothesis testing rather than using other test such as MannWhitneyU during the analysis. Through this a T-test was performed to understand if the mean transaction amount between the two genders are significant or not and this is plotted in a bar graph to visualize the information extracted from the hypothesis testing.

## Reflection
As this was an initial data analysis and exploration done on a new dataset, the visualization was performed to check for the various information that are available in the data. Even without the goal in view, there is a possibility to explore and visualize the various data and also a hypothesis can be crafted and tested in similar data. Similarly, plotly was used to see what are the possible ways to visualize the data. These can be very interersting depending on what we are performing with the dataset
