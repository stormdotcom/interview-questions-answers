# .NET Interview Questions: Essential Topics

## 1. Basics of .NET Framework and .NET Core

### **Q1: What is .NET?**
- **Answer**: .NET is a developer platform by Microsoft for building applications across multiple platforms. It includes frameworks, libraries, and tools for developing web, desktop, mobile, and cloud-based apps.

---

### **Q2: What is the difference between .NET Framework and .NET Core?**
- **Answer**:
  - **.NET Framework**: Windows-only, mature, with a wide range of libraries.
  - **.NET Core**: Cross-platform, modular, open-source, and the foundation for the modern **.NET 5/6+**.

---

### **Q3: What is the CLR?**
- **Answer**: CLR (Common Language Runtime) is the execution engine for .NET applications, providing services like garbage collection, type safety, exception handling, and memory management.

---

## 2. Object-Oriented Programming in .NET

### **Q4: What are the four pillars of OOP?**
- **Answer**: Encapsulation, Inheritance, Polymorphism, and Abstraction.

---

### **Q5: How do you implement inheritance in .NET?**
```csharp
public class Vehicle {
    public void Start() {
        Console.WriteLine("Vehicle started.");
    }
}

public class Car : Vehicle {
    public void Drive() {
        Console.WriteLine("Car is driving.");
    }
}

// Usage
Car car = new Car();
car.Start(); // Inherited method
car.Drive();
```

---

## 3. LINQ (Language Integrated Query)

### **Q6: What is LINQ, and how is it used?**
- **Answer**: LINQ is a feature of .NET for querying collections using a consistent syntax, regardless of the data source (in-memory, database, XML, etc.).

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
var evenNumbers = numbers.Where(n => n % 2 == 0);
Console.WriteLine(string.Join(", ", evenNumbers)); // Output: 2, 4
```

---

## 4. ASP.NET and Web Development

### **Q7: What is ASP.NET?**
- **Answer**: ASP.NET is a framework for building web applications and APIs using .NET. It includes:
  - **ASP.NET Web Forms**: Event-driven, component-based model.
  - **ASP.NET MVC**: Model-View-Controller pattern.
  - **ASP.NET Core**: Modern, cross-platform, lightweight framework.

---

### **Q8: How do you create an API in ASP.NET Core?**
```csharp
[ApiController]
[Route("api/[controller]")]
public class WeatherController : ControllerBase {
    [HttpGet]
    public IEnumerable<string> Get() {
        return new string[] { "Sunny", "Cloudy" };
    }
}
```

---

## 5. Dependency Injection and Services

### **Q9: What is Dependency Injection (DI)?**
- **Answer**: DI is a design pattern used to achieve inversion of control (IoC). It allows dependencies to be provided from the outside rather than being hardcoded.

---

### **Q10: How is DI implemented in ASP.NET Core?**
```csharp
// Register service
services.AddScoped<IMyService, MyService>();

// Use service
public class MyController : ControllerBase {
    private readonly IMyService _myService;

    public MyController(IMyService myService) {
        _myService = myService;
    }

    [HttpGet]
    public string Get() {
        return _myService.GetData();
    }
}
```

---

## 6. Entity Framework Core

### **Q11: What is Entity Framework (EF)?**
- **Answer**: EF is an ORM (Object-Relational Mapper) for .NET that helps developers interact with databases using .NET objects.

---

### **Q12: How do you define a model and context in EF Core?**
```csharp
public class Product {
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}

public class AppDbContext : DbContext {
    public DbSet<Product> Products { get; set; }
}
```

---

## 7. Asynchronous Programming

### **Q13: What is the purpose of `async` and `await` in .NET?**
- **Answer**: They simplify asynchronous programming by allowing non-blocking code execution.

```csharp
public async Task<string> GetDataAsync() {
    await Task.Delay(1000); // Simulate async work
    return "Data fetched";
}
```

---

## 8. Exception Handling

### **Q14: How do you handle exceptions in .NET?**
- **Answer**: Exceptions are handled using `try-catch-finally`.

```csharp
try {
    int result = 10 / 0;
} catch (DivideByZeroException ex) {
    Console.WriteLine($"Error: {ex.Message}");
} finally {
    Console.WriteLine("Execution complete.");
}
```

---

## 9. Memory Management and Garbage Collection

### **Q15: How does garbage collection work in .NET?**
- **Answer**: Garbage Collection (GC) automatically manages memory, reclaiming unused objects and cleaning up resources.

---

### **Q16: What is the `using` statement?**
- **Answer**: It ensures the disposal of resources when no longer needed.

```csharp
using (var file = new StreamWriter("example.txt")) {
    file.WriteLine("Hello, World!");
} // StreamWriter is disposed here.
```

---

## 10. Modern .NET Features (C#)

### **Q17: What is pattern matching in C#?**
```csharp
object obj = 123;

if (obj is int number) {
    Console.WriteLine($"The number is {number}");
}
```

---

### **Q18: What are records in C#?**
```csharp
public record Person(string Name, int Age);

var person = new Person("Alice", 30);
Console.WriteLine(person.Name); // Output: Alice
```

---
