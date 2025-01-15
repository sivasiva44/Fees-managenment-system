# Fee Management System Using Azure

## Project Overview
The **Fee Management System** is a cloud-native solution designed to manage student fee records. The system automates fee notifications, offers secure APIs for managing fee records, and provides role-based access for students and administrators.

## Key Features

### Student Features:
- View fee details and payment status via API.
- Receive automated reminders for pending dues.

### Administrator Features:
- Query student fee details.
- Update fee records securely via API.

## Technical Architecture
The solution uses Azure services to ensure scalability, security, and automation:

1. **Azure SQL Database**: Stores structured data for students and administrators.
2. **Azure Logic Apps**: Automates email reminders for overdue payments.
3. **Azure Functions**: Serverless API for fetching fee details, calculating payment status, and performing fee record updates.
4. **Azure API Management**: Exposes Azure Functions securely with rate-limiting and authentication.
5. **Azure Active Directory (AD)**: Manages role-based access control (RBAC) to secure access for students and admins.

## Architecture Diagram
_Include your architecture diagram here._

## Steps

### Step 1: Azure SQL Database Setup
Create an **Azure SQL Database** with the following tables:

- **Students**: Stores fields like `StudentID`, `Name`, `Course`, `TotalFee`, `PaidAmount`, and `DueDate`.
- **Administrators**: Stores fields like `AdminID`, `Name`, and `Role`.

### Step 2: Automating Fee Reminders
Create a **Logic App** to send fee reminders:

1. **Recurrence**: Schedule (daily, weekly, etc.).
2. **Execute SQL query**: Query overdue students.
3. **For each student**: Loop through results.
4. **Send Email**: Send reminders using Outlook or SendGrid.

#### Example Logic App Workflow:
- Trigger: Runs daily.
- Action: Queries `Students` table for `DueDate < today()` and `PaidAmount < TotalFee`.
- Action: Sends reminder emails to students.

### Step 3: Payment Status API
This API, built using **Azure Functions**, allows students to check their payment status.

- **GET Request**: Fetches fee details based on `StudentID`.
- **Response Example**:

    ```json
    {
      "StudentID": 1,
      "Name": "John Doe",
      "Course": "Computer Science",
      "TotalFee": 10000,
      "PaidAmount": 7000,
      "PaymentStatus": "Partially Paid",
      "DueDate": "2024-12-31T00:00:00Z"
    }
    ```

### Step 4: Secure Admin Operations
Admins can securely update student fee records using an API protected by **Azure AD** for RBAC.

- **POST Request**: Updates fee records.

    ```json
    {
      "StudentID": 123,
      "TotalFee": 12000,
      "PaidAmount": 9000
    }
    ```

The system checks the admin's role through Azure AD before performing the update.

### Step 5: Scalability and Monitoring
- **Application Insights**: Monitors operation success/failure, like fee updates and payment queries.
- **Alerts**: Set up alerts for failed operations to ensure smooth system performance.

## Outcome
The **Fee Management System** is a scalable, secure, and automated platform for managing student fee records. It enables students to view and track fee status in real-time while administrators can securely update records. Automated reminders ensure timely payments, reducing the manual workload. Azure services like **Azure Functions**, **Logic Apps**, **SQL Database**, and **Azure AD** ensure efficiency, security, and data privacy.

## Technologies Used
- **Azure SQL Database**
- **Azure Logic Apps**
- **Azure Functions**
- **Azure API Management**
- **Azure Active Directory (AD)**
- **Application Insights**
