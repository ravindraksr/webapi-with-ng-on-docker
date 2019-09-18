FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-alpine AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-alpine AS stage
WORKDIR /source
COPY src/WebApi/WebApiWithNgOnDocker.csproj .
RUN dotnet restore

FROM stage AS build
COPY /src/WebApi .
RUN dotnet build --configuration Release --runtime linux-musl-x64
RUN dotnet publish --configuration Release --runtime linux-musl-x64 --output artifacts

FROM base AS final
COPY --from=build /source/artifacts /app
ENTRYPOINT ["dotnet", "Awaoa.Samples.WebApiWithNgOnDocker.dll"]