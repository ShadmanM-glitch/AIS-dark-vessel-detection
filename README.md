# AIS-dark-vessel-detection
Dark vessel detection using AIS data of May 2022

Abstract
This project aims to address a possible preemptive solution to prevent Dark vessels from performing illegal activities. These vessels can partake in several illicit activities such as narcotics trafficking, illegal fishing, and violations of human rights. Additionally, they damage the environment by losing or discarding their fishing gear.

The proposed solution employs machine learning technology, which can offer information on missing ships, enabling for more stringent regulation of maritime resources and organized crime. The method will use AIS transponder data to train our model using unsupervised learning algorithms. Using this model, if a fishing vessel deviates from its predicted path, a nearby coast guard or Maritimes patrol unit can be dispatched to investigate the suspected dark vessel, or if the vessel is detected deviating from its predicted path, it can be flagged on the system and detained when it arrives in port, allowing an unexpected quota of fish to be confiscated and fined.

![alt text](https://github.com/ShadmanM-glitch/AIS-dark-vessel-detection/blob/main/Assests/Picture1.jpg)

Problem Statement
Problem
The challenge of finding dark vessel is that it takes large computation resources to process all image and AIS were turned off for dark vessels. If an interval of small time of anomaly activity can be addressed in SAR database by using AIS data, it is much easier to find dark vessels with relatively low cost. 

Challenges

•	The AIS dataset usually contains multiple signal instances of single vessel in different time periods. Process a significant number of vessels will take long time. The anomaly detection model needs to be fast and efficient for viable result produce time.
•	Dark vessel will turn off AIS signal when conducting abusive actions, so there is no ground truth for if a vessel is anomaly or not. All evaluation can only be evaluated in simulated situation.

Proposed Technique
Model Selection
We initially proposed DBSCAN as our model for detecting outliers. We planned to treat the noise that is being detected by DBSCAN as the outlier. However, we could not train the DBSCAN model when we tried to train it. We found out that this model cannot be used for large dataset and the noise is also pretty different from outlier. So, we eventually found Local Outlier Factor as our model. Then, we used the Isolation Forest as another model to compare to our model.

![alt text](https://github.com/ShadmanM-glitch/AIS-dark-vessel-detection/blob/main/Assests/Picture2.png)

Preprocessing
AIS data contains static information of vessel type, name, and MMSI that unique to all vessels, dynamic information of ships position, time, status, the direction vessel heading towards. Although the dataset is really large and contains lots of useful information, we have lots of values missing and duplicated features. So, preprocessing is needed for our project.

Two approaches were taken when preprocessing the AIS dataset:

The first approach is:
Preprocessing process: columns deemed unnecessary for the scope of our project, were dropped such as “Length”, “Width”, “Draft”, “Cargo”. In addition, since vessels can be identified with their unique MMSI; the columns “VesselName”, “IMO” and “CallSign” were also dropped. A missing value check was performed on the dataset which revealed there were two columns with missing data. 
They were “Vesseltype” and “Status” with 38904 and 3005730 no of missing data respectively. To impute the missing data of “Status” column we implemented K nearest neighbors. The missing values of “Status” were isolated and existent values were used as the dependent variables after performing a train_test_split with a 30 percent test size. For the independent variables the columns of “LAT”, “LON”, “SOG”, “COG”, and “Heading” were used. This algorithm had an accuracy score of 88.5 percent which is fairly acceptable. The predicted data was then used to impute the “Status” column of the data frame using the “fillna” function with “inplace” parameter set to True. The sampled dataset being used for this project has 2000 unique MMSI so we checked for unique MMSI for the 38904 missing “VesselType” data. Since only 109 MMSI were missing “VesselType” values, they were dropped as it accounted for less than 20 percent of the dataset. Next the “TransceiverClass” had 2 unique labels, A or B which were mapped to 1 or 0 respectively. Finally, the “BaseDateTime” columns were split into “Date” and “Time” columns; where “Date” contains day as the data being used is from the month of May 2022 and “Time” is the time of receiving the signal from the transponder in minutes. Lastly, the cleaned dataset was stored as a CSV file with index set to False to prevent adding an index column to the file.

 
Another approach is to reconstruct AIS senser signal data into Trip dataset by removing the multiple AIS signal instance of regular time. Leaving start and end position of dock that vessel moving out and docking in, start time, time point and period travel, and the furthest point where vessel send its AIS data away from start point. This will give us more concise data points and we will be able to analyze each trip instead of all the data points during a trip.

![alt text](https://github.com/ShadmanM-glitch/AIS-dark-vessel-detection/blob/main/Assests/reconstruct.jpg)

Evaluation Metrics
The evaluation for unsupervised anomaly detection model is different from many other models as we do not have the true label of the dark vessel. This makes it hard to evaluation our model’s performance. There are some approaches we looked at and analyzed.

F1, Precision and Recall
These are the common evaluation metrices for many models. It can also be used for anomaly detection model to get its accuracy. However, we do not have the true label for dark vessel so none of these metrices can be used in our model evaluation.

Data Simulation Strategy
One of the approaches is to simulate and manually generate some outlier data and include these into our AIS dataset. Then, label these self-generated data as outlier. This way, we can use normal evaluation matrices to evaluate our model. However, there are many difficulties and obstacles for this evaluation approach. Firstly, we do not know what a dark vessel’s AIS data looks like. Then, we have a large number of records in our dataset (millions of rows). So, we need to create lots of fake outlies, and it is hard to make 0.001% percent of the data as outliers. Therefore, this approach is not suitable for our project.

Evaluation Metrics
In the end, we planned to use a side approach to evaluate the performance of our model which is inspired from this paper [9]. In this approach, we do not evaluate the model’s performance directly. We measure the mode’s efficiency and generate plots for detected outlier and compare those to consider which model is better.

![alt text](https://github.com/ShadmanM-glitch/AIS-dark-vessel-detection/blob/main/Assests/compare.png)

LOF performed best as fewer dark vessels were identified so it's more viable than IF.
The outlier has a higher chance of being a dark vessel.



