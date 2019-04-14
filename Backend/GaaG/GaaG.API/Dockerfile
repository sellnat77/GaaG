FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["GaaG.API/GaaG.API.csproj", "GaaG.API/"]
RUN dotnet restore "GaaG.API/GaaG.API.csproj"
COPY . .
WORKDIR "/src/GaaG.API"
RUN dotnet build "GaaG.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "GaaG.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GaaG.API.dll"]