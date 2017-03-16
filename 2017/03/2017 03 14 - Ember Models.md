# Models

## Transforms

In `DS.attr('string')`, string isn't a data type, but is called a transform.  
You can [define your own transform](https://guides.emberjs.com/v2.11.0/models/defining-models/#toc_custom-transforms). Use `ember generate transform dollars`.  
Then use it as `DS.attr('dollars`)`.  

## Reflexive Relations

When you want to define a reflexive relation (a model that has a relationship to itself), you must explicitly define the inverse relationship. If there is no inverse relationship then you can set the inverse to `null`. [More info](https://guides.emberjs.com/v2.11.0/models/relationships/#toc_reflexive-relations)  

## Polymorphism 

Polymorphism is when you want to define a type (model) and its children. Ex: payment method and its children: Visa, Master Card, Cash, etc.  

# Serializers

The `normalizeResponse` function is called once when the adapter gets the response from the server. It passes the response as the `payload` parameters.  
This function transforms the payload returned from the server to a JSON API object.  
JSONAPI object has [this format](http://jsonapi.org/format/#document-structure):  
```json
{
    "data": {
        "id": "id",
        "type": "objectType",
        "attributes": {
            "attr0": false,
            "attr1": 1,
            "attr2": "two"
        }
    }    
}
```
Other parameters are:  
- `store` references the data store.  
- `primaryModelClass` is a Model object that references the model being retrieved.  
- `id` is the ID of the data object being retrieved.  
- `requestType` is the type of the request being made to the data store. It could be 'findRecord', 'queryRecord', 'findAll', 'findBelongsTo', 'findHasMany', 'findMany', 'query', 'createRecord', 'deleteRecord' and 'updateRecord'.  