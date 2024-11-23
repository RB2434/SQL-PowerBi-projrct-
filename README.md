

---

# **Ola Data Analyst Project**

### **Dashboard Link**:https://app.powerbi.com/groups/me/reports/c854e2e1-7007-44ef-96bc-47fab19c1259/9919d320828d2b5d7b8b?bookmarkGuid=ac7cf54d-b9e5-4a1b-a82e-43a30b0c402a&bookmarkUsage=1&ctid=b093bf19-c75b-4900-86fb-1aed2b3b9caa&portalSessionId=5aebc67b-47fa-4604-9df8-4bf8b4b60c2b&fromEntryPoint=export

---

## **Problem Statement**

The **Ola Data Analyst Project** aims to provide insights into ride management by analyzing customer ratings, booking statuses, cancellations, and order values. The dashboard helps identify areas where the company can improve customer satisfaction, reduce delays, and boost sales during peak times such as weekends and match days. With this project, the company can enhance its customer service, better manage resources, and reduce cancellations.

**Key Business Logic** includes:
- Orders cancelled by customers should be no more than 7%.
- Orders cancelled by drivers should be no more than 18%.
- Increase orders on weekends and match days.
- Keep incomplete rides under 6%.


---

## **SQL Queries & Tasks**

### **SQL Tasks**:

1. **Retrieve all successful bookings:**
    ```sql
    SELECT * FROM bookings WHERE Booking_Status = 'Success';
    ```
