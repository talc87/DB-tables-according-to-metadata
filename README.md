# DB-tables-according-to-metadata doc


Hi!
This class will let you create "On the fly" mySQL tables according to a json metadata.
the class uses 2 objects:
1. ExtractionConfig json file includes the list of tables you are asking to create table ("Scoped entites").
2. The MongoDB will include the ,metadata of all the entities.

**The class will create the mySQL table for the scooped entities in the ExtractionConfig json file.**


## Prequision

beside python and the relevant depandadices, you should have the following DB created.
 1. MongoDB instance- the mongoDB will stored the tables metadata. [I used the Atlas free tier](https://www.mongodb.com/)
 2. MySQL instance- **The db name shpuld match the CollectionName **.
 3. ExtractionConfig JSON file



## Setting up the MongoDB:
The MongoDB collection will stores the meatadata for all the entites at the following schema:

 - DB Name- defined by the user.
 - Collection name= defined by the user.
 - MongoDB document schema:
	 - _id- the table name. mongoDB primary key.
	 - Desc- description of the table name (optional)
	 - Fields- Python list of the fileds in the table. For each file you need to define:
		 -  FieldName (mandatory)- string
		 - Field Description (optional)- string
		 - Is the filed is a primary key (mandatory)- Boolean- The class support multiple primary keys in a table.
		 - MySql datatype (mandatory)- String. The datatype in the 'TargetDataType' must by a MySQL datatype.
	
**An example of a metadata document:**
 
```go
{
	"_id": "ABILITIES",
	"Desc": "enter table (entity) description you want",
	"Fields": [{
		"FieldName": "ABILITYCODE",
		"Desc": "enter field description you want",
		"KeyFlag": true,
		"TargetDataType": "String(256)"
	}, {
		"FieldName": "ABILITYDES",
		"SourceDataType": "Edm.String",
		"desc": "enter field description you want",
		"KeyFlag": false,
		"TargetDataType": "String(256)"
	}]
}
```




## ExtractionConfig JSON file

Is cases you don't want to create DWH tables for the entire metadata collection, you can filter your required and created DB tables for  spasific tables.
You should details you reqested tables in the "ExtractionConfig JSON file".
The ExtractionConfig JSON example:

```go
{

	"entities": [{
		"EntityID": "AINVOICES"
	}, {
		"EntityID": "ABILITIES"
	}]
}
```
