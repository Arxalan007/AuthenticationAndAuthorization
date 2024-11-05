# .NET Core 8 MVC Authentication & Authorization Project

This project demonstrates the implementation of Role-Based Authentication and Authorization in an ASP.NET Core 8 MVC application. It includes user registration, login functionality, and role-based access control.

## Features

- User Registration and Login
- Role-Based Authorization (Admin, User, Manager roles)
- Custom User Properties (FirstName, LastName)
- Remember Me Functionality
- Secure Password Requirements
- Access Denied Handling
- Bootstrap UI Integration
- Initial Admin User Seeding

## Prerequisites

- [.NET SDK 8.0](https://dotnet.microsoft.com/download/dotnet/8.0)
- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) (LocalDB or higher)
- [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/) (recommended) or VS Code

## Getting Started

1. **Clone the Repository**
   ```bash
   git clone [repository-url]
   cd AuthenticationAndAuthorization
   ```

2. **Install Required NuGet Packages**
   ```bash
   dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore --version 8.0.0
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 8.0.0
   dotnet add package Microsoft.EntityFrameworkCore.Tools --version 8.0.0
   ```

3. **Update Database Connection String**
   - Open `appsettings.json`
   - Update the connection string if needed:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=(localdb)\\mssqlLocalDB;Database=AuthenticationAndAuthorization;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
     }
   }
   ```

4. **Apply Database Migrations**
   ```bash
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

5. **Run the Application**
   ```bash
   dotnet run
   ```

## Default Users and Roles

The application automatically creates the following roles on startup:
- Admin
- User
- Manager

A default admin user is created with these credentials:
- Email: admin@example.com
- Password: Admin@123

## Authentication Flow

1. Users can register a new account
2. New users are automatically assigned the "User" role
3. Users can login with their email and password
4. Access to certain controllers/actions is restricted based on roles
5. Unauthorized access attempts are redirected to the Access Denied page

## Role-Based Authorization Examples

```csharp
// Controller level authorization
[Authorize(Roles = "Admin")]
public class AdminController : Controller
{
    // Only accessible by Admin role
}

// Action level authorization
[Authorize(Roles = "Admin,Manager")]
public IActionResult ManageUsers()
{
    // Accessible by both Admin and Manager roles
}
```

## Security Features

- Password Requirements:
  - Minimum length: 8 characters
  - Requires uppercase letter
  - Requires lowercase letter
  - Requires number
  - Requires non-alphanumeric character

- SSL/TLS encryption enabled
- Anti-forgery token validation
- Secure password hashing
- Protection against brute force attacks

## Common Issues and Solutions

1. **Migration Error**
   ```bash
   dotnet ef database update --verbose
   ```

2. **SSL Certificate Error**
   - Ensure `TrustServerCertificate=True` is in your connection string
   - Or properly configure SSL certificates for production

3. **Role Seeding Issues**
   ```bash
   dotnet ef database drop
   dotnet ef database update
   ```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Acknowledgments

- ASP.NET Core Identity Framework
- Bootstrap for UI components
- Microsoft Documentation

## Support

For support, please open an issue in the repository or contact Arxalan.arain987@gmail.com
