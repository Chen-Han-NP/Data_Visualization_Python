# Data Visualization Using Python 

## About
Imagine that you are part of the market research team for Fitness Trainer Pte Ltd, a retail business specializing in the sales of stationary bike. The team has collected data on individuals who purchased a stationary bike at Fitness Trainer retail stores for the past three months. The data is stored in the Fitness Trainer Series.csv file. Through data preparation, exploration and visualisation, the market research team decides to investigate whether there are differences across the models with respect to customer characteristics. 

The data consists of the following variables: 
1.	Product: Model of treadmill purchased (FT100, FT400, or FT700); 
2.	Branch: Branch location where purchase is made (Woodlands, Tiong Bahru, Tampines, Jurong);
3.	Gender: Gender of customer (Male or Female);
4.	Age: Age of customer in years (integer values);
5.	Education: Number of years of education customer had completed (integer values);
6.	MaritalStatus: Marital status of customer (Single or Partnered);
7.	Usage: Average number of times the customer plans to use the treadmill each week (integer values);
8.	Fitness: Customer’s self-rated fitness on a 1-to-5 scale (1: very unfit; 5: very fit); 
9.	Income: Customer’s annual household income (integer values); 
10.	Miles: Average number of miles the customer expects to walk/run each week (integer values).
![image](https://user-images.githubusercontent.com/73086331/144265184-a341b04a-202a-4c8e-893e-5a3d0d42f60e.png)



## Data Preparation
-	State of data
The initial state of data is not cleaned. There are total of 183 rows of data, other than Product and Branch, all other columns contain more than missing values. 
For column MaritalStatus, there are few irregular values like “S” and “P”, which supposed to be “Single” and “Partnered”. Thus, a substantial data cleanup is definitely needed to fill up all missing values and make sure data in MaritalStatus is regular and consistent. 

-	Data cleansing
1.  First by defining a list of possible missing values (e.g. “na”). So that when reading the data, it will check and replace the missing values with NULL. 
missing_values = ["n/a", "na", "N.A.", "--"]
df = pd.read_csv("Fitness Trainer Series _ April 2021.csv", na_values = missing_values)

RangeIndex: 183 entries, 0 to 182
Data columns (total 10 columns):
 #   Column         Non-Null Count  Dtype  
---  ------         --------------  -----  
 0   Product        183 non-null    object 
 1   Branch         183 non-null    object 
 2   Age            174 non-null    float64
 3   Gender         180 non-null    object 
 4   Education      180 non-null    float64
 5   MaritalStatus  180 non-null    object 
 6   Usage          172 non-null    float64
 7   Fitness        180 non-null    float64
 8   Income         180 non-null    float64
 9   Miles          180 non-null    float64
dtypes: float64(6), object(4)

2. Check which are the columns contains NULL values.
df.isnull().any()
Product          False
Branch           False
Age               True
Gender            True
Education         True
MaritalStatus     True
Usage             True
Fitness           True
Income            True
Miles             True

3. Next, fill in the NULL values in Age, Education, Usage, Fitness, Income and Miles with the median of all the values of that column.
And convert the data type to int instead of float by default.
df['Age'].fillna(df['Age'].median(),inplace = True)
df["Age"] = df["Age"].astype(int) 

df['Education'].fillna(df['Education'].median(),inplace = True)
df["Education"] = df["Education"].astype(int)

df['Usage'].fillna(df['Usage'].median(),inplace = True)
df["Usage"] = df["Usage"].astype(int)

df['Fitness'].fillna(df['Fitness'].median(),inplace = True)
df["Fitness"] = df["Fitness"].astype(int)

df['Income'].fillna(df['Income'].median(),inplace = True)
df["Income"] = df["Income"].astype(int)

df['Miles'].fillna(df['Miles'].median(),inplace = True)
df["Miles"] = df["Miles"].astype(int)

4. Next, handling irregular values for MaritalStatus, convert all “S” and “P” into “Single” and “Partner”.
df["MaritalStatus"] = df["MaritalStatus"].apply(lambda x: "Single" if x == "S" else x)
df["MaritalStatus"] = df["MaritalStatus"].apply(lambda x: "Partnered" if x == "P" else x)

5. Lastly, I realized that there are 3 missing values in Gender and MaritalStatus, so I made a decision to drop these three rows, because in these three rows, only Product and Branch columns are filled with value, and the rest are NA values, which does not help in the data visualization later. 
df = df.dropna(axis='rows')




Int64Index: 180 entries, 0 to 182
Data columns (total 10 columns):
 #   Column         Non-Null Count  Dtype 
---  ------         --------------  ----- 
 0   Product        180 non-null    object
 1   Branch         180 non-null    object
 2   Age            180 non-null    int32 
 3   Gender         180 non-null    object
 4   Education      180 non-null    int32 
 5   MaritalStatus  180 non-null    object
 6   Usage          180 non-null    int32 
 7   Fitness        180 non-null    int32 
 8   Income         180 non-null    int32 
 9   Miles          180 non-null    int32 
dtypes: int32(6), object(4)

![image](https://user-images.githubusercontent.com/73086331/144264806-a99d5546-474d-4689-808f-d77d1b9e2d7c.png)

## DashBoards
![image](https://user-images.githubusercontent.com/73086331/144264902-4c08bc94-eb4f-4199-8ceb-27048f80d4e9.png)

![image](https://user-images.githubusercontent.com/73086331/144264922-973dfdc8-67e4-4861-966e-02102fec6cf4.png)

![image](https://user-images.githubusercontent.com/73086331/144264942-d27a9ee5-6e00-4ee3-9cd6-e148694f3b74.png)

 
