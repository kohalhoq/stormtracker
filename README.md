# stormtracker

Logical Design
For our logical design we have 8 tables and 7 views. 
The tables are interconnected with foreign keys and are serving our purpose to see how storms are connected or can be differentiated from states or storm types, etc.
All our tables have 3 or more columns and at least 15 data inside each table. 
The table Description is connected by foreign keys to Location, Date, Strength, Damages and satellites tables with their primary keys allowing them to be 
dependent on these tables. Likewise the table states are connected with cities as well as location by its primary key. 
These description, cities and location tables rely on its depending tables allowing these tables to have similar values from their depending tables. 

Views 
We’ve included 7 views which contain queries to answer various questions about the storms contained in our data. 
1. cost_per_state: This view contains the total monetary damages by all storms in each area: DC, Maryland, and Virginia. This is done using 3 JOIN statements. 
2. count_by_state: This view counts the amount of storms and organizes them by state. It contains a column for the total storm count in each of the states included in our data. Two JOINs are used along with the aggregation function count().
3. deaths: The deaths view selects storms where the death count is greater than 25. It selects the death count for each storm and displays it alongside the storm’s ID number and the storm’s type. A JOIN and WHERE statement are used in the query.
4. larger_than_avg: This view displays the storm ID and size storms that have a larger size than the average of all the storms. In this query, a subquery with and avg() function is used to select the average size of all the storms. This value is then used in a WHERE statement to select the storm IDs and sizes of storms higher than it.
5. more_damage: This displays the storm IDs and types of the storms that have caused more than 3000 dollars of monetary damages. This is done using a JOIN and WHERE statement.
6. storms_in_states: This view displays all storms by storm ID alongside the state they occurred in and the type of the storm. Two JOINs are used in this query.
7. storm_types: This view selects all satellite IDs and displays then along with the storm type that they have monitored. This is done using a JOIN statement.
