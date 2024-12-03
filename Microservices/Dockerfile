# Use the official .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy the project files to the container
COPY *.sln .
COPY Microservices.csproj .
COPY ./ ./

# Restore dependencies
RUN dotnet restore

# Build the application in Release mode
RUN dotnet publish -c Release -o out

# Use a smaller runtime image for the final stage
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app

# Copy the built application from the build stage
COPY --from=build /app/out .

# Expose port 80 for the application
EXPOSE 80

# Set the entry point to run the application
ENTRYPOINT ["dotnet", "Microservices.dll"]
