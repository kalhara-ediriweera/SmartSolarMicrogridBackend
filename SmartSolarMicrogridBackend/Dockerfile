# Smart Solar Microgrid API - Render deployment
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY ["SmartSolarMicrogrid.API/SmartSolarMicrogrid.API.csproj", "SmartSolarMicrogrid.API/"]
COPY ["SmartSolarMicrogrid.Application/SmartSolarMicrogrid.Application.csproj", "SmartSolarMicrogrid.Application/"]
COPY ["SmartSolarMicrogrid.Domain/SmartSolarMicrogrid.Domain.csproj", "SmartSolarMicrogrid.Domain/"]
COPY ["SmartSolarMicrogrid.Infrastructure/SmartSolarMicrogrid.Infrastructure.csproj", "SmartSolarMicrogrid.Infrastructure/"]
RUN dotnet restore "SmartSolarMicrogrid.API/SmartSolarMicrogrid.API.csproj"

COPY . .
RUN dotnet publish "SmartSolarMicrogrid.API/SmartSolarMicrogrid.API.csproj" -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:10000
EXPOSE 10000
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "SmartSolarMicrogrid.API.dll"]
