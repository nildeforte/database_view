# Database Tables and View
## Summary

An example of a database view created to provide expected data formatting 
for an external vendor API. The view merges and calculates
data from four different tables (collections).

## Databases
* MySQL
* SQLite
* SQL Server (MS SQL)
* MongoDB


## Tables / Collections

#### location
Basic identifying information about a location where data is acquired

#### groupLocations
An index table of locations that can be group together for easier 
reporting of multiple linked locations

#### currentdata
Timeseries dataset of most recent data reported at a location

#### markedStatus
Supplement to currentdata - backend polling and calculation of location data
to flag and confirm current state 

## View
#### currentStatus
provides only relevant data at a location for an external API
to consume and display on a map

* id - the unique location identifier 
* name - the given name of the location
* lastUpdated - timestamp of last received dataset
* status - calculated to display current state - 0, 1, or 3 (0=OFF, 1=ON, 3=UNVERIFIED)
  * if currentdata.step = 0, status is OFF, else more action is needed to verify
  * if markedStatus.statusMark = even, status is ON, else more action is needed to verify
  * if markedStatus.unverified != 1, status is ON, else there was not enough to confirm state (UNVERIFIED)
* latitude - decimal degrees of geographical location latitude
* longitude - decimal degrees of geographical location longitude 
