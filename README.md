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
