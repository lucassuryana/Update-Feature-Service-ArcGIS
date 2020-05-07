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

After we install the ArcGIS API for Python, we need to connect to our Portal/AGOL in Python.
```ruby
# Import arcgis libraries
from arcgis.gis import GIS
from arcgis import features

# Credentials
# Fill in with your own credential
user = ""
passw = ""

# Connect to your portal/AGOL
gis = GIS("https://petroleumid.maps.arcgis.com/home", username = user, password = passw)
```

Now we will start by updating the feature layer then the table

<b>Updating feature layer</b>

In this case, we will update the location and the contractor name of well

STEP 1: Connect to our editable feature layer.
```ruby
# Get the item id for feature layer
layerid = '62aaf425cc3d4222b3e228bddd70282a'

# Search for the feature layer
search_result = gis.content.search(layerid)

# Access the item's feature layers
well_item = search_result[0]
well_layers = well_item.layers

# Access the editable feature layers
well_flayer = well_layers[0]
```

We can get the item id on our layer’s URL
![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/itemid.png)

STEP 2: Create a JSON file that will update the feature layer. We will change the Abab field location into a new location and change the contractor’s name.

```ruby
# We need to reconstruct json features to be updated
fname = 'Abab'
year = 2018
cont = 'Baker Hughes'
Lat = -6.70
Long = 107
objid = 1

# converting lat long to meter
ty = Lat * 10000000 / 90
tx = Long * 10000000 / 90

# construct json
add_data = {
      "attributes" : {
        "Field_Name" : fname, 
        "Year" : year, 
        "Contractor" : cont, 
        "Lat" : Lat, 
        "Long" : Long,
        "ObjectId" : objid
      }, 
      "geometry" : 
      {
        "x" : tx, 
        "y" : ty
      }
    }
```

STEP 3: Push updates

```ruby
# Push updates
well_result = well_flayer.edit_features(updates = [add_data])
```

Now we can see the well location has been moved from Lat: -6.59 Long 106.00 into Lat: -6.70 Long 107.00. The contractor also has been changed from Schlumberger into Baker Hughes.

![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/update-feature.png)

<b>Updating the table layer</b>

In this case, we will change the updated date. Actually this step is exactly the same as the previous step, but the difference is on # access the item’s feature layers part.

STEP 1: Connect to editable table

```ruby
# Get the item id for feature layer
layerid = '7315f7175ad34b9392f1a83ffa693130'

# Search for the feature layer
search_result = gis.content.search(layerid)

# Access the item's table layers
table_item = search_result[0]
table_layers = table_item.tables

# Access the editable table layers
table_flayer = well_layers[0]
```

If we see at the # Access the item’s table layers, instead of using .layers we use .tables as we are not accessing layers but the table.

STEP 2: Create a JSON file that will update the table. We will change the date from 2020–05–02 to 2020–05–03. And if we see closely, we don’t need to create a geometry in the JSON file as table doesn’t have any geometries.

```ruby
# We need to reconstruct json features to be updated
kelurahan_nama = 'BABAKAN'
tgl_update = '2020-05-03'
kecamatan_nama = 'BOGOR TENGAH'
ODP = 18
PDP = 2
POS = 0
jum_selesai = 0
jum_meninggal = 0
ObjectId = 1

# construct json
add_data = {
      "attributes" : {
        "kelurahan_nama" : kelurahan_nama, 
        "tgl_update" : tgl_update, 
        "kecamatan_nama" : kecamatan_nama, 
        "ODP" : ODP, 
        "PDP" : PDP,
        "POS" : POS,
        "jum_selesai" : jum_selesai,
        "jum_meninggal" : jum_meninggal,
        "ObjectId" : ObjectId
      }
    }
```

STEP 3: Push updates

```ruby
# Push updates
well_result = well_flayer.edit_features(updates = [add_data])
```

Now we can see the table’s date has been updated.

![alt text](https://github.com/lucassuryana/Update-Feature-Service-ArcGIS/blob/master/blob/update-table.png)

<b>CONCLUSION</b>

Finishing the step above means we have done an update for the table and the feature layer. And the most important part is that we did that in our Python environment. If we have hundreds or thousands of rows or columns when a manual update is not effective anymore we can use ArcGIS API for Python for doing that.
