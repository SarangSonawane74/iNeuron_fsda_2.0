SELECT * FROM SALES;

ALTER TABLE SALES
DROP COLUMN ORDER_EXTRACT ;

--Create a new column called order_extract and extract the number after the last ‘–‘ from Order ID column.
UPDATE SALES
SET ORDER_EXTRACT= SUBSTRING(ORDER_ID,9,5);
SELECT * FROM SALES;

--Create a new column called Discount Flag and categorize it based on discount.Use ‘Yes’ if the discount is greater than zero else ‘No’.

SELECT *,
CASE
    WHEN DISCOUNT >0 THEN 'YES'
    ELSE 'NO'
    END AS DISCOUNT_FLAG
    FROM SALES;

--Create a new column called process days and calculate how many days it takes for each order id to process from the order to its shipment.    
ALTER TABLE SALES
ADD COLUMN PROCESS_DAYS INT;

UPDATE SALES
SET PROCESS_DAYS=DATEDIFF(DAYS,ORDER_DATE,SHIP_DATE);
SELECT * FROM SALES;

--Create a new column called Rating and then based on the Process dates give rating like given below.
--a. If process days less than or equal to 3days then rating should be 5
--b. If process days are greater than 3 and less than or equal to 6 then rating should be 4
--c. If process days are greater than 6 and less than or equal to 10 then rating should be 3
--d. If process days are greater than 10 then the rating should be 2.

ALTER TABLE SALES
ADD COLUMN RATING INT ;

SELECT *,
CASE
    WHEN PROCESS_DAYS <= 3 THEN 5
    WHEN PROCESS_DAYS >= 3 AND PROCESS_DAYS <= 6 THEN 4
    WHEN PROCESS_DAYS >= 6 AND PROCESS_DAYS <=10 THEN 3
    WHEN PROCESS_DAYS > 10 THEN 2
    ELSE 1
    END AS RATING
    FROM SALES;
    
