# Weatherverse Backend

The backend API for the Weatherverse weather application. It is an ASP.NET Core 8 Web API that handles user accounts and roles with ASP.NET Core Identity and stores weather data and favourite cities in MongoDB.

## Features

- **Authentication**: ASP.NET Core Identity API endpoints (`MapIdentityApi`) with Entity Framework Core on SQL Server. The initial migration is in `Migrations/`.
- **Roles**: admin-only role management.
- **Weather data**: saves weather lookups and favourite cities to MongoDB (database `WeatherApplicationDB`, collections `WeatherApplicationData` and `FavoriteCities`).
- **Swagger UI** with a bearer-token security definition, and CORS open to any origin.

## Endpoints

| Controller | Routes |
|---|---|
| Identity API | Registration, login and the other built-in Identity endpoints |
| `User` | `GET` (authenticated) and `POST logout` |
| `Role` | `GET GetRoles` and `POST addRoles` (admin), `GET GetUserRole` (authenticated) |
| `Weather` | `POST add`, `POST favorites` and `GET favorites` |

## Project layout

```
Controllers/   Role, User and Weather controllers
Data/          IdentityDbContext
Migrations/    EF Core migrations
Model/         Request models
Services/      RoleService, MongoWeatherService
Program.cs     Service and middleware setup
```

## Configuration

- `ConnectionStrings:idenitycs` in `appsettings.json` is the SQL Server connection string (the key is spelled this way in the code).
- The MongoDB connection is set in `Services/MongoWeatherService.cs`. Replace it with your own.
- `appsettings.json` also has `BackendUrl` and `FrontendUrl` settings.

## Run

Requires the .NET 8 SDK.

```bash
dotnet restore
dotnet run
```

A newer version of this backend, using PostgreSQL, is in [identity-auth-api](https://github.com/jvishwa06/identity-auth-api).
