# sql-assignment

 # Project Objectives
The main objectives of this project are:

## 1)Order & Sales Analysis
  Analyze order status over time
 Identify monthly sales and fulfillment trends

## 2) Customer Analysis
    Segment customers into first-time vs repeat
    Track active customers monthly
     Understand customer order frequency and value

### 3) Payment Status Analysis
    Evaluate the distribution of payment statuses
    Identify success/failure rates and related trends

### 4) Order Details Report
Generate a consolidated view of order details per customer


# Approaches 
: for task1 :(Total orders and revenue by order status) Perform a left join between the customer_orders and payments tables to include all orders, then filter to consider only those with payment_status = 'completed'. Grouping by order_status helps us understand fulfillment and performance across different states.
       (Monthly trends of completed status order and total revenue)Truncate payment_date to the month level using DATE_TRUNC then Filter only completed payments and lastly  Aggregate data by: Total number of payments and Total payment amount(revenue)
       (Monthly trends of orders by order status)  Approach :Start with the customer_orders table as it contains order-level data then Use DATE_TRUNC('month', order_date) to group orders by month then Group the data by both month and order_status to see how many orders fall into each status category every month lastly, Use COUNT(*) to calculate the number of orders for each (month, status) combination.

: for task 2 :(Segement customer types as repeat one or first time customers) Used the customer_orders table to analyze how many orders each customer has placed. A CASE statement is used to categorize customers: If the customer has more than one order, they are labeled as 'Repeat Customer'.Otherwise, they are labeled as 'First-time Customer'.COUNT(DISTINCT customer_id) is used to ensure we count unique customers under each category.The query is grouped by the customer_type derived from the CASE logic.
              (Top Customers Revealed: Most Frequent Buyers and Their Lifetime Spending) This query uses the customer_orders table to generate a detailed summary for each customer. By grouping the data using customer_id, we calculate the total number of orders each customer has placed using COUNT(order_id), the total amount they have spent using SUM(order_amount), and identify their first and most recent purchase dates using MIN(order_date) and MAX(order_date). This approach helps in identifying high-value customers, frequent buyers, and understanding the lifecycle and engagement span of each customer.
              (Monthly Active Customers: Tracking Customer Engagement Over Time) This query analyzes customer engagement over time by calculating the number of unique customers who placed at least one order in each month. Using the customer_orders table, we apply DATE_TRUNC('month', order_date) to group orders by month and COUNT(DISTINCT customer_id) to count active customers within each monthly group. This metric is essential for understanding customer retention, identifying periods of high or low activity, and measuring the effectiveness of marketing campaigns over time.

 for task 3:(Count and percentage of each payment status) This query provides a breakdown of payment outcomes by analyzing the payment_status column in the payments table. It calculates the total number of payments under each status using COUNT(*), and computes the percentage share of each status relative to all payments using a subquery. The result highlights the success and failure rates of transactions, helping to detect operational issues, failed transactions, or unusual patterns in the payment process.

 for task 4 : (Monthly Active Customers: Tracking Customer Engagement Over Time) This query merges order data from the customer_orders table with related payment information from the payments table to generate a detailed and comprehensive view of each order. A LEFT JOIN is used to ensure all orders are included, even if a payment hasn’t been made. Key fields such as payment_method, payment_amount, and payment_status are included, along with a derived payment_summary column that simplifies the interpretation of payment outcomes. Orders are sorted in descending order of order_date to prioritize recent activity. This report is useful for customer support, finance tracking, and operational review.
                         

