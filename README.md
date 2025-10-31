<div align="center">
  <img height="260" src="https://github.com/tsotneforester/infiniteJSTasks/assets/79293287/1cc7c4f6-0317-4e86-bead-11b50bc8cd97">

  <h1>Infinite-PostgreSQL</h1>

</div>

<p>

---

### 🟢 01

```txt
DB: store/customers
Task: Who between the ages of 30 and 50 has an income less than 50 000?
```

<details><summary><b>Answer</b></summary>

```sql
SELECT count(*)
FROM customers
where age between 30 and 50 and income < 50000
```

</details>

---

### 🟢 02

```txt
DB: store/customers
Task: What is the average income between the ages of 20 and 50? (Including 20 and 50)
Expected: 59361.926
```

<details><summary><b>Answer</b></summary>

```sql
SELECT avg(income)
FROM customers where age between 20 and 50;
```

</details>

---

### 🟢 03

```txt
DB: store/customers
Task: How many female customers do we have from the state of Oregon (OR)?
Expected: 106
```

<details><summary><b>Answer</b></summary>

```sql
SELECT COUNT(firstName) FROM customers WHERE gender = 'F' and state = 'OR';
```

</details>

---

### 🟢 04

```txt
DB: store/products
Task: Create a case statement that's named "price class" where if a product is over 20 dollars you show 'expensive', if it's between 10 and 20 you show 'average' and of is lower than or equal to 10 you show 'cheap'
```

<details><summary><b>Answer</b></summary>

```sql
SELECT prod_id, title, price,
    CASE
      WHEN  price > 20 THEN 'expensive'
      WHEN  price <= 10 THEN  'cheap'
      WHEN  price BETWEEN 10 and 20  THEN 'average'
    END AS "price class"
FROM products
```

</details>

---

### 🟢 05

```txt
DB: World/country
Task: get a list of distinct life expectancy ages, make sure there are no nulls
```

<details><summary><b>Answer</b></summary>

```sql
SELECT DISTINCT lifeexpectancy
FROM country
WHERE lifeexpectancy IS NOT NULL
ORDER BY lifeexpectancy;
```

</details>

---

### 🟢 06

```txt
DB: Store/orders
Task: How many orders were made by customer 7888, 1082, 12808, 9623
Expected: 6
```

<details><summary><b>Answer</b></summary>

```sql
SELECT COUNT(orderid)
FROM orders
WHERE customerid IN (7888, 1082, 12808, 9623)
```

</details>

---

### 🟢 07

```txt
DB: Employees/Employees
Task: How many people's name start with A and end with R?
Expected: 1846
```

<details><summary><b>Answer</b></summary>

```sql
SELECT count(emp_no)
FROM employees
WHERE first_name ILIKE 'A%R';
```

</details>

---

### 🟢 08

```txt
DB: Employees/Employees
Task: How many people's name has 5 characters endin with 'gi'?
Expected: 2 - Luigi, Sergi
```

<details><summary><b>Answer</b></summary>

```sql
SELECT distinct first_name
FROM employees
where first_name ilike '___gi';
```

</details>

---

### 🟢 09

```txt
DB: World/country
Task: Set default life expectancy to 10 where no info is provided, sort by acsanding life expectancy
```

<details><summary><b>Answer</b></summary>

```sql
SELECT name, coalesce(lifeexpectancy, 10) as year FROM country order by year;
```

</details>

---

### 🟢 10

```txt
DB: Employees/Employees
Task: Sort employees by first name ascending and last name descending
```

<details><summary><b>Answer</b></summary>

```sql
SELECT * FROM employees ORDER BY first_name ASC, last_name DESC;
```

</details>

---

### 🟢 11

```txt
DB: Employees/Employees
Task: Sort employees who's name starts with a "k" by hire_date
```

<details><summary><b>Answer</b></summary>

```sql
SELECT * FROM employees
WHERE first_name ILIKE 'k%'
ORDER BY hire_date;
```

</details>

