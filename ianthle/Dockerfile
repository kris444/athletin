FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ianthle/ianthle.csproj ianthle/
RUN dotnet restore ianthle/ianthle.csproj
COPY . .
WORKDIR /src/ianthle
RUN dotnet build ianthle.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ianthle.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ianthle.dll"]
