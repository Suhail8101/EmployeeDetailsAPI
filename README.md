# Employee CRUD API

## Project Overview
The Employee CRUD API is a RESTful API developed using ASP.NET Core and Entity Framework Core (Code First approach). The API facilitates CRUD (Create, Read, Update, Delete) operations on employee records, making it suitable for managing organizational employee data. Additionally, Swagger UI is integrated for interactive testing and documentation of the API.

---

## Technology Stack

- **Framework**: ASP.NET Core 6
- **Database**: SQL Server (handled with Entity Framework Core Code First approach)
- **Documentation and Testing**: Swagger UI

---

## Execution Flow

1. **Client Request**: The client (or user) initiates a request to an API endpoint via Swagger UI or any HTTP client like Postman.
2. **Controller Processing**: The request is routed to the `EmployeeController`, where the appropriate action method (GET, POST, PUT, DELETE) is called based on the request type.
3. **Service Layer**: The controller forwards the request to the Service layer, which contains business logic for handling CRUD operations. Here, the necessary validations and transformations take place.
4. **Data Access via Entity Framework**: The service interacts with Entity Framework Core through the `AppDbContext`, which acts as a bridge between the service layer and the SQL Server database.
5. **Database Operation**: Entity Framework processes the request (e.g., retrieving, creating, updating, or deleting employee data) and returns a response.
6. **Response to Client**: The response, typically in JSON format, is sent back to the client, completing the request lifecycle.

---

## Project Modules and Services

This project is organized into multiple layers for separation of concerns and ease of maintenance.

### 1. **Controllers**
   - **EmployeeController**: Manages all API endpoints related to employee operations (CRUD). Each action method corresponds to an endpoint and performs specific operations by calling services in the service layer.
   
### 2. **Services**
   - **EmployeeService**: Contains the core business logic for employee management. It includes methods to:
     - Retrieve a list of all employees
     - Retrieve a specific employee by ID
     - Add a new employee
     - Update an existing employee’s information
     - Delete an employee by ID
   - The service ensures that all CRUD operations adhere to business rules and performs validations before interacting with the database.

### 3. **Data Layer**
   - **AppDbContext**: The central point for database interactions, defined using Entity Framework. It contains the `DbSet<Employee>` that maps to the Employee table in SQL Server.
   - **Employee Model**: Represents the structure of employee data, including properties like `Id`, `FirstName`, `LastName`, `Email`, `Position`, and `Salary`. The model is used for database mapping and for sending data to/from the client.

---

## How the Project Starts

1. **Initialize**: When the project is run, ASP.NET Core initializes the middleware pipeline. Configurations from `appsettings.json` (such as database connection strings) are loaded.
2. **Database Connection**: Entity Framework Core connects to the SQL Server database based on the connection string provided in `appsettings.json`.
3. **Swagger Setup**: Swagger UI is configured and made available at `https://localhost:5001/swagger`, enabling users to test and visualize the API endpoints.
4. **Controller Registration**: ASP.NET Core identifies and registers the `EmployeeController` as an endpoint, allowing it to handle incoming API requests.
5. **Dependency Injection (DI)**: Services like `EmployeeService` are injected into the controller using ASP.NET Core’s DI container, enabling modular and reusable code.

---

## Getting Started

### Prerequisites

Ensure you have:
- [.NET Core SDK 6 or later](https://dotnet.microsoft.com/download)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- Visual Studio or Visual Studio Code (optional, but recommended)

### Setup Instructions

1. **Clone the Repository**: Clone the project repository from GitHub.

   ```bash
   git clone https://github.com/yourusername/employee-crud-api.git
   cd employee-crud-api





### Create an Employee:

**POST /api/employees**
This endpoint allows you to add a new employee to the database. You provide a JSON object containing the employee's FirstName, LastName, Email, Position, and Salary. The endpoint validates the data and, if valid, saves it to the database.


curl -X POST http://localhost:<port>/api/employees \
-H "Content-Type: application/json" \
-d '{"FirstName":"John", "LastName":"Doe", "Email":"johndoe@example.com", "Position":"Developer", "Salary":60000}'



### Retrieve All Employees:

**GET /api/employees**
This endpoint retrieves a list of all employees currently stored in the database. It’s useful for viewing all employee records at once in a list format.


curl http://localhost:<port>/api/employees



### Update an Employee's Information:

**PUT /api/employees/{id}**
This endpoint updates the details of an existing employee based on their unique ID. You provide a JSON object with updated employee information. This is helpful for updating attributes like the role or salary of an employee.


curl -X PUT http://localhost:<port>/api/employees/1 \
-H "Content-Type: application/json" \
-d '{"FirstName":"John", "LastName":"Doe", "Email":"john.doe@newexample.com", "Position":"Senior Developer", "Salary":70000}'




### Delete an Employee:

**DELETE /api/employees/{id}**
This endpoint deletes an employee record based on their unique ID. This is particularly useful for removing an employee record if they have left the organization.

curl -X DELETE http://localhost:<port>/api/employees/1

