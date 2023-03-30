# Data Science Sales Prediction

## Analyzing Product Types at Different Stores to Increase Sales 

Rodrigo Arguello-Serrano

This first project will be a sales prediction for food items sold at various stores. This goal is to help the retailer understand the properties of products and outlets that are crucial in increasing sales. 

## Data Source: 

[Sales Prediction Data](https://github.com/pylabview/sales-predicctions/blob/main/sales_predictions.csv)

For this dataset, there were 8523 rows, 10 columns, and one Target feature.

## Data Dictionary

<table>
  <tr>
    <th>Variable Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Item_Identifier</td>
    <td>Unique product ID</td>
  </tr>
  <tr>
    <td>Item_Weight</td>
    <td>Weight of product</td>
  </tr>
  <tr>
    <td>Item_Fat_Content</td>
    <td>Whether the product is low fat or regular</td>
  </tr>
  <tr>
    <td>Item_Visibility</td>
    <td>The percentage of total display area of all products in a store allocated to the particular product</td>
  </tr>
  <tr>
    <td>Item_Type</td>
    <td>The category to which the product belongs</td>
  </tr>
  <tr>
    <td>Item_MRP</td>
    <td>Maximum Retail Price (list price) of the product</td>
  </tr>
  <tr>
    <td>Outlet_Identifier</td>
    <td>Unique store ID</td>
  </tr> 
  <tr>
    <td>Outlet_Establishment_Year</td>
    <td>The year in which store was established</td>
  </tr> 
  <tr>
    <td>Outlet_Size</td>
    <td>The size of the store in terms of ground area covered</td>
  </tr> 
  <tr>
    <td>Outlet_Location_Type</td>
    <td>The type of area in which the store is located</td>
  </tr> 
  <tr>
    <td>Outlet_Type</td>
    <td>	Whether the outlet is a grocery store or some sort of supermarket</td>
  </tr> 
  <tr>
    <td>Item_Outlet_Sales</td>
    <td>Sales of the product in the particular store. This is the target variable to be predicted.</td>
  </tr> 
</table>



## To prepare this data, the data was cleaned, and the following processes were performed:

### Exploratory Data Analysis
```
- Dataframe datatypes of each variable.
- Removing duplicates.
- Identify missing values.
- Define strategy to address missing values.
- Confirm that there are no missing values after addressing them.
- Find and fix any inconsistent categories of data.
```


> The Item Identifier will not offer good information for the prediction; this feature is like an ID with 1559 unique values. I am dropping this column.
> The Outlet_Size has 28.3% total missing values (8523/2410) and we don't have enough information to fill this feature, so we are dropping this column too


<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Item_Outlet_Sales_Distribution.png">
</p>
<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Item_Outlet_Sales_PlotBox.png">
</p>


This histogram shows that the majority of the food items sales are around 2,181. There are some outliers items with sales > 6000.


 ### Expanatory Data Analysis

    - To visualize the data for explantory purposes, four bargraphs were chosen.
    - The bargraphs were chosen to show how the categories compare to each other. 
   


## Explanatory Visuals

<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Fat_Content.png">
</p>



The stores are bringing more Low Fat Items than Regular:
- Low Fat:    `5517`
- Regular:    `3006`


<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Item_Type_by_Sales.png">
</p>



>Sea and Starchy Food Items show the best sales, baking items the lowest 



<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Store_Sales_by_Time%2Bin_Business.png">
</p>

Outlet_Identifier|  Outlet_Establishment_Year | Sales
|:--|:--|:--|:--|:--|
OUT027     |        1985         |                3694.038558
OUT035     |        2004         |               2438.841866
OUT049     |        1999         |                2348.354635
OUT017     |        2007         |                2340.675263
OUT013     |        1987         |                2298.995256
OUT046     |        1997         |                2277.844267
OUT045     |        2002         |                2192.384798
OUT018     |        2009         |                1995.498739
OUT019     |        1985         |                 340.329723
OUT010     |        1998         |                 339.351662

> The Stores time in business has the more significant effect on sales: Outlet 27 (1985)



<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Store_Sales_by_Type.png">
</p>


>The store location doesn't have a significant effect. The best store (27) and the worst one (10) are from tier 3


 ### Machine Learning Using the Following Models:

    - Baseline Model (Dummy)
    - Linear Regression Model
    - Decision Tree Regressor Model
    - Random Forest Regressor Model


​    

## Models Evaluated & Results

| Training Model |MAE  |MSE  | RMSE | R^2 |
|:--|:--|:--|:--|:--|
| Baseline (Dummy) | 1360.2184  | 2959455.7045 | 1720.3069 | 0.0 |
| Linear Regression |847.2994   | 1298294.1143 | 1139.4271 | 0.5613065 |
| Decision Trees | 762.6851 | 1172179.4097 | 1082.6723 | 0.6039206 |
| Random Forest Trees | 295.3615  |  179682.3558|423.8896  | 0.9392853 |


| Test Model |MAE  |MSE  | RMSE | R^2 |
|:--|:--|:--|:--|:--|
| Baseline (Dummy) | 1326.121  | 2772144.4627  | 1664.9758 | -0.0047725 |
| Linear Regression |804.0018   | 1192926.5671 | 1092.2118 | 0.56762 |
| Decision Trees | 738.4201  | 1118255.1591 | 1057.4758  | 0.5946849 |
| Random Forest Trees | 767.8727   |  1219558.1845|1104.3361  | 0.5579673 |


- The Base Model performed the worst of all simulations
- The Linear Regression Model has good Variance with poor Bias
- The Decision, Ramdon Forest, and Bagged Tree Models have similar performance: High Variance with some Bias on the Testing R^2 scores


## Recommendations

>I recommend using the Random Forest, which has the best Testing Score (R^2) of `0.5946849`. This model still has some bias. However, this model performs best on the testing set with LOW Variance.
>Food Type, Retail Price, and Establishment Year indicated having more effect in the Stores sales

## Revisited: Importances and Coefficients
### Linear Regresion Summary
- What features made the model predict a higher price?
  >- Item_MRP

- Which feature made the model predict a lower price?
  >- Item_Weight, Item_Visibility
- What effect does having more visibility have on predicted price?
  >- Decreases home value by ~$220

<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Linear_Regression_Coefficients.png">
</p>

### Random Forest Summary
- What features made the model predict a higher price?
>  - Item_MRP, Item_Visibility, Item_Weight

- Which feature made the model predict a lower price?
>  - None

<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/Random_Forest_Coefficients.png">
</p>

### Global Explanations
<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/global_bar.png">
</p>


<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/global_dot.png">
</p>

#### Shape Summary
- MRP
> The higher the MRP increase the likehood of predicting item sales

- Visibility:
> The smaller the visibilty, the model likehood decrease in sales prediction 

### Local Explanations
<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/sharp_ind.png">
</p>


<p align = "center"> 
  <img src = "https://raw.githubusercontent.com/pylabview/sales-predicctions/main/rf_sharp_Light.png">
</p>


> For the item ```431th```, The MRP has a stronge correlation to predict the target vaue: Outlet sales.

