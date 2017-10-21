# DisasterResourceTracker
Specs for the DisasterResourceTracker the Miami Day of Civic Hacking

## Features
- Faceted search including location with map and table view
- Saved searches + notifications (e.g. when availability changes of plywood near me)
- Separate permissions for Location CRUD and AvailabilityReport CRUD
- Simplified Text DSL (over sms or even just super basic web app)
	(resource, location) -> [result]
	(resultID) -> location that iMessage can link to maps (probably just address)



## Criteria for ideal resources to track
- Consumable
- Replenish-able
- Broad demand and appeal mid-crisis(e.g. water/plywood is universal and people care enough to report)
- Prone to scarcity ("the first things to go")
- Generic in type (e.g. water not Dasani)

Generalizing that, *universally demanded commodities* seem like a good fit. Things like service and needs can be modeled but it's not ideal (e.g. a "resource" of people needing something at a location)


## Models

### Location
| Field | Type | Description |
| --- | -- | -- |
| Name | `string` | Name of the Resource Host (e.g. store name, service name, etc) |
| URL | `string` | An optional external URL for more info from the Resource Host |
| Location | `geo` | The lat/long cooridinates of the resource |
| ExternalID | `string?` | An optional external system id for integrtation with existing systems |
| ExternalSystem | `string?` | An optional name of an external system |
| ResourceType | `string` | Type of resource from a finite list, e.g. `water`, `gas`, `plywood` |
| ResourceAvailability | `float` | 0-1 quantity indicating current availability, e.g. 0, 0.5, and 1 for a red/yellow/green scale or straight slider (calculated in light of AvailabilityReports) |

*Note* ResourceType and ResourveAvailability could be in a Resources array to support multiple resources per location without fully denormalizing



### AvailabilityReport
| Field | Type | Description |
| --- | -- | -- |
| User | `ID` | User doing Reporting |
| Timestamp | `datetime` | Time of report |
| LocationID | `ID` | Location of Resource |
| ResourceType | `string` | Resource being reported about |
| ResourceAvailabilty | `float` | New availability being reported |
| Image | `string` | URL of uploaded image |
| Comments | `[{message:string, user:ID}]` | Discussion about report |




## Tech Stack
- Elasticsearch (For Indexing Locations + Geo based search)
- Node
- React
- Contexture (https://www.npmjs.com/package/contexture)
- Futil (https://www.npmjs.com/package/futil-js)
