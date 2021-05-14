FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/query/Microservice.CSharp.QueryingApi/Microservice.CSharp.QueryingApi.csproj", "Microservice.CSharp.QueryingApi/"]
RUN dotnet restore "src/query/Microservice.CSharp.QueryingApi/Microservice.CSharp.QueryingApi.csproj"
COPY . .
WORKDIR "/src/Microservice.CSharp.QueryingApi"
RUN dotnet build "Microservice.CSharp.QueryingApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Microservice.CSharp.QueryingApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Microservice.CSharp.QueryingApi.dll"]
