# Challenge 9 - Temperature Analysis for SurfsUp

## Overview of the Analysis
W.Avy wants temperature data for the months of June and December in Oahu, in order to determine if the surf and ice cream shop business is sustainable year-round.We will sort the data and perform the analysis to get the answers.From the hawaii.sqlite database we have filtered the Measurements table to retrieve the temperatures for the month of June and December.
In this Challenege we have used the following softwares.
Python version 3.7.7
Pandas functions and methods
SQLAlchemy
VS code  version 1.51.1
Jupyter notebook version 6.0.3


## Results
### 1. The minimum temperature for june is 64 and for December it is 56. The June weather looks more favorable for the business. 


### 2. The max temperature for june is 85 and for December it is 83. This does not look like a huge difference and December can also be considered as a fair season for the business.

  
### 3. The inter quartile range for June is 73 to 77 with a mean of 74.94 while the inter quartile range for December is 69 to 74 with a mean od 71.04 .
Looking at the overall statistics for the month of June, it is a good warm month for surf and ice cream while December looks little cold and may be challenging for the surf and ice cream business.

## Summary
### Analysis for the June and December temperature data.
The data from SQLite is imported to pandas DataFrame and this lets us access the data to get the statistical information for the analysis. Using the describe() method we get the statistical data like mean,std,min,25%,50%,75%,max and we can suggest that June looks like a nice warm month and is perfect for the surf and ice cream business.

The following steps explain how the data is accessed,filtered and visualized.
1. The dependencies imported are
```
	import numpy as np
	import pandas as pd
	# Python SQL toolkit and Object Relational Mapper
	import sqlalchemy
	from sqlalchemy.ext.automap import automap_base
	from sqlalchemy.orm import Session
	from sqlalchemy import create_engine, func
	from sqlalchemy import extract
 ```

2. create engine function - this lets us query a SQLite database.
```
	engine = create_engine("sqlite:///hawaii.sqlite") ```

3. automap_base() function - to reflect our existing database in SQLite into a new model.
```
	Base = automap_base() ```

4. prepare() function - reflect the schema of our SQLite tables into our code and create mappings.
```
	Base.prepare(engine, reflect=True) ```

5. Reference the measurement and station classes by assigning variables measurement and station.
``` 
	Measurement = Base.classes.measurement
	Station = Base.classes.station ```

6. Use an SQLAlchemy Session to query our database.
``` 	session = Session(engine) ```

7. Using session.query we can now get the june and December temperatures from the SQLite database and save it to a variable.

8. We then covert this data to a list.

9. Next we convert the data to a pandas DataFrame so we can perform functions and use statistical models.

10. Using describe() method we can now get the interquartile range.

### Additional query 1 - Precipitation data for the month of June.
We have the query data saved in a variable called precipitation_june, then we convert this variable to a list named precipitation_june_list and finally convert this list to a pandas DataFrame called precipitation_june_df to get statistical and visulaziation data.
```
precipitation_june = session.query(Measurement.prcp).filter(extract('month', Measurement.date) == 6)
precipitation_june_list =[]
for p in precipitation_june :
   precipitation_june_list.append(p)
#print(precipitation_june_list)
precipitation_june_df = pd.DataFrame(precipitation_june_list)
precipitation_june_df.describe()
```
[June precipitation graph][1]

### Additional query 2 - Precipitation data for the month of December
We have the query data saved in a variable called precipitation_dec, then we convert this variable to a list named precipitation_dec_list and finally convert this list to a pandas DataFrame called precipitation_dec_df to get statistical and visulaziation data
```
precipitation_dec = session.query(Measurement.prcp).filter(extract('month', Measurement.date) == 12)
precipitation_dec_list =[]
for p in precipitation_dec :
   precipitation_dec_list.append(p)
#print(precipitation_june_list)
precipitation_dec_df = pd.DataFrame(precipitation_dec_list)
precipitation_dec_df.describe()

```
[December precipitation graph][2]