# DotNet9 Swagger Integration

This repository demonstrates how to integrate Swagger in a .NET 9 application. In .NET 9, Swagger has been removed from the default template, so this guide will show you how to manually configure and set up Swagger in your .NET 9 project.

## Problem:

In .NET 9, Swagger is no longer part of the default project template. Developers need to manually integrate it for API documentation and testing.

## Solution:

This project provides a step-by-step guide to adding Swagger in .NET 9 API project.

## Getting Started:

Follow these steps to set up Swagger in your .NET 9 application:

1. **Create a new .NET 9 Web API Project:**

   ```
   dotnet new webapi
   ```

2. **Create a new .NET 9 Web API Project:**
   ```
   dotnet add package Swashbuckle.AspNetCore
   ```
3. **Configure Swagger** in `Program.cs`: Open the `Program.cs` file and modify it as follows:

   ```
   var builder = WebApplication.CreateBuilder(args);

   builder.Services.AddOpenApi();

   builder.Services.AddSwaggerGen(); // Add Swagger services

   var app = builder.Build();

   if (app.Environment.IsDevelopment())
   {
       app.MapOpenApi();
       app.UseSwagger();   // Generate Swagger JSON
       app.UseSwaggerUI(); // Serve Swagger UI for interactive API documentation
   }

   app.UseHttpsRedirection();

   var summaries = new[]
   {
       "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
   };

   app.MapGet("/weatherforecast", () =>
   {
       var forecast =  Enumerable.Range(1, 5).Select(index =>
           new WeatherForecast
           (
               DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
               Random.Shared.Next(-20, 55),
               summaries[Random.Shared.Next(summaries.Length)]
           ))
           .ToArray();
       return forecast;
   })
   .WithName("GetWeatherForecast");

   app.Run();

   record WeatherForecast(DateOnly Date, int TemperatureC, string? Summary)
   {
       public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
   }
   ```

4. **Run the application:**
   ```
   dotnet run
   ```
5. **Access Swagger UI:** Once your application is running, navigate to `http://localhost:5002/swagger` to see the Swagger UI.

## Author

- website: [Menayer.com](https://www.menayer.com)
- e-mail: <menayer@outlook.com>
