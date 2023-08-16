# revising-aggregations-the-count-function
Query a count of the number of cities in CITY having a Population larger than 100000.

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)  

	select count(population) from city where population > 100000;

 # revising-aggregations-the-sum
 Query the total population of all cities in CITY where District is California.

	select sum(population) from city where District = 'California';

 # revising-aggregations-the-avg
 Query the average population of all cities in CITY where District is California.

	select avg(population) from city where District = 'California';

 # revising-aggregations-the-avg-round
Query the average population for all cities in CITY, rounded down to the nearest integer.

	select (round(avg(population),-0.5)) from city ;

# Japan Population 
 Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

	select sum(population) from city where countrycode = 'JPN';

 # Population Density Difference  
  
Query the difference between the maximum and minimum populations in CITY.  
  
	SELECT (MAX(population) - MIN(population)) FROM city;
  
# The Blunder  
  
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.  
Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries), and round it up to the next integer.  
  
***Input Format***  
The EMPLOYEES table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12893/1443817108-adc2235c81-1.png)  
  
***Note:*** Salary is measured in dollars per month and its value is < 10^5.  
  
	SELECT CEIL(AVG(salary) - AVG(REPLACE(salary, '0', ''))) FROM employees;
  
  
  
# Top Earners  
  
We define an employee's total earnings to be their monthly salary*months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2-space-separated integers.  
  
***Input Format***  
The Employee table containing employee data for a company is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)  
  
where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.  
  
	SELECT * FROM (SELECT  months*salary, COUNT(*) FROM employee GROUP BY months*salary ORDER BY months*salary DESC) WHERE ROWNUM = 1;
  
  






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
