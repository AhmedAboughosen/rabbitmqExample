FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SecondConsumer/SecondConsumer.csproj", "SecondConsumer/"]
RUN dotnet restore "SecondConsumer/SecondConsumer.csproj"
COPY . .
WORKDIR "/src/SecondConsumer"
RUN dotnet build "SecondConsumer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondConsumer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondConsumer.dll"]
