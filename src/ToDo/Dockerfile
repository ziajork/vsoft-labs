# Etap 1: Budowanie aplikacji
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

# Kopiowanie plików projektu i przywracanie zależności
COPY *.csproj ./
RUN dotnet restore

# Kopiowanie pozostałych plików i kompilacja aplikacji
COPY . ./
RUN dotnet publish -c Release -o /out

# Etap 2: Tworzenie finalnego obrazu
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

# Kopiowanie skompilowanej aplikacji z poprzedniego etapu
COPY --from=build /out .

# Ustawienie domyślnej komendy uruchamiającej aplikację
ENTRYPOINT ["dotnet", "TodoApi.dll"]
# RUN dotnet run ToDoApi.dll