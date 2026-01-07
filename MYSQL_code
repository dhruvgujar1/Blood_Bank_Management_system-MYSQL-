select * from donors;
select * from donations;
select * from hospitals;
select * from inventory;
select * from recipients;
select * from inventory;
select * from requests;


-- How many blood units are currently available for each blood group and component?
select blood_group,component,count(units) from donations group by blood_group,component;

-- Are there any blood groups (including rare groups like A2, A2B, hh) that are critically low in stock?
select 
    d.blood_group,count(*) from donations d join inventory i on d.donation_id=i.donation_id 
       where d.blood_group in ("A2","A2B","hh")
       and
       i.status="Available" group by d.blood_group ;


-- How many blood units have expired and how many are nearing expiry (within the next 7 days)?
select 
    d.blood_group ,count(*) as Expired_unit  from donations d 
        join inventory i on d.donation_id=i.donation_id 
    where
    i.status="Expired" group by d.blood_group;


-- What percentage of the total inventory is available, issued, expired, or quarantined?

select 
    status,count(*)/(select count(*) from inventory)*100
as percentage from inventory group by status;


-- How many blood donations failed the quality tests?
select count(*) from donations where test_status="Contaminated";


-- What are the most common reasons for blood contamination?
select 
   test_details as Most_common_reason from donations 
   where test_status="Contaminated"  group by test_details limit 1;


-- What proportion of total donations are marked as contaminated or pending testing?
select 
    round(count(*)*100.0/(select count(*) from donations),2) as Donation_propotion 
from donations where test_status in ("Contaminated" ,"Pending");


-- Are there donors whose donations repeatedly fail quality tests?
select 
    full_name, count(test_status) as Failing_count from donors a 
    left join donations b on a.donor_id=b.donor_id 
    where b.test_status="Contaminated" group by full_name 
    order by count(test_status) desc limit 3;


-- Which hospitals request the highest number of blood units?
select 
     h.name  as hospital_name,sum(r.required_units) as required_units 
     from hospitals h join requests r on h.hospital_id=r.hospital_id 
     group by h.name order by count(r.required_units) desc limit 1 ;
     
select * from requests;


-- Which blood groups are most frequently requested by hospitals?
select 
     required_blood_group,count(required_blood_group) as Required_unit from requests
     group  by required_blood_group order by count(required_blood_group) desc limit 1;


-- What is the average number of units requested per hospital request?
SELECT 
     ROUND(AVG(required_units), 2) AS avg_units_per_request FROM requests;


-- Are hospitals requesting blood that is currently unavailable?
SELECT 
    r.request_id,
    h.name AS hospital_name,
    r.required_blood_group,
    r.required_units,
    COUNT(i.inventory_id) AS available_units
FROM requests r
JOIN hospitals h 
    ON r.hospital_id = h.hospital_id
LEFT JOIN donations d 
    ON d.blood_group = r.required_blood_group
LEFT JOIN inventory i 
    ON d.donation_id = i.donation_id
    AND i.status = 'Available'
WHERE r.status = 'Open'
GROUP BY 
    r.request_id,
    h.name,
    r.required_blood_group,
    r.required_units
HAVING available_units < r.required_units;

 select * from donors;
select * from donations;
select * from hospitals;
select * from inventory;
select * from recipients;
select * from inventory;
select * from requests;

-- Who are the top donors based on donation frequency?
select  
    full_name,count(*) as Donation_frequency from donors a 
join donations b on a.donor_id=b.donor_id group by a.full_name
order by count(*) desc limit 5;

-- How many active vs inactive donors are registered in the system?
select 
   is_active,count(*) as count from donors group by is_active;


-- How many donors have recorded medical conditions? 
SELECT 
   count(*) as Donars_cout
FROM donors 
WHERE known_conditions IS NOT NULL
  AND known_conditions <> 'None'
  AND known_conditions <> '' ;
  
  --   Which hospitals request the highest number of blood units?
   select
      h.name as Hospital_name ,count(*) as Required_units
  from hospitals h join requests r 
  on h.hospital_id=r.hospital_id group by h.name
  order by  
  count(*) desc limit 1;
  
  -- Which blood groups are most frequently requested by hospitals
  
  
  select 
     r.required_blood_group,count(*) as required_unit from hospitals h join requests r 
     on h.hospital_id=r.hospital_id group by r.required_blood_group
  order by count(*) desc limit 5;
  

