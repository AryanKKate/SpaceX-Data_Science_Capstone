# Data Science Capstone project on SpaceX 
FINAL PROJECT FOR PROFESSIONAL DATA SCIENCE CERTIFICATE

<h2>Problem Statement : </h2>
<p>In this capstone, we will predict if the Falcon 9 first stage will land successfully. SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is because SpaceX can reuse the first stage. Therefore if we can determine if the first stage will land, we can determine the cost of a launch. This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.</p>

<h3>Resources : We will be gathering data from the official SpaceX APIs and webscraping from wikipedia</h3>

<p>Rocket Data : https://api.spacexdata.com/v4/rockets/</p>
LaunchSite Data : https://api.spacexdata.com/v4/launchpads/</p>
Payload Data : https://api.spacexdata.com/v4/payloads/</p>
Core Data : https://api.spacexdata.com/v4/cores/</p>
Launch Data : https://api.spacexdata.com/v4/launches/past</p>
Falcon9 wikipedia (Webscrape) : https://en.wikipedia.org/wiki/List_of_Falcon_9_and_Falcon_Heavy_launches

<h2> Contents :</h2>
<h2>1 : Data Collection using API :</h2>
In this notebook, we have worked on collecting and preparing data from the SpaceX API to predict if the Falcon 9 first stage will land successfully. Here's a summary of the tasks we have completed:

1. **Library Imports and Helper Functions**:
   - Imported `requests`, `pandas`, `numpy`, and `datetime`.
   - Defined functions to fetch specific data from the SpaceX API.

2. **Data Retrieval and Cleaning**:
   - Retrieved launch data from the SpaceX API.
   - Filtered and selected relevant columns.
   - Converted `date_utc` to datetime and filtered launches up to November 13, 2020.

3. **Additional Data Extraction**:
   - Used helper functions to extract booster version, launch site, payload data, and core data.
   - Stored the extracted data in global variables.

4. **Dataframe Construction**:
   - Created a new dataframe `data_launch` with the extracted data.
   - Verified the dataframe structure.

5. **Filtering Falcon 9 Launches**:
   - Filtered the dataframe for Falcon 9 launches.
   - Reset the `FlightNumber` to be sequential.

The resulting `data_falcon9` dataframe includes comprehensive details for Falcon 9 launches, ready for further analysis and modeling to predict landing success.

<h2>2 : Data collection with webscraping :</h2>
In this notebook, we performed web scraping to collect Falcon 9 historical launch records from a Wikipedia page titled List of Falcon 9 and Falcon Heavy launches
The task involves web scraping Falcon 9 launch records from a Wikipedia page using BeautifulSoup. The process includes:

1. **Importing Required Libraries:** Importing libraries such as `requests`, `BeautifulSoup`, `re`, `unicodedata`, and `pandas`.
2. **Helper Functions:** Defining several helper functions to process the web-scraped HTML table, including functions to extract date and time, booster version, landing status, and payload mass.
3. **Fetching HTML Data:** Using the `requests` library to fetch the HTML content of a specific Wikipedia page.
4. **Parsing HTML with BeautifulSoup:** Creating a BeautifulSoup object from the HTML content and verifying the page title to ensure successful parsing.
5. **Extracting Data from Tables:** Finding all tables on the page and identifying the relevant table that contains the Falcon 9 launch records.
6. **Printing and Checking Table Content:** Printing the content of the identified table to verify the correct extraction.


<h2>3 : Data Wrangling :</h2>
In this notebook, we have applied the concepts of EDA to gather insights from the data

1. **Import Libraries:**
   - Use Pandas for data manipulation and NumPy for numerical operations.

2. **Load and Inspect Data:**
   - The SpaceX dataset is loaded and the first few rows are displayed for initial inspection.

3. **Missing Values Analysis:**
   - Calculate the percentage of missing values for each attribute in the dataset. 
   - The `LandingPad` column has about 28.89% missing values.

4. **Data Types Identification:**
   - Identify which columns are numerical and which are categorical.

5. **Launch Site Analysis:**
   - Determine the number of launches from each site using the `value_counts()` method on the `LaunchSite` column.
   - Launches are primarily from three sites: CCAFS SLC 40, KSC LC 39A, and VAFB SLC 4E.

6. **Orbit Analysis:**
   - Identify the number and occurrences of each orbit type using the `value_counts()` method on the `Orbit` column.

7. **Mission Outcome Analysis:**
   - Determine the number of each type of mission outcome using the `value_counts()` method on the `Outcome` column.
   - Define successful and unsuccessful outcomes based on landing results (True/False Ocean, RTLS, ASDS).

8. **Create Landing Outcome Label:**
   - Convert the `Outcome` column into a binary classification label (`landing_class`), where:
     - `1` indicates a successful landing.
     - `0` indicates an unsuccessful landing.
   - Add this new `Class` column to the dataframe.

9. **Calculate Success Rate:**
   - Determine the overall success rate of the first stage landing by calculating the mean of the `Class` column.
   - The success rate is approximately 66.67%.

<h2>4 : EDA with SQL</h2>
In this notebook, we demonstrated how SQL queries can be used for EDA purposes. Here are some of the many tasks performed:

1. **Unique Launch Sites**: Retrieved unique names of the launch sites from the dataset.

2. **Records with Launch Sites Starting with 'CCA'**: Displayed 5 records where the launch site begins with 'CCA'.

3. **Total Payload Mass for NASA (CRS)**: Calculated the total payload mass carried by boosters launched for NASA (CRS), which totaled 45,596 kg.

