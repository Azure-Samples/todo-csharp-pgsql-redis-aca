FROM --platform=linux/amd64 mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM --platform=linux/amd64 mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Todo.Api.csproj", "./"]
RUN dotnet restore "Todo.Api.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "Todo.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Todo.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Todo.Api.dll"]
