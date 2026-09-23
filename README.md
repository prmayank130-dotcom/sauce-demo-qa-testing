# E-Commerce Web Application Testing (Sauce Demo) & REST API Validation

## Project Overview
This project contains comprehensive manual test cases, defect reports, and API testing scripts for the **SauceDemo E-Commerce Application** and RESTful APIs using **Postman** and **SQL**.

---

## 1. Manual Testing & Test Cases

| Test Case ID | Feature | Description | Pre-conditions | Test Steps | Expected Result | Status |
|-------------|---------|-------------|----------------|------------|-----------------|--------|
| TC_AUTH_01 | Login | Validate login with valid credentials | User on login page | 1. Enter `standard_user`<br>2. Enter `secret_sauce`<br>3. Click Login | User redirected to `/inventory.html` | PASSED |
| TC_AUTH_02 | Login | Validate login with locked-out user | User on login page | 1. Enter `locked_out_user`<br>2. Enter `secret_sauce`<br>3. Click Login | Error: "Epic sadface: Sorry, this user has been locked out." | PASSED |
| TC_CART_01 | Cart | Add item to cart and verify count | Logged-in user | 1. Click "Add to Cart" on item<br>2. Check cart icon badge | Cart badge updates to `1` | PASSED |
| TC_CHECK_01| Checkout | Validate checkout without postal code | Item in cart | 1. Go to Cart -> Checkout<br>2. Fill Name, leave Zip empty<br>3. Click Continue | Error message displayed for Postal Code | PASSED |

---

## 2. API Testing (Postman)

### Endpoints Validated
- **GET** `/api/users?page=2` - Payload structure & status `200 OK`
- **POST** `/api/users` - Create user verification, response payload validation & status `201 Created`
- **PUT** `/api/users/2` - Update user details & status `200 OK`
- **DELETE** `/api/users/2` - Delete resource verification & status `204 No Content`

### SQL Verification Queries
```sql
-- Verify order creation in backend database
SELECT order_id, user_id, total_amount, status 
FROM orders 
WHERE user_id = 101 AND status = 'COMPLETED';

-- Validate user inventory reduction
SELECT product_name, stock_quantity 
FROM products 
WHERE product_id = 502;