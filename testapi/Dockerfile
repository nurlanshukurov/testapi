# Build aşaması
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Proje dosyasını kopyala ve restore et
# Projenin tam adıyla .csproj dosyasını kopyala
COPY ["testapi/testapi.csproj", "./"]

# Restore işlemi
RUN dotnet restore

# Diğer dosyaları kopyala ve projeyi build et
COPY . .
RUN dotnet publish -c Release -o /app/out

# Runtime aşaması
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Build aşamasından çıkan dosyaları kopyala
COPY --from=build /app/out .

# Port açıklığı (8080)
EXPOSE 8080

# Uygulamayı başlat
ENTRYPOINT ["dotnet", "testapi.dll"]
