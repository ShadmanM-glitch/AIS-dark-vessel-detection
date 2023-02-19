# Sampling AIS Dataset Using 2000 Unique MMSI

## Dataset we have

The raw AIS data contains 31 csv files each is about 600mb to 1gb. They are the ais data in the fifth month of 2022. All of the files are store in an `AIS_full` folder in the [raw folder](../../data/raw). A local view of the file is provided below.

![The file stucture on a local machine](../../reports/figures/sampling/local_file_structure.png)

## Goal and approaches

The goal is to shrink the size of the dataset. The (`Data_sampling` file)[Data_Sampling.ipynb] used the approach of sampling the MMSI to obtain a porportion of the full dataset. Directly sampling the full ais dataset is not optimal in our project because we want to analyze the movement of vessels in order to detect the obnormal vessels that are not moving as other similar vessels'. By sampling the full ais dataset, records in the middle of a trip could be droped and the movement won't be analyzed properly. For example, if a vessel is moving from point A to point B and there are 3 ais messages sent during the trip, 1 of the message could be droped because we are randomly sampling the whole dataset. In this case, we would lost information for this trip. 

Instead, we use the sampling technique to the MMSI only so that we randomly pick 2000 different vessels. Then, we retrieve the selected MMSI's ais messages so that no ais message for the vessels are lost.

## Short EDA on the sampled dataset

After the sampling, we are left with `(11467262, 17)` records in the sampled ais data as shown in the [EDA_on_sampled_data file](EDA_on_sampled_data.ipynb). Two plotly graphs are ploted to show the movement of the first 5 vessels. One of the two graphs generated are shown below.

![plotly figure for the first five vessels' path](../../reports/figures/sampling/plotly_generated_graph.png)

However, the path is not a sinlge connected line for each vessel as expected. (The single connected line idicating the vessle's path). There are also interconneceted lines which we don't know why it occurs.