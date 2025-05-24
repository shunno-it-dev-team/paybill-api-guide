## **ShunnoIT Pay Bill System Documentation (Using bKash Pay Bill API)**

### **Base URL**
All ShunnoIT applications using the bKash Pay Bill system will interact with the following base URL:
```
https://shunnoit.top/shunno-payment/api/v1
```

### **API Endpoints Overview**

- **1. Check Bill**: Query the bill using bKash Pay Bill system.
- **2. Bill Payment**: Make a bill payment via bKash.
- **3. Transaction Search**: Search for the status of a transaction made via bKash.

---

### **1. Check Bill**
- **Endpoint**: `{{BASE_URL}}/bkash/queryBill`
- **Method**: `POST`
- **Description**: This endpoint allows querying a bill by providing the login credentials and reference ID.

#### **Request Parameters**:
| Parameter  | Data Type | Mandatory | Description                                                    | Example     |
|------------|-----------|-----------|----------------------------------------------------------------|-------------|
| UserName   | String    | Yes       | Login identifier for the bKash system                          | bKash       |
| Password   | String    | Yes       | Password associated with the login identifier                  | K38MO3      |
| RefID      | String    | Yes       | Reference ID for the bill issued by the biller                 | NF1000      |

#### **Success Response**:
```json
{
    "ErrorCode": "200",
    "ErrorMsg": "Successful",
    "BillAmount": "1020",
    "QueryTime": "20250419120643"
}
```

#### **Error Response**:
```json
{
    "ErrorCode": "400",
    "ErrorMsg": "Invalid User"
}
```

---

### **2. Bill Payment**
- **Endpoint**: `{{BASE_URL}}/bkash/payBill`
- **Method**: `POST`
- **Description**: This endpoint processes a payment for the bill using bKash.

#### **Request Parameters**:
| Parameter   | Data Type | Mandatory | Description                                                    | Example     |
|-------------|-----------|-----------|----------------------------------------------------------------|-------------|
| UserName    | String    | Yes       | Login identifier for the bKash system                          | bKash       |
| Password    | String    | Yes       | Password associated with the login identifier                  | K38MO3      |
| RefID       | String    | Yes       | Reference ID for the bill issued by the biller                 | NF1000      |
| Amount      | String    | Yes       | The amount to be paid                                          | 1020        |
| TrxId       | String    | Yes       | Transaction ID for the payment                                 | 5C8300HJ6V  |

#### **Success Response**:
```json
{
    "ErrorCode": "200",
    "ErrorMsg": "Successful",
    "TotalAmount": "1020",
    "TrxId": "5C8300HJ6V",
    "MiddlewarePayTime": "20250419120643"
}
```

#### **Error Response**:
```json
{
    "ErrorCode": "400",
    "ErrorMsg": "Invalid RefId"
}

{
    "ErrorCode": "402",
    "ErrorMsg": "Invalid Amount"
}
```

---

### **3. Transaction Search**
- **Endpoint**: `{{BASE_URL}}/bkash/searchTransaction`
- **Method**: `POST`
- **Description**: This endpoint queries the status of a transaction by the transaction ID using bKash.

#### **Request Parameters**:
| Parameter   | Data Type | Mandatory | Description                                                    | Example     |
|-------------|-----------|-----------|----------------------------------------------------------------|-------------|
| UserName    | String    | Yes       | Login identifier for the bKash system                          | bKash       |
| Password    | String    | Yes       | Password associated with the login identifier                  | K38MO3      |
| TrxId       | String    | Yes       | Transaction ID to search for the payment                       | 5C8300HJ6V  |

#### **Success Response**:
```json
{
    "ErrorCode": "200",
    "ErrorMsg": "Successful",
    "TotalAmount": "1020",
    "TrxId": "5C8300HJ6V",
    "MiddlewarePayTime": "20250419120643"
}
```

#### **Error Response**:
```json
{
    "ErrorCode": "400",
    "ErrorMsg": "Invalid Payment"
}
```

---

### **4. Error Codes**
The following error codes may be returned from the API:

| Code  | Message                                    | Description                                                  |
|-------|--------------------------------------------|--------------------------------------------------------------|
| 200   | Success                                    | The transaction was successful.                               |
| 400   | Invalid User                               | The provided user credentials are invalid.                   |
| 400   | Invalid User Or Amount                     | The user credentials or the provided amount are incorrect.   |
| 406   | Mandatory Field Missing                    | A required field (e.g., customer ID, username, password) is missing. |
| 435   | Data Mismatch                              | Data mismatch between the request and the database.          |
| 436   | Already Paid                               | The bill has already been paid.                              |
| 437   | Due Date Over                              | The payment due date has passed.                             |
| 438   | Minimum Amount Not Paid                    | The amount paid is less than the required minimum amount.    |
| 439   | Pay Amount and Biller Amount Do Not Match  | The payment amount does not match the billed amount.         |

---

### **5. Support Contact**

For any integration issues or questions, please contact ShunnoIT:

- **Email**: muhammad.sujon.cse@gmail.com
- **Phone**: +880 1772-703036

Our team is available to assist you with any challenges you may encounter during integration or setup.
