FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AnalyticsConsumer/AnalyticsConsumer.csproj", "AnalyticsConsumer/"]
RUN dotnet restore "AnalyticsConsumer/AnalyticsConsumer.csproj"
COPY . .
WORKDIR "/src/AnalyticsConsumer"
RUN dotnet build "AnalyticsConsumer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AnalyticsConsumer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AnalyticsConsumer.dll"]