--   What is the average number of units requested per hospital request?
select round(AVG(required_units),2) as Avg_unit_requested from requests;


-- What percentage of blood requests are fulfilled, open, or cancelled?
select 
  round(count(*)*100.0/(select count(*) from requests),2)
  as Percentage_of_Fullfilled_requests from requests where status="Fulfilled";
 

select 
   round(count(*)*100.0/(select count(*) from requests),2)
 as Percentage_of_open_requests from requests where status="Open";
 

select 
    round(count(*)*100.0/(select count(*) from requests),2)
	as Percentage_of_cancelled_requests from requests where status="cancelled";
 

--  Which blood groups have the highest number of unfulfilled requests?
 select 
      required_blood_group,count(*)as unfullfilled_count from requests
      where status="cancelled" group by required_blood_group 
	  order by count(*) desc limit 5;--  For open requests, is sufficient compatible blood currently available?
SELECT 
    r.request_id,
    h.name AS hospital_name,
    r.required_blood_group,
    r.required_units,
    COUNT(i.inventory_id) AS available_units,
    CASE 
        WHEN COUNT(i.inventory_id) >= r.required_units 
        THEN 'Sufficient'
        ELSE 'Insufficient'
    END AS availability_status
FROM requests r
JOIN hospitals h 
    ON r.hospital_id = h.hospital_id
LEFT JOIN donations d 
    ON d.blood_group = r.required_blood_group
LEFT JOIN inventory i 
    ON d.donation_id = i.donation_id
    AND i.status = 'Available'
WHERE r.status = 'Open'
GROUP BY r.request_id, h.name, r.required_blood_group, r.required_units;


-- How do blood donations vary month-wise?
SELECT 
    MONTH(donation_date) AS donation_month,
    COUNT(*) AS total_donations
FROM donations
GROUP BY MONTH(donation_date)
ORDER BY donation_month;


-- Is there a seasonal pattern in blood donation or blood demand?
select 
month(request_date) as donation_month,
sum(required_units) as total_donation from requests
GROUP BY MONTH(request_date)
ORDER BY donation_month;

select * from donations;


-- How has inventory availability changed over time?
select 
month(last_updated) as  month,count(status="Available")  as availability from 
inventory group by month(last_updated) order by month(last_updated);


-- Are rare blood groups donated less frequently compared to common groups?
SELECT
	case
		when blood_group in ("A2B","A2","hh")
		then 'rare'
        else 'Common'
        end as Blood_group_type,
        count(*) as donation 
        from donations
        group by Blood_group_type
        order by donation ;
        
        
select * from donors;
select * from donations;
select * from hospitals;
select * from inventory;
select * from recipients;
select * from inventory;
select * from requests;



-- Which blood groups require urgent donor drives?

SELECT 
    r.required_blood_group,
    SUM(r.required_units) AS total_units_requested,
    COUNT(i.inventory_id) AS available_units
FROM requests r
LEFT JOIN donations d
    ON d.blood_group = r.required_blood_group
LEFT JOIN inventory i
    ON d.donation_id = i.donation_id
    AND i.status = 'Available'
GROUP BY r.required_blood_group
HAVING available_units < total_units_requested
ORDER BY (total_units_requested - available_units) DESC;


-- Which hospitals should be prioritized based on demand and shortage?
SELECT 
    h.name AS hospital_name,
    SUM(r.required_units) AS total_units_requested,
    COUNT(i.inventory_id) AS available_units,
    (SUM(r.required_units) - COUNT(i.inventory_id)) AS shortage_units
FROM hospitals h
JOIN requests r
    ON h.hospital_id = r.hospital_id
LEFT JOIN donations d
    ON d.blood_group = r.required_blood_group
LEFT JOIN inventory i
    ON d.donation_id = i.donation_id
    AND i.status = 'Available'
WHERE r.status = 'Open'
GROUP BY h.hospital_id, h.name
HAVING shortage_units > 0
ORDER BY shortage_units DESC;