---

### 🟢 12

```txt
DB: Store/products
Task: Add column 'updated_special' and show NULL when the product is not on special (0)
```

<details><summary><b>Answer</b></summary>

```sql
SELECT prod_id, title, price, NULLIF(special, 0) as "updated_special"
FROM products
```

</details>

---

# Text Functions

```sql
-- Create a table for practicing text functions
CREATE TABLE text_functions_practice (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(100),
    email VARCHAR(100),
    product_code VARCHAR(50),
    description TEXT,
    messy_text VARCHAR(100),
    phone_raw VARCHAR(20)
);

-- Insert sample data
INSERT INTO text_functions_practice (full_name, email, product_code, description, messy_text, phone_raw) VALUES
('JOHN SMITH', 'JOHN.SMITH@EXAMPLE.COM', 'PROD-001-2023', 'This is a sample product description with multiple words.', '   Hello World!!!   ', '5551234567'),
('mary jones', 'mary.jones@test.org', 'item-042-2024', 'Another EXAMPLE text for testing FUNCTIONS.', '---test-data---', '5559876543'),
('DAVID Wilson', 'DAVID.Wilson@DEMO.NET', 'CAT-789-2022', 'Mixed CASE example for TEXT manipulation.', '123abc456def', '5554567890'),
('sarah brown', 'sarah.brown@sample.com', 'prod-156-2023', 'Simple text for basic operations.', '  spaced  out  ', '5552345678'),
('MICHAEL Davis', 'MICHAEL.DAVIS@TEST.ORG', 'ITEM-999-2024', 'Final demonstration text for exercises.', 'clean', '5553456789');
```

### 🟢 01

```txt
Task: Convert all emails to lowercase
Expected: 'john.smith@example.com', 'mary.jones@test.org', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT LOWER(email) FROM text_functions_practice;
```

</details>

---

### 🟢 02

```txt
Task: Convert product codes to uppercase
Expected: 'PROD-001-2023', 'ITEM-042-2024', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT UPPER(product_code) FROM text_functions_practice;
```

</details>

---

### 🟢 03

```txt
Task: Convert full names to proper case (first letter capitalized)
Expected: 'John Smith', 'Mary Jones', 'David Wilson', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT INITCAP(full_name) FROM text_functions_practice;
```

</details>

---

### 🟢 04

```txt
Task: Show full names and their lengths
Expected: 'JOHN SMITH' | 10, 'mary jones' | 10, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT full_name, LENGTH(full_name) FROM text_functions_practice;
```

</details>

---

### 🟢 05

```txt
Task: Concatenate full name and email with format: "Name (Email)"
Expected: 'JOHN SMITH (JOHN.SMITH@EXAMPLE.COM)', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT CONCAT(full_name, ' (', email, ')') FROM text_functions_practice;
```

</details>

---

### 🟢 06

```txt
Task: Concatenate with separator: full_name + ' - ' + product_code
Expected: 'JOHN SMITH - PROD-001-2023', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT CONCAT_WS(' - ', full_name, product_code) FROM text_functions_practice;
```

</details>

---

### 🟢 07

```txt
Task: Pad phone numbers to 15 characters with leading zeros
Expected: '0000005551234567', '0000005559876543', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT LPAD(phone_raw, 15, '0') FROM text_functions_practice;
```

</details>

---

### 🟢 08

```txt
Task: Pad product codes to 20 characters with trailing hyphens
Expected: 'PROD-001-2023-------', 'item-042-2024-------', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT RPAD(product_code, 20, '-') FROM text_functions_practice;
```

</details>

---

### 🟢 09

```txt
Task: Extract first 3 characters from product codes
Expected: 'PRO', 'ite', 'CAT', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT LEFT(product_code, 3) FROM text_functions_practice;
```

</details>

---

### 🟢 10

```txt
Task: Extract last 4 characters from product codes (year)
Expected: '2023', '2024', '2022', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT RIGHT(product_code, 4) FROM text_functions_practice;
```

