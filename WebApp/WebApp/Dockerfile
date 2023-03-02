# Set the base image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

# Set the working directory in the container
WORKDIR /app

# Copy the project files to the container
COPY WebApp/WebApp.csproj ./
RUN dotnet restore

COPY WebApp/ ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .

# Expose the port that the web server will listen on
EXPOSE 80

# Start the web server
ENTRYPOINT ["dotnet", "WebApp.dll"]
