# neo4j-crime-visualization

## Links
[Blog Post](https://cambridge-intelligence.com/visualizing-crime-patterns-data-graph/?mkt_tok=eyJpIjoiTkRBME1XWXhaVFF4Tm1RMiIsInQiOiJJdlZsQ0NENHdhdFVvQlI5alB5ZzZYVHloUVN3RmRkeGdRRkFcLzJ1ZTRtdEJiWVZ6c0p1M201emJBMU4yVDcwUDRxQmRCNHc5eW9VeFhtWEo3VTFMY3Q0UDVFZ3d6bEthSFFlOElnNCtJSUozZHBzUUJMN0wzUkNnQ0s4dzE4QXEifQ%3D%3D)

## Install
* Install neo4j
* Install [neo4j awesome procedures on Cyper](https://github.com/neo4j-contrib/neo4j-apoc-procedures)
* Make sure plugin version matches [version of neo4j](https://github.com/neo4j-contrib/neo4j-apoc-procedures#version-compatibility-matrix)

Corrected query
```
CALL apoc.load.json('https://data.cityofboston.gov/resource/29yf-ye7n.json?$limit=1000&$offset=0')
	YIELD value AS crime
	MERGE (c:Crime {incidentnum: crime.incident_number})
	ON CREATE SET	c.offense=crime.offense_code_group, 
					c.date=crime.occured_on_date, c.district=crime.district, 
					c.latitude=crime.lat, c.longitude=crime.long
	MERGE (desc:Description {name: crime.offense_code_group})
	CREATE (c)-[:HAS_DESCRIPTION]->(desc);
```