</details>

---

### 🟢 11

```txt
Task: Extract middle part of product code (between first and second dash)
Expected: '001', '042', '789', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT SPLIT_PART(product_code, '-', 2) FROM text_functions_practice;
```

</details>

---

### 🟢 12

```txt
Task: Split email into username and domain
Expected: 'JOHN.SMITH' | 'EXAMPLE.COM', 'mary.jones' | 'test.org', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT SPLIT_PART(email, '@', 1) as username, SPLIT_PART(email, '@', 2) as domain FROM text_functions_practice;
```

</details>

---

### 🟢 13

```txt
Task: Get the second word from descriptions
Expected: 'is', 'EXAMPLE', 'CASE', 'text', 'demonstration'
```

<details><summary><b>Answer</b></summary>

```sql
SELECT SPLIT_PART(description, ' ', 2) FROM text_functions_practice;
```

</details>

---

### 🟢 14

```txt
Task: Remove all leading/trailing spaces from messy_text
Expected: 'Hello World!!!', '---test-data---', '123abc456def', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT TRIM(messy_text) FROM text_functions_practice;
```

</details>

---

### 🟢 15

```txt
Task: Remove only leading spaces from messy_text
Expected: 'Hello World!!!   ', '---test-data---', '123abc456def', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT LTRIM(messy_text) FROM text_functions_practice;
```

</details>

---

### 🟢 16

```txt
Task: Remove only trailing spaces from messy_text
Expected: '   Hello World!!!', '---test-data---', '123abc456def', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT RTRIM(messy_text) FROM text_functions_practice;
```

</details>

---

### 🟢 17

```txt
Task: Remove all hyphens from product codes
Expected: 'PROD0012023', 'item0422024', 'CAT7892022', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT REPLACE(product_code, '-', '') FROM text_functions_practice;
```

</details>

---

### 🟢 18

```txt
Task: Replace 'EXAMPLE' with 'SAMPLE' in descriptions (case-sensitive)
Expected: 'This is a sample product description...', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT REPLACE(description, 'EXAMPLE', 'SAMPLE') FROM text_functions_practice;
```

</details>

---

### 🟢 19

```txt
Task: Translate all vowels in full_name to uppercase (a->A, e->E, etc.)
Expected: 'JOHN SMITH', 'mAry jOnEs', 'DAvID WilsOn', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT TRANSLATE(full_name, 'aeiou', 'AEIOU') FROM text_functions_practice;
```

</details>

---

### 🟢 20

```txt
Task: Reverse the full_name
Expected: HTIMS NHOJ', 'senoj yram', 'nosliW divaD', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT REVERSE(full_name) FROM text_functions_practice;
```

</details>

---

### 🟢 21

```txt
Task: Find position of first '@' symbol in emails
Expected: 11, 11, 13, 12, 13
```

<details><summary><b>Answer</b></summary>

```sql
SELECT POSITION('@' IN email) FROM text_functions_practice;
```

</details>

---

### 🟢 22

```txt
Task: Find position of 'text' in descriptions (using STRPOS)
Expected: 0, 18, 26, 12, 0
```

<details><summary><b>Answer</b></summary>

```sql
SELECT STRPOS(description, 'text') FROM text_functions_practice;
```

</details>

---

### 🟢 23

```txt
Task: Format phone numbers as (XXX) XXX-XXXX
Expected: '(555) 123-4567', '(555) 987-6543', etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT CONCAT('(', LEFT(phone_raw, 3), ') ', SUBSTRING(phone_raw FROM 4 FOR 3), '-', RIGHT(phone_raw, 4)) FROM text_functions_practice;
```

</details>

---

# Math

