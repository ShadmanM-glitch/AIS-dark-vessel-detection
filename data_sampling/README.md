## Dataset 
We will be using the Automatic Identification System (AIS) data to detect the potential dark vessels. AIS is a system that allows ships to transmit their vessel’s data such as id, name, position, and speed. It is a helpful tool to avoid collusions on the sea. For our project, we will utilize AIS data to analyze the vessels' movement so our model can identify dark vessels. The data we will be using is from MarineCadastre.gov. This is a website that provides authoritative ocean data. We will choose the data from the time interval of 2021-01-01 to 2021-01-31. The data has the following features:
 
## Feature Name	Description
MMSI -	It is a unique nine-digit calling number that is used by marine traffic monitoring systems to identify a vessel.
BaseDateTime -	The time that the AIS message was sent
LAT -	Latitude of the vessel
LON -	Longitude of the vessel
SOG -	Speed over ground
COG -	Course over ground. The direction that the ship is actually going
Heading -	The direction that the vessel is intended to go
VesselName -	Name of the vessel
IMO -	A unique permanent reference number assigned to each vessel for identification
CallSign -	The vessel’s unique callsign is assigned by the national authority and allows you to identify the vessel.
VesselType -	Indicates the type of the vessel
Status -	Status of the vessel. Such as at anchor or engaged in fishing
Length -	Length of the vessel
Width -	Width of the vessel
Draft -	The maximum depth of any part of the vessel
Cargo -	Cargo classification
TransceiverClass -	Class of AIS transceiver. Class A and B.

## Identify Dataset:
Finding the appropriate datasets for the topic. AIS data and port information data.
Data Cleaning:
1.	Fill in missing data:
There are missing data in our dataset, so it is important to use methods to fill in the missing data
2.	Delete unnecessary column:
Columns such as MMSI, IMO, and CallSign is pretty similar to each other, so it is enough to only keep the MMSI column.
Feature Engineering:
1.	Create new columns:
Create new columns so that the dataset is more representable of the vessel movement. Columns such as distance traveled (driven from latitude and longitude for two consecutive AIS message from the same vessel), and geohash (creating a new column for the geohash might be also beneficial because this way the algorithm can analyze the vessels movement within an area).
2.	Integrate new dataset:
Integrating a port information dataset can be very beneficial. With this information, we can know when the vessel arrived and departed from a port. Columns such as trip number (vessel from one port to another), departure port, destination port can be added by combining the two datasets together.
3.	Summarize records:
After knowing its trip number, we can make another dataset that consists of all the vessels' trip information. This new dataset can contain columns such as distance traveled in a trip and average velocity. 
Data Versioning:
Create pipeline for data preprocessing, so we can keep all the versions of dataset we have used. The changes we made to the dataset can be stored. We can analyze the different dataset’s impact on the model, and see which dataset is better to use.
Data Visualization:
By using the Plotly library, we are able to see the vessel’s movement on map and more easily to get an overview of the dataset.
Model Training:
Apply PCA to reduce the dimensions. Try to train an unsupervised learning for our dataset. Mini Batch KMeans could be a possible model to use because the dataset is expected to be large.
Hyperparameter Tuning:
Tune the hyperparameter to indicate the suitable hyperparameters for our model to perform dark vessel detection.
Model Versioning:
Create pipeline for generating and training the model. Different models based on different versions of dataset and hyperparameters could be generated, so it is good to keep track of all the model versions we have.
Model Testing and Evaluation:
Test and evaluate our model with different evaluation metrics.
Model Visualization:
Create visualizations for the model evaluation so it can be seen clearly how the model is doing.
Benchmark:
Run other models on our dataset and evaluate their performance. Implement a hyperparameter tuning if necessary for these models.
Comparison Visualization:
Make visualization for all the benchmark models and compare the performance to our model.

