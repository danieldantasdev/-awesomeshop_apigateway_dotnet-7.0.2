FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["AwesomeShop.Services.ApiGateway/AwesomeShop.Services.ApiGateway.csproj", "AwesomeShop.Services.ApiGateway/"]
RUN dotnet restore "AwesomeShop.Services.ApiGateway/AwesomeShop.Services.ApiGateway.csproj"
COPY . .
WORKDIR "/src/AwesomeShop.Services.ApiGateway"
RUN dotnet build "AwesomeShop.Services.ApiGateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AwesomeShop.Services.ApiGateway.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AwesomeShop.Services.ApiGateway.dll"]
