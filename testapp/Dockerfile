#Build imagesi olarak aspnet 5.0 ı kullanıyoruz
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build


#imajın /app klasörü içerisinde çalışacağını söyledik.
WORKDIR /app

#webapinin proje dependencylerinin tutulduğu dosyayı app klasörüne kopyaladık
COPY *.csproj .

# restore ile dependencylerin indirilmesini sağladık
RUN dotnet restore
RUN dotnet add package Microsoft.OpenApi --version 1.2.3

# tüm dependencyleri app'ın altına kopyaladık.
COPY . ./

# projeyi publish ettik
RUN dotnet publish -c Release -o out

#yukarda kodlarımızı build ettik şimdi runtime işlemlerini yapalım.
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app/out .

#testapp.dll i çalıştır.
ENTRYPOINT ["dotnet", "testapp.dll"]