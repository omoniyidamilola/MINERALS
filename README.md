# MINERALS
IMA Database of Mineral Properties
# IMA Database of Mineral Properties

Minerals data by international mineralogical Association.

### Introduction

In this report, I investigated the IMA database of mineral properties. The dataset contains mineral names, unique formula(RRUFF and IMA) in plain text(f.e., Abellaite is NaPb2+2(CO2)2(OH) which means NaPb2+(CO3)2(OH), IMA numbers, RRUFF IDs, Chemistry elements, countries of locality, Structural Group and Age.



## Problem Statement

To Identify:

How many minerals were approved?

Which crystal system does the mineral have.

What is the oldest known Age?

The most abundant chemical elements.

Which country has the highest number of minerals.




### The following questions will be answered:


(a) What is the most abundant chemical elements?


(b) Regions where minerals are more common.


(c) The oldest known age.


(d) Properties of the minerals.


(e) Mineral Status.


The data was downloaded from Kaggle datasets:
 https://www.kaggle.com/datasets/lsind18/ima-database-of-mineral-properties/download?datasetVersionNumber=2

## Import Libraries

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns


#Load  the dataset
mineral = pd.read_csv('RRUFF_Export_20230608_052338.csv')

mineral

#preview the dataset
mineral.head()

mineral.tail()

 #.info() function is used to understand the data types, numbers of columns, number of rows and memory storage of the data.
mineral.info()

#Summary statistics of  the dataset
mineral.describe()

#Lets get the shape of the dataset.
mineral.shape

There are 14 columns (or features) in this dataset.

#List all columns names
mineral.columns

## Data Cleaning

Checking for null values, drop rows with null values..
mineral.isna()

#let count for the number of null values
mineral.isna().sum()

from the column, 7 columns has null values; IMA Number, RRUFF IDs, IMA Status, Status Notes, Crystal Systems, Space Groups, Oldest Known Age and Paragenetic Modes.

#Calculating mean value of Oldest Known Age(Ma)
x = mineral['Oldest Known Age (Ma)'].mean()
print(x)

#Filling the null value of Oldest Known Age(Ma)
mineral['Oldest Known Age (Ma)'].fillna(x, inplace=True)

mineral

Column that contained missing values in the dataset that are not necessary for the analysis such as the RRUFF IDs, IMA Number and Space Groups had to be removed, which significantly reduced the total columns used for the analysis.

#I deleted the columns that will not needed for the analysis:
mineral.drop('IMA Number', axis =1, inplace=True)

#Deleted unnecessary columns
mineral.drop('RRUFF IDs', axis =1, inplace=True)

#Deleted unnecessary columns
mineral.drop('Space Groups', axis=1, inplace=True)

mineral

#Dropping the row with null values, inplace=True is used so that the changes are saved without creating new object.
mineral.dropna(axis=0, inplace=True)


mineral

#Lets get the shape of the dataset after dropping and filling the null values.
mineral.shape

#Checking if there is duplicate values
mineral.duplicated()

#Let count for the number of duplicate values
mineral.duplicated().sum()

## Exploratory Data Analysis



Here, I analyzed and created visualizations so as to get insights of my data.

mineral.corr()

mineral['Mineral Name'].value_counts()

### Region Where Minerals Are Common

Country_of_Type_Locality_count= mineral['Country of Type Locality'].value_counts()
Country_of_Type_Locality_count

Locality = Country_of_Type_Locality_count[ :20]

Locality.plot(kind = 'barh', color='hotpink')

font1= {'family':'serif', 'color':'black', 'size':12}
font2= {'family':'serif', 'color':'red', 'size':15}


plt.title('Chart Showing The Top 20 Country of type Locality', fontdict=font1)
plt.xlabel('Count', fontdict=font2)
plt.ylabel('Country of type Locality', fontdict=font2)
plt.show()

From the above chart, Minerals are common in the USA, followed by Russia. Brazil, Norway, has low minerals

### Geological Processes(Oldest Known Age(Ma))

 mineral['Oldest Known Age (Ma)'].value_counts()

#find the top 10 OLdest Known Age(Ma)
mineral_count = mineral.sort_values('Oldest Known Age (Ma)')
top_10_earning = mineral_count[ :10]

#list of titles of top ten Oldest known Age(Ma)
top_rating= list(top_10_earning)

font1= {'family':'serif', 'color':'blue', 'size':12}
font2= {'family':'serif', 'color':'black', 'size':15}


#plot the histogram
plt.figure(figsize = (15, 8))
plt.hist(mineral['Oldest Known Age (Ma)'], histtype='bar', rwidth=0.5, color='purple')
plt.title( 'Chart Showing The Oldest Known Age(Ma)', fontdict = font1)
plt.xlabel('Oldest Known Age (Ma)', fontdict= font2)
plt.ylabel('Count', fontdict= font2)
plt.show()


mineral['Year First Published'].value_counts()

### Mineral Status

Total_IMA_Status = mineral['IMA Status'].value_counts()
Total_IMA_Status

3600 minerals were approved and 355 minerals were approved and renamed. Below is the graphical representation of the IMA Status of the minerals.

#find the top 10 IMA Status
mineral_count = mineral.sort_values('IMA Status')
top_10_earning = mineral_count[ :10]

#list of titles of top 10 highest IMA Status
top_rating= list(top_10_earning)

font1= {'family':'serif', 'color':'blue', 'size':12}
font2= {'family':'serif', 'color':'black', 'size':15}


sns.countplot(x = 'IMA Status',  data= mineral)
font1= {'family':'serif', 'color':'black', 'size':12}
font2= {'family':'serif', 'color':'red', 'size':15}

plt.xticks(rotation=75, color='black')
plt.title('Chart Showing IMA Status of the Mineral', fontdict=font1)
plt.xlabel('IMA Status', fontdict=font2)
plt.ylabel('Count', fontdict=font2)
plt.show()

### Mineral Classification (Abudance Chemical Elements)

Chemistry_Elements_count= mineral['Chemistry Elements'].value_counts()
Chemistry_Elements_count

First_15_Chemistry_Elements= Chemistry_Elements_count[ :15]

#plot bar chart
First_15_Chemistry_Elements.plot(kind = 'bar', color='yellow')

font1= {'family':'serif', 'color':'black', 'size':12}
font2= {'family':'serif', 'color':'red', 'size':15}

plt.xticks(rotation=75, color='black')
plt.title('Chart Showing the Highest Chemical Element', fontdict=font1)
plt.xlabel('Chemistry Element', fontdict=font2)
plt.ylabel('count', fontdict=font2)
plt.show()

From the above chart, FE P OH is the abundant chemical elements.

### Mineral Properties

Crystal_System_count=mineral['Crystal Systems'].value_counts()
Crystal_System_count

First_15_Crystal_System= Crystal_System_count[ :15]

#plot bar chart
First_15_Crystal_System.plot(kind = 'bar', color='green')

font1= {'family':'serif', 'color':'black', 'size':15}
font2= {'family':'serif', 'color':'red', 'size':15}

plt.xticks(rotation=75, color='black')
plt.title('Chart Showing Crystal System', fontdict=font1)
plt.xlabel('Crystal Systems', fontdict=font2)
plt.ylabel('Count', fontdict=font2)
plt.show()

Valence_Elements_count=mineral['Valence Elements'].value_counts()
Valence_Elements_count

First_15_Valence_Elements= Valence_Elements_count[ :15]

#plot a bar chart
First_15_Valence_Elements.plot(kind = 'bar', color='Magenta')

font1= {'family':'serif', 'color':'black', 'size':15}
font2= {'family':'serif', 'color':'red', 'size':15}

plt.xticks(rotation=75, color='black')
plt.title('Chart Showing The Valence Elements', fontdict=font1)
plt.xlabel('Valence Elements', fontdict=font2)
plt.ylabel('Count', fontdict=font2)
plt.show()

#Correlation between Year First Published and Oldest Known Age(Ma)
mineral.corr()


plt.figure(figsize=(10,5))
sns.heatmap(mineral.corr(), cmap="coolwarm", annot=True)

From our heatamap above, we can infer that there is a correlation with a value of 1 and -0.32 respectively.

## Conclusion


3600 minerals were approved.

USA is the region where minerals are common although USA has 814 minerals while Russia has 810 minerals. 

Fe P OH is the most abundant chemical elements with 23 minerals.

The minerals are mostly monoclinic, orthorhombic and hexagonal crystal systems. 1799 minerals were monoclinic crystal system, 1043 minerals were orthorhombic crystal and 1004 minerals are hexagonal crystal system.

The Oldest Known Age(Ma) is 1271.84.

There is a correlation between Year First Published and Oldest Known Age with a value of 1 and -0.32 respectively.

### Recommendation




Based on the analysis, USA is the region with high concentration of minerals, the company should focus more on the region.The company should prioritize exploring areas with high concentration.

Exploring areas with high concentration of mineral with unique properties such as the monoclinic crystal system or high valence elements like CA SI OH. 

By taking these factors into account, there is a likelihood of increase in finding new mineral deposits. 

