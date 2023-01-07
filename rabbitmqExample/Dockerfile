FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["rabbitmqExample/rabbitmqExample.csproj", "rabbitmqExample/"]
RUN dotnet restore "rabbitmqExample/rabbitmqExample.csproj"
COPY . .
WORKDIR "/src/rabbitmqExample"
RUN dotnet build "rabbitmqExample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "rabbitmqExample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "rabbitmqExample.dll"]
