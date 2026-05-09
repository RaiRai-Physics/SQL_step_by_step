CREATE OR REPLACE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    state VARCHAR(50),
    segment VARCHAR(30),
    signup_date DATE
);

CREATE OR REPLACE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price NUMBER(10,2),
    cost NUMBER(10,2)
);

CREATE OR REPLACE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    status VARCHAR(30),
    total_amount NUMBER(10,2)
);

CREATE OR REPLACE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    unit_price NUMBER(10,2)
);

INSERT INTO customers VALUES
(1, 'Asha Patel', 'Dallas', 'TX', 'Retail', '2025-01-12'),
(2, 'Miguel Torres', 'Austin', 'TX', 'Retail', '2025-01-20'),
(3, 'Priya Shah', 'Chicago', 'IL', 'SMB', '2025-02-03'),
(4, 'Noah Kim', 'Dallas', 'TX', 'Retail', '2025-02-15'),
(5, 'Hana Lee', 'Seattle', 'WA', 'Enterprise', '2025-03-01'),
(6, 'Omar Khan', 'Chicago', 'IL', 'SMB', '2025-03-10'),
(7, 'Emma Brown', 'Boston', 'MA', 'Retail', '2025-03-22'),
(8, 'Leo Martin', 'Austin', 'TX', 'Retail', '2025-04-05'),
(9, 'Sara Ahmed', 'Seattle', 'WA', 'SMB', '2025-04-14'),
(10, 'Daniel Chen', 'Denver', 'CO', 'Retail', '2025-05-08'),
(11, 'Maya Singh', 'Phoenix', 'AZ', 'Retail', '2025-05-12');

INSERT INTO products VALUES
(101, 'Laptop', 'Electronics', 900.00, 650.00),
(102, 'Headphones', 'Electronics', 120.00, 70.00),
(103, 'Coffee Maker', 'Home', 80.00, 45.00),
(104, 'Desk Chair', 'Furniture', 150.00, 90.00),
(105, 'Notebook', 'Stationery', 5.00, 2.00),
(106, 'Monitor', 'Electronics', 250.00, 170.00),
(107, 'Backpack', 'Accessories', 60.00, 35.00),
(108, 'Standing Desk', 'Furniture', 400.00, 260.00),
(109, 'Keyboard', 'Electronics', 75.00, 40.00),
(110, 'Water Bottle', 'Accessories', 25.00, 10.00);

INSERT INTO orders VALUES
(1001, 1, '2025-01-18', 'Completed', 1020.00),
(1002, 2, '2025-01-21', 'Completed', 85.00),
(1003, 1, '2025-02-10', 'Completed', 325.00),
(1004, 3, '2025-02-14', 'Cancelled', 150.00),
(1005, 4, '2025-02-20', 'Completed', 425.00),
(1006, 5, '2025-03-02', 'Completed', 1300.00),
(1007, 6, '2025-03-12', 'Completed', 185.00),
(1008, 2, '2025-03-25', 'Returned', 250.00),
(1009, 3, '2025-04-01', 'Completed', 300.00),
(1010, 7, '2025-04-04', 'Completed', 60.00),
(1011, 9, '2025-04-18', 'Completed', 580.00),
(1012, 4, '2025-05-03', 'Completed', 975.00),
(1013, 6, '2025-05-07', 'Pending', 80.00),
(1014, 10, '2025-05-08', 'Completed', 145.00),
(1015, 5, '2025-05-10', 'Completed', 725.00),
(1016, 1, '2025-05-18', 'Completed', 90.00),
(1017, 8, '2025-06-01', 'Completed', 275.00);

INSERT INTO order_items VALUES
(1001, 101, 1, 900.00),
(1001, 102, 1, 120.00),
(1002, 103, 1, 80.00),
(1002, 105, 1, 5.00),
(1003, 106, 1, 250.00),
(1003, 109, 1, 75.00),
(1004, 104, 1, 150.00),
(1005, 108, 1, 400.00),
(1005, 110, 1, 25.00),
(1006, 101, 1, 900.00),
(1006, 108, 1, 400.00),
(1007, 102, 1, 120.00),
(1007, 107, 1, 60.00),
(1007, 105, 1, 5.00),
(1008, 106, 1, 250.00),
(1009, 104, 1, 150.00),
(1009, 109, 1, 75.00),
(1009, 110, 3, 25.00),
(1010, 107, 1, 60.00),
(1011, 108, 1, 400.00),
(1011, 103, 1, 80.00),
(1011, 107, 1, 60.00),
(1011, 105, 8, 5.00),
(1012, 101, 1, 900.00),
(1012, 109, 1, 75.00),
(1013, 103, 1, 80.00),
(1014, 102, 1, 120.00),
(1014, 110, 1, 25.00),
(1015, 106, 1, 250.00),
(1015, 108, 1, 400.00),
(1015, 109, 1, 75.00),
(1016, 103, 1, 80.00),
(1016, 105, 2, 5.00),
(1017, 106, 1, 250.00),
(1017, 110, 1, 25.00);
