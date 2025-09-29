<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

  <h1>Delivery Time Prediction 📦</h1>
  <p>This project aims to predict the delivery time of orders using a machine learning model. The analysis is performed using a dataset of Amazon deliveries and focuses on data cleaning, feature engineering, and model training with a simple linear regression model.</p>
  <hr>
  <h2>📁 Repository Contents</h2>
  <ul>
    <li><code>Delivery_Time_Prediction.ipynb</code>: A Jupyter Notebook containing the complete analysis, including data loading, preprocessing, and model training.</li>
    <li><code>amazon_delivery.csv</code>: The dataset used for this project (not provided, but assumed to be present).</li>
  </ul>
  <hr>
  <h2>🚀 Objective</h2>
  <p>The main goal of this analysis is to predict the <strong>Delivery_Time</strong> of an order <cite></cite>. The following features are used to build the predictive model <cite></cite>:</p>
  <ul>
    <li><code>Agent_Age</code>: Age of the delivery agent <cite></cite></li>
    <li><code>Agent_Rating</code>: Rating of the delivery agent <cite></cite></li>
    <li><code>Order_Time</code>: Time when the order was placed <cite></cite></li>
    <li><code>Pickup_Time</code>: Time when the order was picked up <cite></cite></li>
    <li><code>Weather</code>: Weather conditions during delivery <cite></cite></li>
    <li><code>Traffic</code>: Traffic conditions <cite></cite></li>
    <li><code>Vehicle</code>: Vehicle type used for delivery <cite></cite></li>
    <li><code>Area</code>: Area type (e.g., Metropolitan, Urban) <cite></cite></li>
    <li><code>Category</code>: Product category (e.g., Electronics, Grocery) <cite></cite></li>
    <li><code>Distance</code>: Distance between the store and the drop location <cite></cite></li>
  </ul>
  <hr>
  <h2>🛠️ Methodology</h2>
  <h3>1. Data Loading and Initial Exploration</h3>
  <p>The analysis begins by loading the <code>amazon_delivery.csv</code> file into a pandas DataFrame and performing initial checks to understand the data's structure, including the number of rows and columns, data types, and presence of missing values <cite></cite>. The dataset contains 43,739 observations and 16 columns <cite></cite>.</p>
  <h3>2. Data Cleaning and Preprocessing</h3>
  <ul>
    <li><strong>Handling Missing Values</strong>: The columns <strong><code>Agent_Rating</code></strong> and <strong><code>Weather</code></strong> contain a small number of missing values (54 and 91 respectively) <cite></cite>. Since these missing values make up only a tiny fraction (0.33%) of the total dataset, the corresponding rows are dropped <cite></cite>.</li>
    <li><strong>Handling Duplicates</strong>: The dataset was checked for duplicate records, but none were found <cite></cite>.</li>
    <li><strong>Handling Outliers</strong>: Outliers were identified and removed from the <strong><code>Distance</code></strong> column using the Interquartile Range (IQR) method <cite></cite>. Other numerical columns with outliers were kept as they were deemed to be normal variations in the data (e.g., a low agent rating is a valid data point) <cite></cite>.</li>
    <li><strong>Handling Typos</strong>: Categorical columns like <code>Weather</code>, <code>Traffic</code>, <code>Vehicle</code>, <code>Area</code>, and <code>Category</code> were checked for typos or inconsistencies using <code>value_counts()</code> <cite></cite>. The notebook indicates that no typos were found <cite></cite>.</li>
  </ul>
  <h3>3. Feature Engineering and Transformation</h3>
  <ul>
    <li><strong>Distance Calculation</strong>: The four geographical coordinates (<strong><code>Store_Latitude</code></strong>, <strong><code>Store_Longitude</code></strong>, <strong><code>Drop_Latitude</code></strong>, <strong><code>Drop_Longitude</code></strong>) were combined into a single feature called <strong><code>Distance</code></strong> using the Haversine formula <cite></cite>. The original columns were then dropped, as was the irrelevant <code>Order_ID</code> column <cite></cite>.</li>
    <li><strong>Date and Time Features</strong>: The <strong><code>Order_Date</code></strong> was split into <strong><code>Order_Day</code></strong> (day of the week) and <strong><code>Order_Month</code></strong> <cite></cite>. The <strong><code>Order_Time</code></strong> and <strong><code>Pickup_Time</code></strong> columns were converted into time-of-day categories (morning, afternoon, evening, night) and then one-hot encoded <cite></cite>.</li>
    <li><strong>Categorical Feature Encoding</strong>:
      <ul>
        <li><strong><code>Weather</code></strong>: Values were converted to ordinal numbers based on their impact on commuting: Sunny (1), Stormy/Sandstorms/Windy (2), and Fog/Cloudy (3) <cite></cite>.</li>
        <li><strong><code>Category</code></strong>: The analysis found that most product categories took similar delivery times, with the exception of 'Grocery'. As such, categories were simplified into two groups: Grocery (0) and Non-Grocery (1) <cite></cite>.</li>
        <li><strong><code>Area</code></strong>: 'Semi-Urban' was encoded as 1 and all other area types were encoded as 0 <cite></cite>.</li>
        <li><strong><code>Traffic</code></strong>: This feature was transformed into ordinal numbers from 0 to 3 based on traffic intensity: Low (0), Medium (1), High (2), and Jam (3) <cite></cite>.</li>
        <li><strong><code>Vehicle</code></strong>: This feature was simplified into a binary format: 'motorcycle' (1) and all others (0) <cite></cite>.</li>
        <li><strong><code>Order_Day</code></strong>: This feature was dropped as the correlation with <code>Delivery_Time</code> was found to be very low <cite></cite>.</li>
        <li><strong><code>Order_Month</code></strong>: This feature was one-hot encoded <cite></cite>.</li>
      </ul>
    </li>
  </ul>
  <h3>4. Model Training and Evaluation</h3>
  <ul>
    <li>A simple <strong>Linear Regression</strong> and a <strong>Lasso Regression</strong> model were trained on the preprocessed data <cite></cite>. Both models yielded very low R2 scores of approximately <strong>0.34</strong>, indicating that the simple models were insufficient to capture the complexity of the data <cite></cite>.</li>
    <li>To improve the model, <strong>Polynomial Features</strong> of degree 3 were introduced <cite></cite>. This more complex model resulted in a significantly better R2 score of <strong>0.656</strong>, suggesting a non-linear relationship between the features and delivery time <cite></cite>.</li>
  </ul>
  <hr>
  <h2>📝 Conclusion &amp; Next Steps</h2>
  <ul>
    <li><strong>Order Date and Time</strong> are the most important features in this analysis <cite></cite>.</li>
    <li>A simple linear model is not a good fit for this dataset, but a more complex model using polynomial features provides a much better fit <cite></cite>.</li>
    <li>The model's R2 score improved as the complexity of the features increased. A polynomial model of degree 3 performed significantly better than a simple linear model <cite></cite>.</li>
    <li>The next steps will be to add more features and find more complex relations <cite></cite>. The author notes that their laptop is not currently supporting polynomial features of a degree higher than 3, but they observed that as the model complexity increased, the R2 score seemed to improve <cite></cite>.</li>
  </ul>

</body>
</html>
