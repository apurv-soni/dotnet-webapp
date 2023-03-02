FROM mcr.microsoft.com/dotnet/core/sdk:6.0 AS build-env
WORKDIR /MVC_Core_WebApp

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:6.0
WORKDIR /MVC_Core_WebApp
COPY --from=build-env /MVC_Core_WebApp/out .
ENTRYPOINT ["dotnet", "MVC_Core_WebApp.dll"]