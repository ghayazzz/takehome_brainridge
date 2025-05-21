# 💳 Banking Transactions API

This is a simple Java Spring Boot application that simulates a basic banking system with in-memory data storage. It supports account creation, balance inquiries, and transaction transfers. The project follows a layered architecture using DTOs, services, repositories, and controllers.

---
## 🚀 Features

- Create new bank accounts
- Transfer funds between accounts
- View transaction history per account
- Input validation and error handling
- Swagger UI for API testing
- In-memory data storage (no external DB)
- Rate-limiting and health check

---

## 🧰 Tech Stack

- Java 17
- Spring Boot 3.4.5
- Spring Web, Spring Transactions, Spring Validation
- SpringDoc OpenAPI (Swagger)
- Maven
- Lombok
## 📁 Project Structure
---

```
src/main/java/com/example/banking/
├── controller/
│   ├── AccountController.java
│   └── TransactionController.java
├── dto/
│   ├── AccountCreationRequest.java
│   ├── AccountResponse.java
│   ├── TransactionRequest.java
│   └── TransactionResponse.java
├── exception/
│   ├── AccountNotFoundException.java
│   ├── InsufficientFundsException.java
│   ├── SameAccountTransferException.java
│   └── GlobalExceptionHandler.java
├── model/
│   ├── Account.java
│   └── Transaction.java
├── repository/
│   ├── AccountRepository.java
│   └── TransactionRepository.java
├── service/
│   ├── AccountService.java
│   ├── AccountServiceImpl.java
│   ├── TransactionService.java
│   └── TransactionServiceImpl.java
└── BankingApplication.java
```

---

## 🚀 Getting Started

### ✅ Prerequisites

- Java 17+
- Maven 3.8+
- IDE (IntelliJ or VS Code)
- Browser for Swagger testing

### 🔧 Setup & Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/ghayazzz/takehome_brainridge.git
   cd takehome_brainridge/banking/
   ```

2. **Install dependencies:**
   ```bash
   mvn clean install
   ```

3. **Run the application:**
   ```bash
   mvn spring-boot:run
   ```

4. **Access Swagger UI:**
   Open [http://localhost:8080/swagger-ui/index.html#/](http://localhost:8080/swagger-ui/index.html#/) in your browser or directly access banking/index.html in a browser (make sure to keep the Spring Boot app running).

5. **Health Check:**
   Open [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health) in your browser for health check.

---

## 📘 How It Works

### ▶️ Account API

| Method | Endpoint                  | Description              |
|--------|---------------------------|--------------------------|
| POST   | `/api/accounts`           | Create a new account     |
| GET    | `/api/accounts/{userId}`  | Get account by user ID   |

#### Example: `AccountCreationRequest`
```json
{
  "name": "John Doe",
  "initialBalance": 1000.0
}
```

#### Example: `AccountResponse`
```json
{
  "userId": 1000000,
  "name": "John Doe",
  "balance": 1000.0
}
```

---

### 💸 Transaction API

| Method | Endpoint                                  | Description                         |
|--------|-------------------------------------------|-------------------------------------|
| POST   | `/api/transactions/transfer`              | Transfer money between accounts     |
| GET    | `/api/transactions/history/{accountId}`   | Get transaction history for account |

#### Example: `TransactionRequest`
```json
{
  "fromAccount": 1000000,
  "toAccount": 1000001,
  "amount": 250.0
}
```

#### Example: `TransactionResponse`
```json
{
  "fromAccount": 1000000,
  "toAccount": 1000001,
  "amount": 250.0,
  "timestamp": "2025-05-20T12:00:00Z",
  "status": "SUCCESS"
}
```

---

## 🧪 Testing with Swagger

1. Navigate to: [http://localhost:8080/swagger-ui/index.html#/](http://localhost:8080/swagger-ui/index.html#/)
2. Try the available endpoints by filling in the request bodies and executing the requests directly from the browser.
3. All schema models are defined and documented in the Swagger interface.

---

## ❗ Exception Handling

Your application handles various error scenarios using custom exceptions and a global exception handler:

### 🔸 `AccountNotFoundException`
Thrown when a requested account does not exist.

**Response:**
```json
{
  "timestamp": "2025-05-20T16:00:00Z",
  "status": 404,
  "error": "Not Found",
  "message": "Account with ID 1000002 not found"
}
```

---

### 🔸 `InsufficientFundsException`
Thrown when the sender's account balance is too low to complete a transfer.

**Response:**
```json
{
  "timestamp": "2025-05-20T16:00:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Insufficient funds in account 1000000"
}
```

---

### 🔸 `SameAccountTransferException`
Thrown when the source and destination account IDs in a transfer are the same.

**Response:**
```json
{
  "timestamp": "2025-05-20T16:00:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Cannot transfer to the same account"
}
```

---

### 🔸 `GlobalExceptionHandler`
Handles:
- Input validation errors
- Illegal arguments
- Any unhandled or runtime exceptions

**Example Response (Validation Error):**
```json
{
  "timestamp": "2025-05-20T16:00:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Validation failed: 'name' must not be blank"
}
```

---

## Rate Limiting
<img src="https://github.com/user-attachments/assets/f74ae567-d246-4508-a5fe-5137a0a3404f" width="600" />
<img src="https://github.com/user-attachments/assets/4ce50837-853d-4341-8aa0-947279831832" width="600" style="margin-top: 20px;" />
<img src="https://github.com/user-attachments/assets/4f2c40c9-16f0-4a7c-a663-4ce66f90fb33" width="600" style="margin-top: 20px;" />
<img src="https://github.com/user-attachments/assets/9ce969bb-e9ea-41ec-9333-50acdc699c3e" width="600" style="margin-top: 20px;" />

## 📸 Screenshots

- Swagger UI interface


  ![image](https://github.com/user-attachments/assets/549bafe0-f87f-4d2a-b447-adaf1f6056d0")



  ![image](https://github.com/user-attachments/assets/8b5eca0c-599b-4a14-82fe-5a3df5a8f6de)

- Sample request/response with custom HTML interface for testing


  ![image](https://github.com/user-attachments/assets/bdfc7c79-d3c5-4ee7-82d0-fec446255efd)


  ![image](https://github.com/user-attachments/assets/4f313cd1-0445-4524-a3ae-ee6699732c2f)


If initial balance is not given, it takes 0 by default.

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/44c30687-3833-4893-9ba3-59f869bf2b7c" alt="Image 2" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/a9de939f-cef2-4a56-a74e-89cf813e4178" alt="Image 3" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/cec23574-c818-4e33-9de7-bbe613331889" alt="Image 4" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/15d52c33-8ed2-4349-882e-e982967ed015" alt="Image 6" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/8f849d63-132d-4d71-ae9d-4f1cbc64fe17" alt="Image 5" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/63998ec3-93d8-40ad-8708-47a6964458f8" alt="Image 7" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/0f07f00c-011e-4a02-82b3-29d829c1710e" alt="Image 8" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/56dbd5d8-8721-4b41-b38e-d12ebf0595e3" alt="Image 9" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/56131b1f-f7d9-4b38-815e-25618f9615bd" alt="Image 11" width="100%"/>
</div>

<div style="width: 350px; margin-top: 10px;">
  <img src="https://github.com/user-attachments/assets/34f42894-257c-4f36-b4af-7941f6d8f8e7" alt="Image 10" width="100%"/>
</div>




---

## 🧾 License

This project is for testing purposes only.

---

## 🙋‍♀️ Author

**Mohammed Ghayasuddin** – [GitHub](https://github.com/ghayazzz)