Ans - ![Screenshot 2024-11-23 220045](https://github.com/user-attachments/assets/f11fd856-a70a-45b9-927d-e4fff49d9a63)

2. **Find the average ride distance for each vehicle type:**
    ```sql
    SELECT Vehicle_Type, AVG(Ride_Distance) as avg_distance FROM bookings GROUP BY Vehicle_Type;
    ```
Ans - ![Screenshot 2024-11-23 220106](https://github.com/user-attachments/assets/1af37746-11c9-42a7-abba-ff4bd0833ace)

3. **Get the total number of cancelled rides by customers:**
    ```sql
    SELECT COUNT(*) FROM bookings WHERE Booking_Status = 'Cancelled by Customer';
    ```
Ans - ![Screenshot 2024-11-23 220122](https://github.com/user-attachments/assets/ed9063b4-87a6-4f6d-a269-294a0bdcfad0)

4. **List the top 5 customers who booked the highest number of rides:**
    ```sql
    SELECT Customer_ID, COUNT(Booking_ID) as total_rides FROM bookings GROUP BY Customer_ID ORDER BY total_rides DESC LIMIT 5;
    ```
Ans - ![Screenshot 2024-11-23 220137](https://github.com/user-attachments/assets/6fe85281-f522-45fc-a59b-f1867c72aa9a)

5. **Get the number of rides cancelled by drivers due to personal and car-related issues:**
    ```sql
    SELECT COUNT(*) FROM bookings WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';
    ```
Ans -![Screenshot 2024-11-23 220137](https://github.com/user-attachments/assets/6fe85281-f522-45fc-a59b-f1867c72aa9a)

6. **Find the maximum and minimum driver ratings for Prime Sedan bookings:**
    ```sql
    SELECT MAX(Driver_Ratings) as max_rating, MIN(Driver_Ratings) as min_rating FROM bookings WHERE Vehicle_Type = 'Prime Sedan';
    ```
Ans - ![Screenshot 2024-11-23 220208](https://github.com/user-attachments/assets/933ebace-d367-48a5-b86c-2527e36e3965)

7. **Retrieve all rides where payment was made using UPI:**
    ```sql
    SELECT * FROM bookings WHERE Payment_Method = 'UPI';
    ```
Ans - ![Screenshot 2024-11-23 220543](https://github.com/user-attachments/assets/b78b9a59-bfc8-4ad6-a2f6-764443301f58)

8. **Find the average customer rating per vehicle type:**
    ```sql
    SELECT Vehicle_Type, AVG(Customer_Rating) as avg_customer_rating FROM bookings GROUP BY Vehicle_Type;
    ```
Ans - ![Screenshot 2024-11-23 220652](https://github.com/user-attachments/assets/a5155abc-025a-4d2c-b173-29c041eb6153)

9. **Calculate the total booking value of rides completed successfully:**
    ```sql
    SELECT SUM(Booking_Value) as total_successful_value FROM bookings WHERE Booking_Status = 'Success';
    ```
Ans - ![Screenshot 2024-11-23 220742](https://github.com/user-attachments/assets/e18e7cf5-7a9c-4a4c-8528-cc3504a67a25)

10. **List all incomplete rides along with the reason:**
    ```sql
    SELECT Booking_ID, Incomplete_Rides_Reason FROM bookings WHERE Incomplete_Rides = 'Yes';
    ```
Ans -![Screenshot 2024-11-23 220822](https://github.com/user-attachments/assets/d55459c9-5966-47e7-94f1-ce7c53652551)

---

## **Power BI Visualizations**

### **Power BI Visualizations**:

1. **Ride Volume Over Time**  
   A time-series chart showing the number of rides per day/week.

2. **Booking Status Breakdown**  
   A pie or doughnut chart displaying the proportion of different booking statuses (success, cancelled by customer, cancelled by driver, etc.).

Ans- ![Screenshot 2024-11-23 224048](https://github.com/user-attachments/assets/604440c4-766b-4696-9ecb-104c9d53b71b)

3. **Top 5 Vehicle Types by Ride Distance**  
   A bar chart ranking vehicle types based on the total distance covered.

Ans- ![Screenshot 2024-11-23 224113](https://github.com/user-attachments/assets/11944b81-1496-4d4a-a40c-1b75815e12bc)

4. **Average Customer Ratings by Vehicle Type**  
   A column chart showing the average customer ratings for different vehicle types.

5. **Cancelled Rides Reasons**  
   A bar chart highlighting the common reasons for cancellations by customers and drivers.

6. **Revenue by Payment Method**  
   A stacked bar chart displaying total revenue based on payment methods (Cash, UPI, Credit Card, etc.).

Ans- ![Screenshot 2024-11-23 224131](https://github.com/user-attachments/assets/ae0198d4-164a-447e-a379-4e86c9075465)

7. **Top 5 Customers by Total Booking Value**  
   A leaderboard visual listing customers who have spent the most on bookings.

8. **Ride Distance Distribution Per Day**  
   A histogram or scatter plot showing the distribution of ride distances for different Dates.

Ans-![Screenshot 2024-11-23 224147](https://github.com/user-attachments/assets/17757ab2-8e25-469e-afb8-c405cd775a6c)

9. **Driver Ratings Distribution**  
   A box plot visualizing the spread of driver ratings for different vehicle types.

10. **Customer vs. Driver Ratings**  
   A scatter plot comparing customer and driver ratings for each completed ride, analyzing correlations.

Ans- ![Screenshot 2024-11-23 224200](https://github.com/user-attachments/assets/8aa20712-4eb0-4460-b3c9-061f757bdfab)
---



## **Database Setup**

```sql
CREATE DATABASE Ola;
USE Ola;

-- Create Views for SQL Queries
CREATE VIEW Successful_Bookings AS
SELECT * FROM bookings WHERE Booking_Status = 'Success';

CREATE VIEW ride_distance_for_each_vehicle AS
SELECT Vehicle_Type, AVG(Ride_Distance) as avg_distance FROM bookings GROUP BY Vehicle_Type;

CREATE VIEW cancelled_rides_by_customers AS
SELECT COUNT(*) FROM bookings WHERE Booking_Status = 'Cancelled by Customer';

CREATE VIEW Top_5_Customers AS
SELECT Customer_ID, COUNT(Booking_ID) as total_rides FROM bookings GROUP BY Customer_ID ORDER BY total_rides DESC LIMIT 5;

CREATE VIEW Rides_cancelled_by_Drivers_P_C_Issues AS
SELECT COUNT(*) FROM bookings WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';

CREATE VIEW Max_Min_Driver_Rating AS
SELECT MAX(Driver_Ratings) as max_rating, MIN(Driver_Ratings) as min_rating FROM bookings WHERE Vehicle_Type = 'Prime Sedan';

CREATE VIEW UPI_Payment AS
SELECT * FROM bookings WHERE Payment_Method = 'UPI';

CREATE VIEW AVG_Cust_Rating AS
SELECT Vehicle_Type, AVG(Customer_Rating) as avg_customer_rating FROM bookings GROUP BY Vehicle_Type;

CREATE VIEW total_successful_ride_value AS
SELECT SUM(Booking_Value) as total_successful_ride_value FROM bookings WHERE Booking_Status = 'Success';

CREATE VIEW Incomplete_Rides_Reason AS
SELECT Booking_ID, Incomplete_Rides_Reason FROM bookings WHERE Incomplete_Rides = 'Yes';
```

---

## **Conclusion**

This project integrates **SQL** queries for data retrieval with **Power BI** visualizations to provide insights into Ola’s booking and order management system. The analysis helps improve customer service, reduce cancellations, increase bookings during peak times, and optimize order value distribution.

---
