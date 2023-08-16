# Weather Observation Station 18  
  
Consider P1(a,b) and P2(c,d) to be two points on a 2D plane.  
a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).  
b happens to equal the minimum value in Western Longitude (LONG_W in STATION).  
c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).  
d happens to equal the maximum value in Western Longitude (LONG_W in STATION).  
  
Query the [Manhattan Distance](https://xlinux.nist.gov/dads/HTML/manhattanDistance.html) between points P1 and P2 and round it to a scale of 4 decimal places.  

	SELECT ROUND(MAX(Lat_N) - MIN(Lat_N) + MAX(Long_W) - MIN(Long_W), 4)
	FROM Station;
# Weather Observation Station 19  
  
Consider P1(a,c) and P2(b,d) to be two points on a 2D plane.   
(a,b) - the respective minimum and maximum values of Northern Latitude (LAT_N)  
(c,d) - the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.  
  
Query the [Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance) between points P1 and P2 and format your answer to display 4 decimal digits.  

  	select round (sqrt (power(max(lat_n) - min(lat_n),2)+ power(max(long_w) - min(long_w),2)),4) from station;

# Weather Observation Station 19  

A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4  decimal places.

 	SELECT LAT_N FROM (SELECT ROUND(LAT_N, 4) AS LAT_N,
            ROW_NUMBER() OVER (ORDER BY LAT_N) AS RN,
            (SELECT ROUND(ABS(COUNT(LAT_N)/2),0) FROM STATION) AS MID FROM STATION) IQ WHERE RN = MID ;
