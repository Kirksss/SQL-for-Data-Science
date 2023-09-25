# SQL-for-Data-Science
Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
	i. 	Attribute table =			10000
	ii. 	Business table =		10000
	iii. 	Category table =		10000
	iv. 	Checkin table =			10000
	v. 	elite_years table =			10000
	vi. 	friend table = 			10000
	vii. 	hours table =			10000
	viii. 	photo table = 			10000
	ix. 	review table = 			10000
	x. 	tip table = 				10000
	xi. 	user table =			10000
	


2. Find the total number of distinct records for each of the keys listed below:

	i. 		Business =			10000 	(id)
	ii. 	Hours =				1562 	(business_id)
	iii. 	Category =			2643    (business_id)
	iv. 	Attribute =			1115	(business_id)
	v. 		Review =			10000	(id),		8090 (business_id), 	9581 (user_id)
	vi. 	Checkin = 			493 	(business_id)
	vii. 	Photo =				10000	(id),		6493 (business_id)
	viii. 	Tip = 				537		(user_id),  3979 (business_id)
	ix. 	User = 				10000	(id)
	x. 		Friend = 			11		(user_id)
	xi. 	Elite_years =	    2780	(user_id)
	


3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: No
	
	
	SQL code used to arrive at answer:
		SELECT *
		FROM  user
		WHERE 	id is null OR
				name is null OR
				review_count is null OR
				yelping_since is null OR
				useful is null OR
				funny is null OR
				cool is null OR
				fans is null OR
				average_stars is null OR
				compliment_hot is null OR
				compliment_more is null OR
				compliment_profile is null OR
				compliment_cute is null OR
				compliment_list is null OR
				compliment_note is null OR
				compliment_plain is null OR
				compliment_cool is null OR
				compliment_funny is null OR
				compliment_writer is null OR
				compliment_photos is null;
	

	
4. Find the minimum, maximum, and average value for the following fields:

	i. Table: Review, Column: Stars
		min: 1		max: 5		avg: 3.7082
		
	ii. Table: Business, Column: Stars
		min: 1.0	max: 5.0	avg: 3.6549
	
	iii. Table: Tip, Column: Likes
		min: 0		max: 2		avg: 0.0144
	
	iv. Table: Checkin, Column: Count
		min: 1		max: 53		avg: 1.9414
	
	v. Table: User, Column: Review_count
		min: 0		max: 2000	avg: 24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
		SELECT city AS 'City'
		, SUM(review_count) AS 'Total_Reviews'
		FROM business
		GROUP BY city
		ORDER BY SUM(review_count) DESC;
	
	Copy and Paste the Result Below:
		+-----------------+---------------+
		| City            | Total_Reviews |
		+-----------------+---------------+
		| Las Vegas       |         82854 |
		| Phoenix         |         34503 |
		| Toronto         |         24113 |
		| Scottsdale      |         20614 |
		| Charlotte       |         12523 |
		| Henderson       |         10871 |
		| Tempe           |         10504 |
		| Pittsburgh      |          9798 |
		| Montréal        |          9448 |
		| Chandler        |          8112 |
		| Mesa            |          6875 |
		| Gilbert         |          6380 |
		| Cleveland       |          5593 |
		| Madison         |          5265 |
		| Glendale        |          4406 |
		| Mississauga     |          3814 |
		| Edinburgh       |          2792 |
		| Peoria          |          2624 |
		| North Las Vegas |          2438 |
		| Markham         |          2352 |
		| Champaign       |          2029 |
		| Stuttgart       |          1849 |
		| Surprise        |          1520 |
		| Lakewood        |          1465 |
		| Goodyear        |          1155 |
		+-----------------+---------------+
	(Output limit exceeded, 25 of 362 total rows shown)

	
6. Find the distribution of star ratings to the business in the following cities:

	i. Avon
	
		SQL code used to arrive at answer:
			SELECT stars AS 'Star Rating'
			, COUNT(stars) AS 'Count'
			FROM business b
			WHERE city = 'Avon'
			GROUP BY stars;
		
		Copy and Paste the Resulting Table Below (2 columns - star rating and count):
			+-------------+-------+
			| Star Rating | Count |
			+-------------+-------+
			|         1.5 |     1 |
			|         2.5 |     2 |
			|         3.5 |     3 |
			|         4.0 |     2 |
			|         4.5 |     1 |
			|         5.0 |     1 |
			+-------------+-------+
	
	
	ii. Beachwood

		SQL code used to arrive at answer:
			SELECT stars AS 'Star Rating'
			, COUNT(stars) AS 'Count'
			FROM business b
			WHERE city = 'Beachwood'
			GROUP BY stars;
		
		Copy and Paste the Resulting Table Below (2 columns - star rating and count):
			+-------------+-------+
			| Star Rating | Count |
			+-------------+-------+
			|         2.0 |     1 |
			|         2.5 |     1 |
			|         3.0 |     2 |
			|         3.5 |     2 |
			|         4.0 |     1 |
			|         4.5 |     2 |
			|         5.0 |     5 |
			+-------------+-------+


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
		SELECT name
		, review_count
		FROM user
		ORDER BY review_count DESC
		LIMIT 3;
		
	Copy and Paste the Result Below:
		+--------+--------------+
		| name   | review_count |
		+--------+--------------+
		| Gerald |         2000 |
		| Sara   |         1629 |
		| Yuri   |         1339 |
		+--------+--------------+


