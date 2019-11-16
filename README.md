# The Water Framework REST API
The Water Framework REST API can deploy vast amounts of data about water, soil, snow and vegetation.    This API follows the NOAA API format and structure.  

## API Structure

**BASE URL** | **MATERIAL** | **TYPE** | **PRODUCT** | STATION | DATE | UNITS | TIME_ZONE | INTERVAL | FORMAT | KEY

```yaml
GET:
  https://thewaterframework.com/api/v1/:
  
    material: water
    data_type: data
    product: ["water_level"], ["water_capacity"], ["tide"],["tide_current"],["wave_height"],["ice_layer"],["snow_layer"]
    
    material: land
    data_type: data
    product: ["soil_moisture"], ["veg_height"], ["veg_density"],["snow_accum"],["snow_density"],["snow_water"],["topology"]
    
  options:
    station: station, range, all
    date: ['*/*'] # numerous options available
    units: metric, standard
    time_zone: gst, lst, lst_dst
    interval: h, hilo
    format: json, xml, csv
```

### Example API Requests:

thewaterframework.com/api/v1/water/data?product=water_level&station=3&date=today&units=metric&format=csv&authkey=KEY

# Water Data Products

The ​**product**​ represents attributes of water data.  Specify the type of data with the "product=" option parameter.