```sql
-- Create a table for practicing math functions
CREATE TABLE math_functions_practice (
    id SERIAL PRIMARY KEY,
    product_name VARCHAR(100),
    price DECIMAL(10,2),
    quantity INTEGER,
    discount_percent DECIMAL(5,2),
    weight_kg DECIMAL(8,3),
    temperature_celsius DECIMAL(5,2),
    sales_amount DECIMAL(10,2),
    measurement_value DECIMAL(8,4),
    employee_id INTEGER,
    department VARCHAR(50)
);

-- Insert sample data
INSERT INTO math_functions_practice
(product_name, price, quantity, discount_percent, weight_kg, temperature_celsius, sales_amount, measurement_value, employee_id, department) VALUES
('Laptop', 999.99, 5, 10.00, 2.500, 25.50, 1500.75, 15.6789, 101, 'Electronics'),
('Mouse', 25.50, 20, 5.00, 0.250, 22.30, 800.25, 8.9123, 102, 'Electronics'),
('Keyboard', 75.00, 15, 15.00, 1.200, 23.10, 1200.50, 12.3456, 101, 'Electronics'),
('Monitor', 299.99, 8, 20.00, 5.800, 26.70, 950.80, 9.8765, 103, 'Electronics'),
('Desk', 450.00, 3, 25.00, 25.000, 21.50, 675.30, 6.5432, 104, 'Furniture'),
('Chair', 199.99, 10, 10.00, 12.500, 22.80, 450.90, 4.3210, 104, 'Furniture'),
('Notebook', 5.99, 50, 0.00, 0.500, 24.20, 300.45, 3.2109, 105, 'Office Supplies'),
('Pen', 2.49, 100, 2.50, 0.050, 23.90, 125.60, 1.2345, 105, 'Office Supplies'),
('Tablet', 399.99, 12, 12.50, 0.800, 27.30, 1800.20, 18.7654, 101, 'Electronics'),
('Headphones', 89.99, 25, 8.00, 0.450, 25.10, 650.75, 6.7890, 102, 'Electronics');
```

### 🟢 01

```txt
Task: Count total number of products
Expected: 10
```

<details><summary><b>Answer</b></summary>

```sql
SELECT COUNT(*) FROM math_functions_practice;
```

</details>

---

### 🟢 02

```txt
Task: Calculate total value of all inventory (sum of price × quantity)
Expected: ~ 19982.90
```

<details><summary><b>Answer</b></summary>

```sql
SELECT SUM(price * quantity) FROM math_functions_practice;
```

</details>

---

### 🟢 03

```txt
Task: Find the cheapest product price
Expected: 2.49
```

<details><summary><b>Answer</b></summary>

```sql
SELECT MIN(price) FROM math_functions_practice;
```

</details>

---

### 🟢 04

```txt
Task: Find the most expensive product price
Expected: 999.99
```

<details><summary><b>Answer</b></summary>

```sql
SELECT MAX(price) FROM math_functions_practice;
```

</details>

---

### 🟢 05

```txt
Task: Calculate average product price
Expected: ~ 254.893
```

<details><summary><b>Answer</b></summary>

```sql
SELECT AVG(price) FROM math_functions_practice;
```

</details>

---

### 🟢 06

```txt
Task: Calculate absolute value of temperature differences from 25°C
Expected: 0.50, 2.70, 1.90, 1.70, 3.50, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT ABS(temperature_celsius - 25) FROM math_functions_practice;
```

</details>

---

### 🟢 07

```txt
Task: Round all prices to nearest whole number
Expected: 1000, 26, 75, 300, 450, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT ROUND(price) FROM math_functions_practice;
```

</details>

---

### 🟢 08

```txt
Task: Round measurement values to 2 decimal places
Expected: 15.68, 8.91, 12.35, 9.88, 6.54, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT ROUND(measurement_value, 2) FROM math_functions_practice;
```

</details>

---

### 🟢 09

```txt
Task: Get ceiling value of all prices (round up)
Expected: 1000, 26, 75, 300, 450, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT CEIL(price) FROM math_functions_practice;
```

</details>

---

### 🟢 10

```txt
Task: Get floor value of all prices (round down)
Expected: 999, 25, 75, 299, 450, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT FLOOR(price) FROM math_functions_practice;
```

