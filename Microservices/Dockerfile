# Use the official .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy the solution and project files
COPY Microservices.sln .
COPY Microservices/*.csproj ./Microservices/

# Restore dependencies
RUN dotnet restore

# Copy the rest of the application files
COPY Microservices ./Microservices/

# Build the application in Release mode
RUN dotnet publish -c Release -o out

# Use a smaller runtime image for the final stage
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app

# Copy the published application from the build stage
COPY --from=build /app/out .

# Expose port 80 for the application
EXPOSE 80

# Set the entry point to run the application
ENTRYPOINT ["dotnet", "Microservices.dll"]