4. **Average Payload Mass for Booster Version 'F9 v1.1'**: Computed the average payload mass for boosters of version 'F9 v1.1', which was 2,928.4 kg.

5. **Total Number of Successful and Failed Mission Outcomes**: Listed counts of different mission outcomes, including 'Failure (in flight)' and 'Success'.

6. **Booster Versions with Maximum Payload Mass**: Identified booster versions that carried the maximum payload mass of 15,600 kg.

<h2>4 : EDA with visualization</h2>
In this notebook, we demonstrated visualization of data and performed EDA to gather further insights. 

1. **Flight Number vs. Payload Mass**: Visualized the relationship between flight number and payload mass. Observed that as flight numbers increase, successful landings become more frequent. Heavier payloads tend to reduce the likelihood of successful landings.

2. **Flight Number vs. Launch Site**: Created a scatter plot showing flight numbers against launch sites, colored by launch success. Noted different success rates among launch sites, with CCAFS LC-40 having a 60% success rate, and KSC LC-39A and VAFB SLC-4E having 77% success rates.

3. **Payload Mass vs. Launch Site**: Analyzed how payload mass relates to launch sites. Found that VAFB-SLC has no launches with payloads greater than 10,000 kg.

4. **Success Rate by Orbit Type**: Generated a bar chart showing the success rate for each orbit type. Observed varying success rates across different orbits, with some orbits showing higher success rates.

5. **Flight Number vs. Orbit Type**: Plotted flight numbers against orbit types, colored by launch success. Noted that LEO orbits show a positive relationship with the number of flights, while GTO orbits do not.

6. **Payload vs. Orbit Type**: Visualized payload mass against orbit types, colored by launch success. Found that heavier payloads are more successful in Polar, LEO, and ISS orbits, but GTO orbits show mixed results.

7. **Yearly Launch Success Trend**: Created a line chart of yearly average success rates. Observed a general increase in success rates from 2013 to 2020.

8. **Feature Engineering**: Selected features for future success prediction models, including flight number, payload mass, orbit, launch site, and other related features.

9. **One-Hot Encoding**: Applied one-hot encoding to categorical columns (orbit, launch site, landing pad, and serial) and converted the entire dataframe to `float64`.

10. **Export Data**: Saved the processed data to a CSV file for future use.

These analyses help in understanding factors affecting launch success and preparing data for predictive modeling.

<h2>6 : Visualization with Folium</h2>

This notebook involves using Folium for interactive visualization of SpaceX launch site locations and their geographical context. Here are the detailed steps:

1. **Mark All Launch Sites on a Map**
   - Import necessary libraries (`folium`, `pandas`).
   - Read a dataset (`spacex_launch_geo.csv`) containing launch site coordinates.
   - Initialize a Folium map centered on NASA Johnson Space Center.
   - Add circles and markers for each launch site using their latitude and longitude.
   - Customize markers to display the launch site names.

2. **Mark Success/Failed Launches**
   - Add a column to the dataset for marker colors based on launch success (green for success, red for failure).
   - Create a MarkerCluster to group markers with the same coordinates.
   - Add markers to the cluster based on launch outcomes, using the color to indicate success or failure.
   - Display the updated map with these markers.

3. **Calculate Distances**
   - Add a MousePosition feature to the map to obtain coordinates of points of interest.
   - Calculate distances from launch sites to nearby features (e.g., coastlines) using the Haversine formula.
   - Mark and draw lines on the map to show these distances.
   - Analyze the proximity of launch sites to coastlines, railways, highways, and cities.

The goal is to identify geographical patterns and assess how launch sites are positioned relative to key features.

<h2>7 : Predictive Analysis</h2>

In this lab, we have developed a machine learning pipeline to predict if the first stage of a SpaceX Falcon 9 rocket will land successfully, based on historical launch data. Here are the detailed steps:

1. **Import Libraries and Define Functions**
   - Import necessary libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`, `sklearn`).
   - Define a function to plot the confusion matrix.

2. **Load Data**
   - Load the datasets (`dataset_part_2.csv` and `dataset_part_3.csv`) containing launch data and features.
   - Convert the `Class` column from `data` into a NumPy array and assign it to `Y`.

3. **Standardize Data**
   - Standardize the feature data (`X`) using `StandardScaler`.

4. **Split Data**
   - Split the data into training and test sets with an 80/20 split using `train_test_split`.

5. **Logistic Regression**
   - Create and tune a `LogisticRegression` model using `GridSearchCV` with specified hyperparameters.
   - Output the best hyperparameters and accuracy on the validation data.
   - Evaluate the model on the test data and plot the confusion matrix.

6. **Support Vector Machine (SVM)**
   - Create and tune an `SVC` model using `GridSearchCV` with a range of kernels and hyperparameters.
   - Output the best hyperparameters and accuracy on the validation data.
   - Evaluate the model on the test data and plot the confusion matrix.

7. **Decision Tree Classifier**
   - Create and tune a `DecisionTreeClassifier` model using `GridSearchCV` with various criteria and parameters.
   - Output the best hyperparameters and accuracy on the validation data.
   - Evaluate the model on the test data and plot the confusion matrix.

8. **K-Nearest Neighbors (KNN)**
   - Create and tune a `KNeighborsClassifier` model using `GridSearchCV` with a range of neighbors and algorithms.
   - Output the best hyperparameters and accuracy on the validation data.
   - Evaluate the model on the test data and plot the confusion matrix.

9. **Compare Models**
   - Compare the performance of all models based on their accuracy and confusion matrices to determine the best performing method.

The objective is to assess which classification algorithm provides the most accurate prediction for the success of rocket landings, using hyperparameter tuning and cross-validation to optimize each model.










