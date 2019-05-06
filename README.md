Neural Network Analysis of San Francisco 311 Data
Data: https://data.sfgov.org/City-Infrastructure/311-Cases/vw6y-z8j6 

San Francisco receives thousands of 311, or non-emergency service requests each year. The requests are classified as different types. Most of these requests also contain an image of the reported issue. I want to predict what kind of service request it is from the image. 

Predicting the type of request from the image could save time in reporting issues since people would need to fill out fewer form attributes. This could encourage more people to submit a request and help San Francisco to be better maintained. It could also help the city confirm that requests are correctly submitted and for resource allocation. 

My data comes from San Francisco open data. There are 3.48M available samples in the data set. If an image was provided with the service request, a URL is included in the data set. Requests was used to query these URLs and download images. Due to RAM and time constraints, this analysis was limited to images taken in 2017 and 2018. I used requests.get to download the images associated with the data points, and this resulted in about 160,000 classified images. 

Exploratory data analysis was used to look at the categorical variables associated with each of the downloaded samples. Street, neighborhood, day of the week, and month were included. A random forest classifier was used to determine a baseline for what kind of accuracy coud be expected from running a model on just the categorical data. 

Next, neural networks were used to classify the samples by image. The first attempt to model the data was with a convoluted neural network I created. After tuning, this neural network achieved an accuracy of 48%. I then used VGG16 to model the image data. The accuracy of the model imporved to 50% with the use of the pretrained model. Next, I modeled the categorical data using a multi-level perceptron model. Once I achieved similar accuracy as the random forest model I had previously created for the data, I considered it tuned. 

My next step was to see what would happen when I combined models. Combining just the VGG16 model and the MLP model resulted in a lower accuracy in the 30s, even after trying many variations of including fully connected layers and dropout after the data in concatenated. However, when all three models are combined (CNN, VGG16, MLP), my top accuracy improves from 50% to 52%.

