FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/command/Microservice.CSharp.CommandApi/Microservice.CSharp.CommandApi.csproj", "Microservice.CSharp.CommandApi/"]
RUN dotnet restore "src/command/Microservice.CSharp.CommandApi/Microservice.CSharp.CommandApi.csproj"
COPY . .
WORKDIR "/src/Microservice.CSharp.CommandApi"
RUN dotnet build "Microservice.CSharp.CommandApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Microservice.CSharp.CommandApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Microservice.CSharp.CommandApi.dll"]
