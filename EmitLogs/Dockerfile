FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["EmitLogs/EmitLogs.csproj", "EmitLogs/"]
RUN dotnet restore "EmitLogs/EmitLogs.csproj"
COPY . .
WORKDIR "/src/EmitLogs"
RUN dotnet build "EmitLogs.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EmitLogs.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EmitLogs.dll"]
