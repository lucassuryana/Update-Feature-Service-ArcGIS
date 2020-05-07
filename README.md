# Update Feature Service with Python API for ArcGIS
On this occasion, we will learn how to update a feature service by using ArcGIS API for Python. For you, who's still new in ArcGIS, this is really a powerful API that will help you to manage your tasks with Python. Especially if we are used to programming.
Before we start, make sure that you have an account and access to publish a service on the following (you can choose one)*:
1. ArcGIS Enterprise 
2. ArcGIS Online
*) For the next part, I will use Portal term for ArcGIS Enterprise and AGOL for ArcGIS Online

Next, we first need to publish a service to our Portal/AGOL. The service could be either a table or a feature layer. We will learn how to update the data for both the table and the feature layer.
![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/Table%20and%20Feature%20Layer.JPG)
<p align="center">
  Feature Layer and Table in My Content
</p>

![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/Feature%20Layer.JPG)
<p align="center">
  Feature Layer
</p>

![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/Well.JPG)
<p align="center">
  Table
</p>

Before we start, we need to install ArcGIS API for Python, which is a library in your Python environment.
```
pip install arcgis
```

