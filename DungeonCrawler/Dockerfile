FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DungeonCrawler/DungeonCrawler.csproj", "DungeonCrawler/"]
RUN dotnet restore "DungeonCrawler/DungeonCrawler.csproj"
COPY . .
WORKDIR "/src/DungeonCrawler"
RUN dotnet build "DungeonCrawler.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DungeonCrawler.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DungeonCrawler.dll"]
