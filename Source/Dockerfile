# Build container. Load full SDK as base image.
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# TODO: Adapt the directories!
COPY Seom.Application Seom.Application
COPY Seom.Webapp      Seom.Webapp

# Compile the app
RUN dotnet restore "Seom.Webapp"
RUN dotnet build   "Seom.Webapp" -c Release -o /app/build
RUN dotnet publish "Seom.Webapp" -c Release -o /app/publish /p:UseAppHost=false

# App container. Only needs runtime (smaller image)
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS final
EXPOSE 80
EXPOSE 443
WORKDIR /app

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Seom.Webapp.dll"]