| Product | Description |
|:--------|:------------|
| water_level | Specifies the current height of the visible water.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`
| water_capacity | Specifies the capacity of the visible water.<br /><br />**Metric:** `M^3` <br />**Standard:** `Acre Ft.`
| tide | Specifies the height of the current tide.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`
| tide_current | Specifies the speed of the current tide.<br /><br />**Metric:** `M/s` <br />**Standard:** `Ft./s`
| wave_height | Specifies the height of the current wave.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`
| ice_layer | Specifies the thickness of the current ice layer.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`
| snow_layer | Specifies the thickness of the current snow layer.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`

# Land Data Products


The ​**product**​ represents attributes of water data.  Specify the type of data with the "product=" option parameter.

| Product | Description |
|:--------|:------------|
| soil_moisture | Specifies the percentage of water in the visible soil.<br /><br />**Metric:** `%` <br />**Standard:** `%`
| veg_height | Specifies the height of the current vegetation.<br /><br />**Metric:** `M` <br />**Standard:** `Ft.`
| veg_moisture | Specifies the percentage of water in the visible vegetation.<br /><br />**Metric:** `%` <br />**Standard:** `%`
| snow_accum | Specifies the rate of snow accumulation.<br /><br />**Metric:** `M/s` <br />**Standard:** `Ft./s`
| snow_density | Specifies the density of the visible snowpack.<br /><br />**Metric:** `Kg/M^3` <br />**Standard:** `N/A`
| snow_water | Specifies the snow water equivalency.<br /><br />**Metric:** `cm` <br />**Standard:** `inches`
| topology | Specifies the water topology on top of the soil.<br /><br />**Metric:** `M (x,y,z)` <br />**Standard:** `Ft. (x,y,z)`


# Station ID# or Range

The ​**station** ​references which sensor unit or range of units to pull data from.  Specify the type of data with the "station=" option parameter.

| Option | Description |
|:--------|:------------|
| station | A Single sensor unit identied by an **int** (0-9999)
| range | An array of sensors identified by two **int** (0-9999) {A,B}
| all | Return the current data request for ALL active sensors. **Pro License Required**

### Station ID# Examples:

> **Station #292**
> 
> station=292
> 
> **Station Range #292 - #299**
> 
> station=292&range=7
> 

# Date & Time

The ​**date** ​will allow for many different ranges and formats for the interval of time of data to be sent. 

The API understands several parameters related to date ranges.  
All dates can be formatted as follows:  
yyyyMMdd, yyyyMMdd HH:mm, MM/dd/yyyy, or MM/dd/yyyy HH:mm  
  
One the 4 following sets of parameters can be specified in a request:

| Parameter | Description |
|:--------|:------------|
| begin_date and end_date | Specify the date/time range of retrieval
| date | Valid options for the date parameters are: latest (last data point available within the last 18 min), today, or recent (last 72 hours)
| begin_date and a range | Specify a begin date and a number of hours to retrieve data starting from that date
| end_date and a range | Specify an end date and a number of hours to retrieve data ending at that date
| range | Specify a number of hours to go back from now and retrieve data for that date range

### Date & Time Examples:

> **January 1st, 2012 through January 2nd, 2012**
> 
> begin_date=20120101&end_date=20120102
> 
> **48 hours beginning on April 15, 2012**
> 
> begin_date=20120415&range=48
> 
> **48 hours ending on March 17, 2012**
> 
> end_date=20120307&range=48
> 
> **Today's data**
> 
> date=today
> 
> **The last 3 days of data**
> 
> date=recent
> 
> **The last data point available within the last 18 min**
> 
> date=latest
> 
> **The last 24 hours from now**
> 
> range=24
> 
> **The last 3 hours from now**
> 
> range=3

# Units

The ​**units** ​support either Metric or Standard data to be returned.  The unit type can be specified with the "units=" option parameter.

| Option | Description |
|:--------|:------------|
| metric | Return the data using the **metric** form listed for each attribute.
| standard | Return the data using the **standard** form listed for each attribute.

### Units Examples:

> **Get the data returned in metric**
> 
> units=metric
> 
> **Get the data returned in standard**
> 
> units=standard


# Time Zone

The ​**time_zone** is where the sensor data will reference from.  The time_zone can be specified with the "time_zone=" option parameter.

| Option | Description |
|:--------|:------------|
| gmt | Greenwich Mean Time
| lst | Local Standard Time. The time local to the requested station.
| lst_ldt | Local Standard/Local Daylight Time. The time local to the requested station.

### Time Zone Examples:

> **Retrieve data with GMT date/times.**
> 
> time_zone=gmt
> 

# Interval

The ​**interval** decides how much data is sent per time request.  **The default is 6 minute interval** and there is no need to specify it. The hourly interval is supported for Met data and Predictions data only. The output format can be specified with the "interval=" option parameter.

| Option | Description |
|:--------|:------------|
| h | Hourly Met data and predictions data will be returned
| hilo | High/Low tide predictions for subordinate stations.


### Interval Examples:

> **Send data at a 1-second interval**
> 
> interval=h
> 

# Format

The ​**format** will decide what format the data is sent back in.  The output format can be specified with the "format=" option parameter.

| Option | Description |
|:--------|:------------|
| json | Javascript Object Notation. This format is useful for direct import to a javascript plotting library. Parsers are available for other languages such as Java and Perl.
| xml | Extensible Markup Language. This format is an industry standard for data.
| csv | Comma Separated Values. This format is suitable for export to Microsoft Excel or other spreadsheet programs. This is also the most easily human-readable format.

### Format Examples:

> **Send the data back using JSON**
> 
> format=json
> 

# Sample Output

 Sample JSON Output

```yaml
{
    {
    "metadata": {
        "id": "0100",
        "name": "Oxford MD",
        "lat": "38.693211",
        "lon": "-76.174249"
    },
    "data": [
        {
            "t": "2019-10-23 00:00:00",
            "v": "0.895"
        },
        {
            "t": "2019-10-23 00:06:00",
            "v": "0.911"
        }
    ]
}}
```


Sample XML Output

```yaml
 <?xml version="1.0" encoding="UTF-8" ?> 
    <data>
    <metadata id="0100" name="Oxford MD" lat="38.693211" lon="-76.174249" /> 
    <observations>
        <wl t="2019-10-23 00:00:00" v="0.895" />
        <wl t="2019-10-23 00:06:00" v="0.911" />
    </observations>
    </data>
```
 Sample CSV Output

```yaml
Station ID: 0100
Name: Oxford MD
Latitude: 38.693211
Longitude: -76.174249
2019-10-23 00:00:00,0.895
2019-10-23 00:06:00,0.911
2019-10-23 00:12:00,0.932
2019-10-23 00:18:00,0.947
2019-10-23 00:24:00,0.96
```