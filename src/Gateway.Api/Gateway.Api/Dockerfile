FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY Gateway.Api/Gateway.Api.csproj Gateway.Api/
RUN dotnet restore Gateway.Api/Gateway.Api.csproj
COPY . .
WORKDIR /src/Gateway.Api
RUN dotnet build Gateway.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Gateway.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Gateway.Api.dll"]
