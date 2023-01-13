FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PaymentsConsumer/PaymentsConsumer.csproj", "PaymentsConsumer/"]
RUN dotnet restore "PaymentsConsumer/PaymentsConsumer.csproj"
COPY . .
WORKDIR "/src/PaymentsConsumer"
RUN dotnet build "PaymentsConsumer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PaymentsConsumer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PaymentsConsumer.dll"]
