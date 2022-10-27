FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /app
EXPOSE 80/tcp

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["all-spice.csproj", "./"]
RUN dotnet restore "all-spice.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "all-spice.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "all-spice.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "all-spice.dll"]
