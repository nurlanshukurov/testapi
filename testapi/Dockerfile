# Build aşaması
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Proje dosyalarını kopyalayın ve restore edin
COPY *.csproj .
RUN dotnet restore

# Geri kalan dosyaları kopyalayın ve uygulamayı yayınlayın
COPY . .
RUN dotnet publish -c Release -o out

# Runtime aşaması
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .

# Uygulamayı başlatın
ENTRYPOINT ["dotnet", "testapi.dll"]
