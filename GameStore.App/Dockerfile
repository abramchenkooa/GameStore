﻿FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["GameStore.App/GameStore.App.csproj", "GameStore.App/"]
RUN dotnet restore "GameStore.App/GameStore.App.csproj"
COPY . .
WORKDIR "/src/GameStore.App"
RUN dotnet build "GameStore.App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GameStore.App.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GameStore.App.dll"]
