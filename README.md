# WQD7005 DATA MINING Alternative Assessment 1

The datasets used is name as:
A. Customer DataSets Part1.csv
B. Customer DataSets Part2.csv

## 1. Talend Open Studio for Data Integration
### 1.1 Dataset Import
Since there are 2 datasets, we will be using Talend Open Studio for Data Integration. Talend Open Studio for Data Integration is a popular choice for data preprocessing because it offers a wide range of features, including the ability to add data quality, big data integration, and processing resources.

There are 2 tFileInputDelimited nodes for each dataset. Both node settings are as below:
 
The header will be the first row and their Filed Separator is “,”.
After the datasets are imported.  tFileInputDelimited nodes will be set their schemas, below are the schema for both datasets. All is float except CUST_ID will be string

### 1.2	Dataset Join
Once the datasets are imported and their schemas been set, they both need to be joined. To join the datasets, connect the tFileInputDelimited to tMap_1 node. Since both datasets have CUST_ID in common, CUST_ID will be used for as the key to map both datasets.
Below are the settings of the mapping:
 
After mapping both datasets, we can set the outcome of the joined dataset be as the table below:

### 1.3 Dataset Produce
To produce the joined dataset, connect tMap_1 node to tOutputDelimited. What we want is the joined dataset to be exported as a single CSV file. Below are the settings of the node, the output will include their headers.

The separator is set to “,” as usual CSV file.

**The project file for Talend Open Studio for Data Integration is stored in DataPrep_0.1.zip**

## 2. Talend Data Preparation
### 2.1 Data Cleaning
To clean the data, we will use Talend Data Preparation. Talend Data Preparation is a great choice for data preprocessing because it offers a wide range of features, including the ability to quickly identify errors and apply rules that you can easily reuse and share, even across massive data sets. This is the result after importing the dataset:

Some columns have wrong data types assigned to them, some of them becomes Integer and 1 becomes a Geo_Coordinate. Hence why the colour below the column names is not green. Indicated some data produce errors. Below are the columns and their datatypes:

We can set them to correct datatypes, which is Decimal by clicking the columns such as below:
 
By correcting all datatypes, now we can see all colour turns into green. Below are current datatypes of the columns:
 
### 2.2 Missing Data
By clicking the columns one by one, we can see the value of missing data of the column, this is the result of CREDIT_LIMIT and MINIMUM_PAYMENTS:

We can see that there are 1 missing data in CREDIT_LIMIT and 313 misssing data in MINIMUM_PAYMENTS. However, we cannot replace CREDIT_LIMIT and MINIMUM_PAYMENTS with 0 or null. CREDIT_LIMIT is the limit of customer’s credit and MINIMUM_PAYMENTS is the minimum payment made by customer. This column will be imputed the in SAS Enterprise Miner.
Now the cleaned dataset can be exported to a CSV file.
 
**The output file of this out.csv**

## 3. SAS Enterprise Miner
#### 3.1. Data Import
Now the dataset is ready for prediction. The prediction will be done using SAS Enterprise Miner. SAS Enterprise Miner is a great choice for prediction because it offers a wide range of features, including the ability to generate models using SAS Rapid Predictive Modeler, which is an easy-to-use GUI that steps you through a workflow of data mining tasks. We can start by importing the dataset using File import node.
 
Above are the settings of the node. The Import File is the Customer Datasets file we exported after cleaning in Talend Data Preparation, the Maximum Row to Import will be set to 1000000 so all row will be imported, the Delimiter of this dataset is “,” so it will set to “,”. Since the file contains headers. Name Row will be “Yes”. The role of this dataset will be “Train” as it will be used for training the models.

### 3.2. Variables Settings
The roles of each attributes need to be decided. The roles of attributes define the purpose of each attribute in the dataset, which is essential for accurate prediction. By setting the roles of each attribute, we can ensure that the data is properly prepared for prediction and that the model is trained on the correct variables. 
The CUST_ID will be set to ID as it is the ID of the Customers. Thus, not really contribute for prediction. The target role will be assigned to Balance.
 
### 3.3. StatExplore
To measure how much data is missing, we can use StatExplore node. The StatExplore node in SAS Enterprise Miner is a multipurpose tool that can be used to examine variable distributions and statistics in your data sets. It generates summarization statistics and provides a wide range of features, including the ability to select variables for analysis, compute standard univariate distribution statistics, compute standard bivariate statistics by class target and class segment, and compute correlation statistics for interval variables by interval input and target.
We will connect File Import node to StatExplore and run it. By running the node, we can see the result.

From the result, we can see CREDIT_LIMIIT is missing 1 data while MINIMUM_PAYMENTS lost 313 data similar in Talend Data Preparation.

**The diagram of this SAS miner project is stored**