</details>

---

### 🟢 11

```txt
Task: Truncate prices to remove decimal places (no rounding)
Expected: 999, 25, 75, 299, 450, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT TRUNC(price) FROM math_functions_practice;

```

</details>

---

### 🟢 12

```txt
Task: Truncate measurement values to 1 decimal place
Expected: 15.6, 8.9, 12.3, 9.8, 6.5, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT TRUNC(measurement_value, 1) FROM math_functions_practice;
```

</details>

---

### 🟢 13

```txt
Task: Calculate square root of weight_kg
Expected: ~1.581, ~0.500, ~1.095, ~2.408, ~5.000, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT SQRT(weight_kg) FROM math_functions_practice;
```

</details>

---

### 🟢 14

```txt
Task: Calculate price raised to power of 2 (price squared)
Expected: ~999980, 650, 5625, 89994, 202500, etc.
```

<details><summary><b>Answer</b></summary>

```sql
SELECT POWER(price, 2) FROM math_functions_practice;
```

</details>

---

### 🟢 15

```txt
Task: Calculate modulus (remainder) of quantity divided by 3
Expected: 2, 2, 0, 2, 0, 1, 2, 1, 0, 1
```

<details><summary><b>Answer</b></summary>

```sql
SELECT MOD(quantity, 3) FROM math_functions_practice;
```

</details>

---

### 🟢 16

```txt
Task: Generate a random number between 0 and 1 for each product
Expected: Various random numbers between 0-1
```

<details><summary><b>Answer</b></summary>

```sql
SELECT RANDOM() FROM math_functions_practice;
```

</details>

---

### 🟢 17

```txt
Task: Generate random numbers between 1 and 100 for each product
Expected: Various random integers between 1-100
```

<details><summary><b>Answer</b></summary>

```sql
SELECT FLOOR(RANDOM() * 100 + 1) FROM math_functions_practice;
```

</details>

---

# Data

### 🟢 01

```txt
DB: Employees/employees
Task: Get me all the employees above 60, use the appropriate date functions
```

<details><summary><b>Answer</b></summary>

```sql
SELECT AGE(birth_date), * FROM employees
WHERE (
   EXTRACT (YEAR FROM AGE(birth_date))
) > 60 ;

SELECT count(birth_date) FROM employees
WHERE birth_date < now() - interval '61 years' -- 61 years before the current date

```

</details>

---

### 🟢 02

```txt
DB: Employees/employees
Task: How many employees where hired in February?
```

<details><summary><b>Answer</b></summary>

```sql
SELECT count(emp_no) FROM employees
where EXTRACT (MONTH FROM hire_date) = 2;
```

</details>

---

### 🟢 03

```txt
DB: Employees/employees
Task: How many employees were born in november?
```

<details><summary><b>Answer</b></summary>

```sql
SELECT COUNT(emp_no) FROM employees
WHERE EXTRACT (MONTH FROM birth_date) = 11;
```

</details>

---

### 🟢 04

```txt
DB: Employees/employees
Task: Who is the oldest employee?
```

<details><summary><b>Answer</b></summary>

```sql
SELECT MAX(AGE(birth_date)) FROM employees;
```

</details>

---

### 🟢 05

```txt
DB: Store/orders
Task: How many orders were made in January 2004?
```

<details><summary><b>Answer</b></summary>

```sql
SELECT COUNT(orderid)
FROM orders
WHERE DATE_TRUNC('month', orderdate) = date '2004-01-01';

SELECT COUNT(orderid)
FROM orders
WHERE orderdate >= '2004-01-01'
  AND orderdate < '2004-02-01';

SELECT count(*) FROM orders
WHERE (
EXTRACT (YEAR FROM orderdate)
) = 2004 and (
EXTRACT (month FROM orderdate)
) = 1
```

</details>

---

Expected

<!--

### 🟢🔴🟡

```txt

```

<details><summary><b>Answer</b></summary>

```sql

```

</details>

---

-->
