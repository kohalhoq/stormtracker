# stormtracker
DROP VIEW IF EXISTS cost_per_state;
CREATE VIEW cost_per_state AS
	SELECT state_name, 
    CONCAT('$', FORMAT (sum(monetary_damages), 'C')) AS 'Total Damages Per State', 
    CONCAT('$', FORMAT(sum(monetary_damages)/count(storm_id),'C')) AS 'Average Damage Cost per Storm (USD)'
	FROM states
		JOIN location USING (state_id)
			JOIN description USING (location_id)
				JOIN damages USING (damages_id)
	GROUP BY state_name;

DROP VIEW IF EXISTS count_by_state; 
CREATE VIEW count_by_state AS
	SELECT state_name, count(storm_id)
	FROM states
		JOIN location USING (state_id)
			JOIN description USING (location_id)
	GROUP BY state_name;
    
DROP VIEW IF EXISTS deaths;
CREATE VIEW deaths AS 
	SELECT deaths, storm_id, storm_type
	FROM damages
		JOIN storm_description USING (damages_id) 
    	WHERE deaths > 25
    	ORDER BY deaths;
        
DROP VIEW IF EXISTS larger_than_avg;     
CREATE VIEW larger_than_avg AS 
	SELECT storm_id, size
	FROM storm_description
		JOIN strength USING (strength_id)
	WHERE size > (SELECT AVG(size) FROM strength);

DROP VIEW IF EXISTS more_damage;
CREATE VIEW more_damage AS 
	SELECT storm_id, storm_type, monetary_damages
    	FROM storm_description 
		JOIN damages USING (damages_id)
	WHERE monetary_damages > 3000
   	 ORDER BY monetary_damages;
     
DROP VIEW IF EXISTS storms_in_states; 
CREATE VIEW storms_in_states AS 
SELECT storm_id, state_name, storm_type 
FROM states
	JOIN location USING (state_id)
		JOIN storm_description USING (location_id);

DROP VIEW IF EXISTS storm_types;
CREATE VIEW storm_types AS
	SELECT satellite_id, storm_type
	FROM satellites
		JOIN storm_description USING (satellite_id);

	



