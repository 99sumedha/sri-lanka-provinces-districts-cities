# Sri Lanka Provinces Districts Cities Database ##


### About



This is a MySQL version of Sri Lankan Provinces => Districts => Cities related data.

There are three SQL files,
 1. provinces.sql (Names of nine provinces)
 2. districts.sql (All districts related to each province)
 3. cities.sql (All cities related to each district)

###Statistics

*  Provinces - 9
*  Districts - 25
*  Cities - 1836

###Sample tables structure with data


**Provinces**

| id  | name |
| --- | ------- |
| 1   | Western |
| 2   | Central |


**Districts**

| id  | province_id| name         |
| --- | ---------- | ------------ |
| 1   | 6          | Ampara       |
| 2   | 8          | Anuradhapura |


**Cities**

| id  | district_id | name          | postcode | latitude | longitude |
| --- | ----------- | ------------- | -------- | -------- | --------- |
| 1   | 1           | Akkaraipattu  | 32400    | 7.2167   | 81.85     |
| 2   | 1           | Ambagahawatta | 90326    | 7.4      | 81.3      |



### MySQL Usage


**Advantages of latitude and longitude**

* Integrate with google map or any map related service to show exact place of the city in the map.
* Find locations are within a certain radius distance of a given latitude/longitude.


Here's the SQL statement that will find the closest locations that are within a radius of 25 kilometers to the 7.358849, 81.280133 coordinate. It calculates the distance based on the latitude/longitude of that row and the target latitude/longitude, and then asks for only rows where the distance value is less than 25, orders the whole query by distance.

```SQL
SELECT id, name, (6371 * ACOS(COS(RADIANS(7.358849)) * COS(RADIANS(latitude)) * COS(RADIANS(longitude) - RADIANS(81.280133)) + SIN(RADIANS(7.358849)) * SIN(RADIANS(latitude)))) AS distance
FROM cities
HAVING distance < 25
ORDER BY distance
```


### Note


* This free database dose not guarantee for the complete list of cities in Sri Lanka.
* You can manually change the spelling mistakes or add edit any records, which are not correct.
