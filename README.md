# Cryptocurrencies
The code for this analysis can be found here: [Clustering Crypto](https://github.com/mrma2318/Cryptocurrencies/blob/d532d76614f1ad7231250faa1d1d152de860a22a/Starter_Code/crypto_clustering.ipynb)
## Overview: For this analysis I will be preprocessing data for PCA, reducing data dimensions using PCA, clustering crytpocurriencies using K-means, and visualizing crytopcurrency results. 
### Purpose: The purpose of this analysis is to create a report that includes what cryptocurrencies are on the trading market and how they could be grouped to create a classification system for a new investment. 

## Analysis
### Preprocessing the Data for PCA
- First, I read the [cryto](https://github.com/mrma2318/Cryptocurrencies/blob/5208e4bc04c5a90edbac95c98ad3a0e9fc681767/Starter_Code/crypto_data.csv) dataset into a Pandas DataFrame, cryto_df. I only wanted to keep the cryptocurrencies that were being traded so I droped the "IsTrading" column and removed rows that had a least one null value. Then I filtered crypto_df DataFrame so that it only had rows where coins have been mined. 

- Next, I created a new DataFrame that holds only the cyrptocurrency names, and used the previous DataFrame, crypto_df, index as the index for the new DataFrame. Then I removed the coin name column from the crypto_df DataFrame since I wasn't going to use it on the clustering algorithm, Image 1.

#### Image 1: New Cyrpto DataFrame
![New Crypto DataFrame](https://github.com/mrma2318/Cryptocurrencies/blob/bda32fd8979a86909f1b9dd5410011b1213fc561/images/new_crypto_df.png)

- For the Algorithm and ProofType columns, I used the get_dummies method to create variables and stroe the resulting data in a new DataFrame, X. Then I used the StandardScaler fit_transform() function to standardize the features from the X DataFrame. 

### Reducing Data Dimensions Using PCA
- Now I can apply PCA to reduce the dimensions to three principle components. I created a new DataFrame, pcs_df, that included the following three columns, PCA1, PCA2, PCA3, and used the index from the crypto_df DataFrame, Image 2. 

#### Image 2: PCS DataFrame
![PCS DataFrame](https://github.com/mrma2318/Cryptocurrencies/blob/78b80ea9d1ec6290d4c77f13e38f221d61d82c77/images/pcs_df.png)

### Clustering Cryptocurrencies Using K-means
- Useing the pcs_df DataFrame, I created an elbow curve using the hvPlot function to find the best value for K, Image 3. Then, I used the pcs_df DataFrame to run the K-means algorithm to make predictions of the K clusters for the cryptocurrencies' data. 

#### Image 3: Elbow Curve
![Elbow Curve](https://github.com/mrma2318/Cryptocurrencies/blob/63d2951819593b5382cb4c990ac8467f72136548/images/elbow_curve.png)

- Next, I created another new DataFrame, clustered_df, by concatenating the crypto_df and pcs_df DataFrames on the same columns. Then, I added the coin name column, and added another new columns to the clustered_df DataFrame named class to hold the predicitions, Image 4. 

#### Image 4: Clustered DataFrame
![Clustered DataFrame](https://github.com/mrma2318/Cryptocurrencies/blob/9597f786febaf677488c07fe5ae00675cf5fd44f/images/clustered_df.png)

### Visualizing Cryptocurrencies Results
- I wanted to create a 3D scatter plot of the clustered_df DataFrame using the Plotly Express' scatter_3d() function, Image 5. I also added the coin name and algorithm columns to the hover name and hover data parameters so each data point shows the CoinName and Algorithm when you hover over a data point. 

#### Image 5: 3D Scatter Plot of Clustered DataFrame
![3D Scatter Plot](https://github.com/mrma2318/Cryptocurrencies/blob/0dba52875a447f15e9d89b7774af625ae8a937f9/images/3D.png)

- Then, I created a table with tradeable cryptocurrencies using the hvplot.table() function. Using the MinMaxScaler().fit_transform method, I scaled the TotalCoinSupply and TotalCoinsMined columns between the range of zero and one. Next, I created a new DataFrame, plot_df, using the clustered_df DataFrame index. I added the CoinName and Class columns from the clustered_df DataFrame to the plot_df DataFrame, Image 6: 

#### Image 6: Plot DataFrame
![Plot DataFrame](https://github.com/mrma2318/Cryptocurrencies/blob/c1c6270b64791b3d137b121595bb4e1a4e5ce1ef/images/plot_df.png)

- Lastly, I created an hvplot scatter plot where x="TotalCoinsMined", and y="TotalCoinSupply", by Class. I also had the CoinName appear when you hover over the data point, Image 7. 

### Image 7: plot_df hvplot Scatter Plot
![plot_df](https://github.com/mrma2318/Cryptocurrencies/blob/d532d76614f1ad7231250faa1d1d152de860a22a/images/plot_df_scatter.png)


