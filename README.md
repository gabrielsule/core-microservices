# coreServices

#### descargar el .net SDK
http://bit.ly/2LE5i4B

#### descargar Docker para Windows
https://dockr.ly/2XJoiVz


#### corroborar las instalaciones
````
dotnet

docker --version
````

#### crear webAPI
```
dotnet new webapi -o coreService --no-https

cd coreService

code .

```

#### crear archivo DockerFile
```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY coreService.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c release -o /app

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "coreService.dll"]
```

#### crear archivo .dockerignore
```
Dockerfile
[b|B]in
[O|o]bj
```

#### crear imágen de Docker
```
docker build -t coreservice .
```

#### listar imágenes
```
docker images
```

#### ejecutar imágen y navegarla
```
docker run -it --rm -p 3000:80 --name coreservicecontainer coreservice
```

http://localhost:3000/api/values
