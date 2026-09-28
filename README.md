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

-# Before
<img width="676" height="504" alt="image" src="https://github.com/user-attachments/assets/aa794db1-3ae3-454b-958f-5eb1d9e13f37" />

-# After
<img width="608" height="444" alt="image" src="https://github.com/user-attachments/assets/f9f575cd-4bb7-40a0-9110-0d874b85ce77" />




