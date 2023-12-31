#Base image olarak aspnet 5.0 ı kullanıyoruz
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build


#imajın /app klasörü içerisinde çalışacağını söyledik.
WORKDIR /app

#webapinin proje dependencylerinin tutulduğu dosyayı app klasörüne kopyaladık
COPY *.csproj .

# restore ile dependencylerin indirilmesini sağladık
run dotnet restore

# tüm dependencyleri app'ın altına kopyaladık.
COPY . ./

# projeyi publish ettik
RUN dotnet publish --no-restore -c Release -o out

#yukarda kodlarımızı build ettik şimdi runtime işlemlerini yapalım.
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
COPY --from-build-env 	/app/out .

#testapp.dll i çalıştır.
ENTRYPOINT ["dotnet", "testapp.dll"]