# AGS URL

Example URL: http://sampleserver6.arcgisonline.com/arcgis/rest/services/LocalGovernment/Events/MapServer

This can broken down into:  
- http: protocol  
- sampleserver6.arcgisonline.com: is the host
- arcgis/rest: root which can be broken into:  
    - arcgis: instance
    - rest: constant
- services: is a constant
- LocalGovernment: folder name
- Events/MapServer: service which can be broken into:  
    - Events: service name
    - MapServer: service type

# Routes
## p
p for Protocol. Either HTTP or HTTPS.  
This should be optional. It would disappear if the user didn't specify anything.  
The default value is HTTPS but it should fall back to HTTP if HTTPS isn't available.  

## host
Just the base url, only the name of the server: sampleserver6.arcgisonline.com 

## instance
The name of the instance. Usually: arcgis.

## folder
The name of the folder's path.  
It must allow for / in the value.  
ex: /this/is/the/full/folder/path  

## services
There's one route for each service type  
ex: MapServer, FeatureServer, GPServer, etc  
The name of the route is the name of the service type.  

## operations 
Each operation will have its own route.  
ex: Query, ApplyEdits, ExportMap, Identify, etc.  

# Treeview
Use [jsTree](https://www.jstree.com/) which has an [Ember plugin](https://github.com/ritesh83/ember-cli-jstree)  

## How to share tree state/data across the application
Tree data is stored in the controller. If the tree is added in `application.hbs`, then `data` is stored in `controller/application.js` as a property of the application object.  
