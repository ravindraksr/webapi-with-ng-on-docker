FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-alpine AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-alpine AS build
WORKDIR /src
COPY src/WebApi/WebApiWithNgOnDocker.csproj .
RUN dotnet restore

COPY src/WebApi ./WebApi
WORKDIR /src/WebApi
RUN dotnet build --configuration Release --runtime linux-musl-x64 --output /app

FROM build AS publish
WORKDIR /src/WebApi
RUN dotnet publish --configuration Release --runtime linux-musl-x64 --output /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Awaoa.Samples.WebApiWithNgOnDocker.dll"]