8. Does posing more reviews correlate with more fans?
		- No
		
	Please explain your findings and interpretation of the results:
		
		SQL code used to arrive at answer:
			SELECT name
			, review_count
			, fans
			FROM user
			ORDER BY fans desc
			LIMIT 10;
		
		Results:
			+-----------+--------------+------+
			| name      | review_count | fans |
			+-----------+--------------+------+
			| Amy       |          609 |  503 |
			| Mimi      |          968 |  497 |
			| Harald    |         1153 |  311 |
			| Gerald    |         2000 |  253 |
			| Christine |          930 |  173 |
			| Lisa      |          813 |  159 |
			| Cat       |          377 |  133 |
			| William   |         1215 |  126 |
			| Fran      |          862 |  124 |
			| Lissa     |          834 |  120 |
			+-----------+--------------+------+
			
		Interpretation:
		The above table shows the number of fans sorted in the descending order and it can be seen that depite having the second to the last number of reviews, 'Amy' has themost fans. There is also no particular pattern observed in the review_count column so it can be concluded that there is no correlation between the two columns. Further assumptions based on the correlation based on content and other criteria between the number of reviews and fans, however, requires additional investigation.
	
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: more reviews with the word "love"

	
	SQL code used to arrive at answer:
		SELECT (SELECT COUNT(text)
		FROM review
		WHERE text LIKE "%love%") AS  'Love_text', 

			(SELECT COUNT(text) 
			FROM review
			WHERE text LIKE "%hate%") AS 'Hate_text';
		
		
		Results:
		+-----------+-----------+
		| Love_text | Hate_text |
		+-----------+-----------+
		|      1780 |       232 |
		+-----------+-----------+
	
	
		OR:
		
		SELECT 'love' Word 
		, COUNT(text) AS  'Total Count'
		FROM review
		WHERE text LIKE '%love%'
		UNION
		SELECT 'hate' Word
		, COUNT(text) AS 'Total Count'
		FROM review
		WHERE text LIKE '%hate%';
		
		+------+-------------+
		| Word | Total Count |
		+------+-------------+
		| hate |         232 |
		| love |        1780 |
		+------+-------------+
	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
		SELECT name
		, fans
		FROM user
		ORDER BY fans DESC
		LIMIT 10;
	
	Copy and Paste the Result Below:
		+-----------+------+
		| name      | fans |
		+-----------+------+
		| Amy       |  503 |
		| Mimi      |  497 |
		| Harald    |  311 |
		| Gerald    |  253 |
		| Christine |  173 |
		| Lisa      |  159 |
		| Cat       |  133 |
		| William   |  126 |
		| Fran      |  124 |
		| Lissa     |  120 |
		+-----------+------+
	
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

	- I have chosen city = Las Vegas and category = Shopping.
	
i. Do the two groups you chose to analyze have a different distribution of hours?

	SQL code used to arrive at answer:
		SELECT stars
		, COUNT(DISTINCT id) AS 'number_of_shopping_centers'
		, COUNT(hours) AS 'number_of_opening_days'
		, COUNT(hours)/COUNT(DISTINCT id) AS 'avg_opening_days'
		, SUM(review_count) AS 'total_reviews'
		FROM business b JOIN hours h
		ON b.id = h.business_id
		JOIN Category c
		ON c.business_id = b.id
		WHERE city = 'Las Vegas' AND category = 'Shopping'
		GROUP BY stars;

	Results:
	+-------+----------------------------+------------------------+------------------+---------------+
	| stars | number_of_shopping_centers | number_of_opening_days | avg_opening_days | total_reviews |
	+-------+----------------------------+------------------------+------------------+---------------+
	|   2.5 |                          1 |                      7 |                7 |            42 |
	|   3.5 |                          1 |                      6 |                6 |            66 |
	|   4.5 |                          1 |                      7 |                7 |           224 |
	|   5.0 |                          1 |                      5 |                5 |            20 |
	+-------+----------------------------+------------------------+------------------+---------------+

