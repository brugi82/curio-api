FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Curio.Api/Curio.Api.csproj", "Curio.Api/"]
RUN dotnet restore "Curio.Api/Curio.Api.csproj"
COPY . .
WORKDIR "/src/Curio.Api"
RUN dotnet build "Curio.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Curio.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Curio.Api.dll"]