# .NET Coding Best Practices 🚀

## 1️⃣ Follow SOLID Principles
Ensure your code is scalable and maintainable:
- **S**ingle Responsibility: One class, one responsibility.
- **O**pen/Closed: Open for extension, closed for modification.
- **L**iskov Substitution: Subclasses should replace base classes seamlessly.
- **I**nterface Segregation: Keep interfaces small and focused.
- **D**ependency Inversion: Depend on abstractions, not implementations.

```csharp
// ✅ GOOD: Follows SRP (Separate responsibilities)
public class EmailService {
    public void SendEmail(string email) { /* Email logic */ }
}
```

---

## 2️⃣ Use Proper Naming Conventions
- Use **PascalCase** for classes and methods.
- Use **camelCase** for variables and parameters.
- Avoid abbreviations and use meaningful names.

```csharp
// ❌ BAD: Unclear variable names
var dt = DateTime.Now;

// ✅ GOOD: Clear and meaningful
var currentDate = DateTime.Now;
```

---

## 3️⃣ Keep Methods Small & Focused
- A method should perform **only one task**.
- Keep methods **under 20 lines**.
- Reduce the number of parameters.

```csharp
// ❌ BAD: Too much logic in one method
public void ProcessOrder(Order order) {
    ValidateOrder(order);
    SaveOrder(order);
    SendOrderEmail(order);
}

// ✅ GOOD: Break into smaller methods
public void ProcessOrder(Order order) {
    ValidateOrder(order);
    SaveOrder(order);
    NotifyCustomer(order);
}
```

---

## 4️⃣ Use Dependency Injection (DI)
Avoid hardcoded dependencies and use constructor injection.

```csharp
// ❌ BAD: Hardcoded dependency
public class OrderService {
    private EmailService _emailService = new EmailService();
}

// ✅ GOOD: Use dependency injection
public class OrderService {
    private readonly IEmailService _emailService;
    public OrderService(IEmailService emailService) {
        _emailService = emailService;
    }
}
```

---

## 5️⃣ Use Async/Await for Asynchronous Code
Avoid blocking calls (`.Result`, `.Wait()`), and use async methods.

```csharp
// ❌ BAD: Blocking call
var users = dbContext.Users.ToList(); 

// ✅ GOOD: Use async method
var users = await dbContext.Users.ToListAsync();
```

---

## 6️⃣ Handle Exceptions Properly
Use try-catch blocks and log errors properly.

```csharp
// ✅ GOOD: Proper exception handling
try {
    var user = await _userRepository.GetUserById(id);
} catch (Exception ex) {
    _logger.LogError(ex, "Error fetching user");
    throw;
}
```

---

## 7️⃣ Optimize Database Queries
- Use `AsNoTracking()` for read-only queries.
- Implement **pagination**.
- Avoid **N+1 query problems** using `Include()`.

```csharp
// ❌ BAD: Fetching unnecessary data
var users = await _dbContext.Users.ToListAsync();

// ✅ GOOD: Optimize with filters & projection
var users = await _dbContext.Users
    .Where(u => u.IsActive)
    .Select(u => new { u.Id, u.Name })
    .ToListAsync();
```

---

## 8️⃣ Write Unit Tests & Follow TDD
Use `xUnit`, `Moq`, and follow the **Arrange-Act-Assert (AAA)** pattern.

```csharp
[Fact]
public async Task GetUserById_ShouldReturnUser_WhenUserExists() {
    // Arrange
    var userId = 1;
    _userRepoMock.Setup(repo => repo.GetByIdAsync(userId))
                 .ReturnsAsync(new User { Id = userId, Name = "John" });

    // Act
    var result = await _userService.GetUserById(userId);

    // Assert
    Assert.NotNull(result);
    Assert.Equal("John", result.Name);
}
```

---

## 9️⃣ Follow Clean Architecture & Design Patterns
Use **Clean Architecture (Onion, Hexagonal)** and patterns like **Repository Pattern** and **CQRS**.

```
Presentation (Controllers)
    |
Application (Services, DTOs)
    |
Domain (Entities, Interfaces)
    |
Infrastructure (EF Core, APIs, File Storage)
```

---

## 🔟 Keep Your Code DRY, KISS, & YAGNI
✅ **DRY** (Don't Repeat Yourself) → Extract reusable logic.
✅ **KISS** (Keep It Simple, Stupid) → Avoid over-complication.
✅ **YAGNI** (You Ain’t Gonna Need It) → Don’t add unnecessary features.

```csharp
// ❌ BAD: Repeating logic
if (user.Role == "Admin") { /* Do admin tasks */ }
if (user.Role == "User") { /* Do user tasks */ }

// ✅ GOOD: Use a method
public void HandleUserRole(User user) {
    switch (user.Role) {
        case "Admin": // Admin tasks
        case "User": // User tasks
    }
}
```

---

## 📌 Conclusion
By following these **best practices**, you'll write cleaner, more efficient, and scalable .NET code. Happy coding! 🎯🔥

### ⭐ Follow for more: [GitHub Profile](https://github.com/yourusername)
