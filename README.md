# Overview
Warframe market sim is a proof of concept project about predicting real life changes in how prices change during the life cycle of the game. 

This project is designed to be a showcase of data analysis practices and tools of using DL tools such as pytorch.


# Gathering the data.
Before we can create a prediction model the first step is to gather the data. This was done using python's built in request library, coupled with warframe markets api functions which can be found [here](https://docs.warframe.market/docs/api/orders). Warframe market's item list is a rather large dataset python will need to take a moment to process all the listed items, For the sake of this project I have uploaded a file of a pre  existing scan i did to create my prediction algorithm found below.

[WM_DataCLEANED.zip](https://github.com/user-attachments/files/32775598/WM_DataCLEANED.zip)

<img width="1327" height="727" alt="Screenshot 2026-09-28 170429" src="https://github.com/user-attachments/assets/6858a85f-953f-46ed-ab3a-5ef2bd47b2f6" />

# Filtering the data.
For this demonstration the main variables we are concerned about in the columns are "ITEM_NAME", "PLATINUM", "QUANTITY", "ID", and "ORDER TYPE". So we can drop the first unnamed column. We can do this by converting the .csv file we created earlier into a pytorch dataframe like this

<img width="412" height="52" alt="image" src="https://github.com/user-attachments/assets/aec94cee-9902-426f-8e8c-42c44f3b2506" />

In order for this algorithm to function properly we must make a destination between what even is "valid" data to train our model off of. Filtering the dates ew can see we have  random outliers of date listings from items that were most likely overpriced or forgotten about on the marketplace.

<img width="996" height="446" alt="image" src="https://github.com/user-attachments/assets/808f46fa-bec6-4fc7-a0c7-a26acc5951c6" />

An easy way to start filtering out all this noise is to train the algorithm on a more limited dataset to reduce outliers and extreme values. This is done through trying to get the model to predict the values of just one specific item, in my project i decided to focus on the item named "Nekros prime set" and limiting the data to one year which would be 2024. Doing so instantly makes our data more understandable and less sparatic.

# Before
<img width="676" height="504" alt="image" src="https://github.com/user-attachments/assets/aa794db1-3ae3-454b-958f-5eb1d9e13f37" />

# After
<img width="608" height="444" alt="image" src="https://github.com/user-attachments/assets/f9f575cd-4bb7-40a0-9110-0d874b85ce77" />

# Developing the algorithm
The last thing to do is to gather important data like the buy and sell order prices and what times of the day it would be most profitable to place them. I chose to use RSI(Relative Strength Index) from real life stock trading that helps determine the change in profitability between the time of day.
<img width="372" height="60" alt="image" src="https://github.com/user-attachments/assets/ee40ca30-d08e-4b6d-b3f7-e6564ccd5dae" />

The algorithm this project uses is a LSTM(Long Short Term Memory) which is a recurren neurel network used to learn information over a long sequence of data. This is perfect for a price prediction calculator but with our current data we'd need more variables to help with the "Short term" memory part of the algorithm.

We can find the return percentage of previous days to solve this. This will determine how effective and profitable trades are between a short time span. I chose to calculate the past two days indicated with the new columns of "Returnlag1" and "returnlag2".

<img width="598" height="440" alt="image" src="https://github.com/user-attachments/assets/19e477dc-539d-4503-af46-f3c9e0f5f3f2" />
<img width="580" height="322" alt="image" src="https://github.com/user-attachments/assets/e11151fc-6446-40b8-be90-577fa7c85ec2" />

With this were finally ready to use pytorches library to create a simple LSTM. For my algorithm i found the sweetspot for my amount of data was 50 epochs, but with a larger or smaller dataset for certain warframe items would require more tuning with pytorches "hyperparameters". For visualization purposes the repo adds a evaluation function to see how effective the simulation ran throughout a set point of time.
<img width="844" height="547" alt="image" src="https://github.com/user-attachments/assets/0276bd55-bb42-4dba-b19c-de8ca60b6e78" />










