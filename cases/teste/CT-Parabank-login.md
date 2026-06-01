# 🔐 Login — Test Cases

---

## CT-001 — Login with valid credentials

**Precondition:**  
User is registered and active in the system.

**Test Data:**  
Username: qa.squad@test.com  
Password: Squad@2026  

**Steps:**
1. Navigate to login page  
2. Enter valid username  
3. Enter valid password  
4. Click on "Log In"

**Expected Result:**  
User is successfully authenticated and redirected to the "Accounts Overview" page with account information displayed.

---

## CT-002 — Login with invalid password

**Precondition:**  
User is registered in the system.

**Test Data:**  
Username: qa.squad@test.com  
Password: wrongPassword123  

**Steps:**
1. Navigate to login page  
2. Enter valid username  
3. Enter invalid password  
4. Click on "Log In"

**Expected Result:**  
An error message is displayed:  
"The username and password could not be verified"  
User remains on the login page.