ii. Do the two groups you chose to analyze have a different number of reviews?
    
	- Yes, the two groups have different number of reviews with the 4-5 star businesses having more.    
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

	SQL code used for analysis:
		SELECT stars
		, neighborhood
		, address
		, postal_code
		FROM business b JOIN Category c
		ON c.business_id = b.id
		WHERE city = 'Las Vegas' AND category = 'Shopping'
		ORDER BY stars;
		
	Results:
	+-------+--------------+-----------------------------+-------------+
	| stars | neighborhood | address                     | postal_code |
	+-------+--------------+-----------------------------+-------------+
	|   2.5 | Eastside     | 3808 E Tropicana Ave        | 89121       |
	|   3.5 | Southeast    | 3421 E Tropicana Ave, Ste I | 89121       |
	|   4.5 |              | 1000 Scenic Loop Dr         | 89161       |
	|   5.0 |              | 3555 W Reno Ave, Ste F      | 89118       |
	+-------+--------------+-----------------------------+-------------+
	
	
	Based on the results above, it can be inferred that most shopping centers in the first group (2 to 3 stars) are located in Tropicana Avenue and therefore are in the same vicinity as opposed  to the locations of the second group that have no visible correlation.
	
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
    
	- There are more open businesses than closed ones, however, there is only a small difference in the average no. of stars between the two groups.    
         
ii. Difference 2:
	
	- There is a quantitative difference in the number of total reviews between the closed businesses and open business.
	
	SQL code used for analysis:
		SELECT is_open AS 'Open_Businesses'
		, COUNT(DISTINCT id) AS 'Total_Businesses' 
		, AVG(stars) AS 'Avg_Stars'
		, SUM(review_count) AS 'Total_Reviews'
		FROM business 
		GROUP BY is_open;

	+-----------------+------------------+-------------------+---------------+
	| Open_Businesses | Total_Businesses |         Avg_Stars | Total_Reviews |
	+-----------------+------------------+-------------------+---------------+
	|               0 |             1520 | 3.520394736842105 |         35261 |
	|               1 |             8480 | 3.679009433962264 |        269300 |
	+-----------------+------------------+-------------------+---------------+   
         

	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
    - Which city offers the best service based on restaurant establishments?
	
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
    
	- For the category of restaurants across all cities included in the database, I have determined the total number of businesses, the total number of functioning businesses, the average star rating, and the total number of review counts. As shown in the table below, the City of Mesa has 2 businesses that garnered the most average stars, however, one business later closed down. The cities of Scottsdale and Madison, both with an average of 4 stars suffered from the same conclusion of having their sole restaurants closing down.
                  
iii. Output of your finished dataset:
         
	+-------------------+------------------+-----------+---------------+-----------------------+
	| City              | No_of_Businesses | AVG_Stars | Total_Reviews | No_of_Open_Businesses |
	+-------------------+------------------+-----------+---------------+-----------------------+
	| Mesa              |                2 |       4.5 |           396 |                     1 |
	| Charlotte         |                2 |      4.25 |            11 |                     1 |
	| Cleveland         |                2 |       4.0 |           423 |                     1 |
	| Westlake          |                1 |       4.0 |           105 |                     1 |
	| Medina            |                1 |       4.0 |            94 |                     1 |
	| Cuyahoga Falls    |                1 |       4.0 |            55 |                     1 |
	| Oakville          |                1 |       4.0 |            55 |                     1 |
	| Middleton         |                1 |       4.0 |            37 |                     1 |
	| Chesterland       |                1 |       4.0 |            30 |                     1 |
	| Tolleson          |                1 |       4.0 |            23 |                     1 |
	| Brampton          |                1 |       4.0 |            10 |                     1 |
	| Scottsdale        |                1 |       4.0 |            91 |                     0 |
	| Madison           |                1 |       4.0 |             4 |                     0 |
	| Las Vegas         |                4 |     3.875 |          1062 |                     2 |
	| Phoenix           |                6 |       3.5 |           757 |                     5 |
	| Mississauga       |                4 |       3.5 |           160 |                     4 |
	| Edinburgh         |                3 |       3.5 |            44 |                     2 |
	| Sun Prairie       |                1 |       3.5 |            87 |                     1 |
	| Litchfield Park   |                1 |       3.5 |            83 |                     1 |
	| Fitchburg         |                1 |       3.5 |            74 |                     1 |
	| Aurora            |                1 |       3.5 |            32 |                     1 |
	| Sheffield Village |                1 |       3.5 |            27 |                     1 |
	| Fountain Hills    |                1 |       3.5 |            21 |                     1 |
	| Verdun            |                1 |       3.5 |            11 |                     1 |
	| Inverness         |                1 |       3.5 |             3 |                     1 |
	+-------------------+------------------+-----------+---------------+-----------------------+
	(Output limit exceeded, 25 of 43 total rows shown)	 
         
iv. Provide the SQL code you used to create your final dataset:

	SELECT city AS 'City'
	, COUNT(DISTINCT id) AS 'No_of_Businesses'
	, AVG(stars) AS 'AVG_Stars'
	, SUM(review_count) AS 'Total_Reviews'
	, SUM(is_open) AS 'No_of_Open_Businesses'
	FROM business JOIN category
	ON id = business_id
	WHERE category = 'Restaurants' 
	GROUP BY city
	ORDER BY AVG(stars) DESC, SUM(is_open) DESC, SUM(review_count) DESC;
