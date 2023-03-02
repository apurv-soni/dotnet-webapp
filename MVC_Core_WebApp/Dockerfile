FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /src

COPY ["MVC_Core_WebApp.csproj", "MVC_Core_WebApp/"]
# Restore as distinct layers
RUN dotnet restore ./MVC_Core_WebApp.csproj
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /App
COPY --from=build-env /src/out .
ENTRYPOINT ["dotnet", "MVC_Core_WebApp.dll"]